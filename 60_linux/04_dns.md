# 家庭内DNSサーバーの作成

### 参考
https://gihyo.jp/admin/serial/01/ubuntu-recipe/0834


### DNSサーバーとは・・・
以下２つの役割がある
- コンテンツサーバー
  - ドメインの名前情報を管理するサーバーで、インターネット全体に対してサービスを提供する必要がある
- キャッシュサーバー
  - クライアントはキャッシュサーバーに対してリクエストを投げ、実際の名前解決はキャッシュサーバーがクライアントの代理として行う
  - ルーターがキャッシュサーバーを兼ねていることが多い。
  - 家庭内のLANでは使用するDNSサーバーとしてルーターのIPアドレスが指定されているのが一般的

### 家庭内にDNSサーバーを立てることによって
- 接続ログを確認できる
- 家庭内ネットワークでもドメインを使える
- 特定のドメインをブロックできる


### Unboundのインストール
```bash
# インストール
sudo apt install -U -y unbound

# 起動確認
sudo ss -lutnp

# DNS確認
dig google.com
dig -x 1.1.1.1
dig -x 1.1.1.2
dig -x 1.1.1.3

```


### 固定IPにする
ネットワーク > 設定 > IPv4
| 項目 | 値 |
| -- | -- |
| IPv4メソッド | 手動 |
| アドレス | 任意のアドレス(192.168.12.2) |
| ネットマスク | 255.255.255.0 |
| ゲートウェイ | ルーターのアドレス(192.168.12.1) |
| DNS | ルーターのアドレス(192.168.12.1) |

接続断　⇛　接続でインターネット接続確認


### 自分のIPの確認
```bash
networkctl status
```


### unbound.conf作成
```bash
# ファイル作成
vim /etc/unbound/unbound.conf.d/10_my_unbound.conf

# ファイルの中身
server:
	interface: 自分自身のIPアドレス
	port: 53
	access-control: 127.0.0.0/8 allow
	access-control: LANのネットワークアドレス/サブネットマスク allow
	use-syslog: yes
	log-queries: yes
	hide-version: yes
	hide-identity: yes

forward-zone:
	name: "."
 	forward-addr: フォワード先のプライマリDNS
 	forward-addr: フォワード先のセカンダリDNS

# 再起動
sudo systemctl restart unbound.service 

```


### IPアドレスとサブネットマスク
192.168.90がネットワークアドレスの場合、書き方は以下になる（どちらでも良い）
- 192.168.90.0/255.255.255.0
- 192.168.90.0/24

下の書き方は、255.255.255.0を32bitの2進数で考えると最上位から24bitが全部1といっている。
- 255.255.255.0 ⇛ 10進数表現
- 11111111 11111111 11111111 00000000 ⇛ 2進数表現


### ログの出力先設定
```bash
vim /etc/rsyslog.d/30-unbound.conf

# 設定内容
if $syslogfacility-text == 'daemon' and $programname contains 'unbound' then 
  -/var/log/unbound/unbound.log
& ~

# サービスの再起動
sudo systemctl restart rsyslog.service
```

### ログローテションの設定
```bash
vim /etc/logrotate.d/unbound

# 設定内容
/var/log/unbound/unbound.log
{
        rotate 30
        daily
        copytruncate
        compress
        su root syslog
        postrotate
        	/usr/lib/rsyslog/rsyslog-rotate
        endscript
}
```

### 特定ドメインのブロック
