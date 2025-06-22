# LXDについて

### インストール
https://lxd-ja.readthedocs.io/ja/latest/installing/


### 仮想マシン作成
```bash
# イメージの検索
lxc image list ubuntu: 24.04 amd64
# イメージの起動
lxc launch ubuntu:24.04 ${コンテナ名}

# インスタンス確認
lxc list

# インスタンスの操作
lxc start/stop/pause/delete ${コンテナ名}

# shellログイン
lxc shell ${コンテナ名}

```

### VSコード接続
```bash
# rootログインを許可する
vim /etc/ssh/sshd_config.d/10-basic.conf

# 10-basic.confに以下設定
PermitRootLogin yes
KbdInteractiveAuthentication yes

# rootのパスワード設定
sudo passwd root

# sshdの再起動
systemctl restart ssh

# sshでログイン
ssh root@${仮想マシンのIPアドレス}

# キーペアの作成
ssh-keygen -t ed25519 -f ~/.ssh/id_lxc_dev01
# 仮想マシンにpublicキー登録
ssh-copy-id -i ~/.ssh/id_lxc_dev01 root@${仮想マシンのIPアドレス}

# sshconfig追加
vim ~/.ssh/config

# ~/.ssh/configに以下追加
Host lxc_dev01
  HostName ${仮想マシンのIPアドレス}
  User root
  port 22
  IdentityFile ~/.ssh/id_lxc_dev01

# ログイン確認
ssh lxc_dev01
```

### ファイルの受け渡し
```bash
コンテナからファイルを取得する
lxc file pull コンテナ名/フルパス 保存先

コンテナにファイルを渡す
lxc file push ファイル コンテナ名/フルパス
```

### LXDのコンテナ内でDockerを使う
```bash
lxc config set dev02 security.nesting=true security.syscalls.intercept.mknod=true security.syscalls.intercept.setxattr=true
lxc restart dev02
```


### ポートマッピングの追加
コンテナ内で起動したportをHost側に公開する
```bash
# 80ポートの公開
lxc config device add dev01 webapp01 proxy listen=tcp:0.0.0.0:3000 connect=tcp:127.0.0.1:3000 bind=host

lxc config device add dev02 http proxy listen=tcp:0.0.0.0:80 connect=tcp:127.0.0.1:80 bind=host
lxc config device add dev02 https proxy listen=tcp:0.0.0.0:443 connect=tcp:127.0.0.1:443 bind=host
lxc config device add dev02 webapp01 proxy listen=tcp:0.0.0.0:8080 connect=tcp:127.0.0.1:8080 bind=host
lxc config device add dev02 webapp02 proxy listen=tcp:0.0.0.0:13000 connect=tcp:127.0.0.1:13000 bind=host
lxc config device add dev02 webapp03 proxy listen=tcp:0.0.0.0:10000 connect=tcp:127.0.0.1:10000 bind=host

# 確認
lxc config device show dev01
lxc config device show dev02

# 削除
lxc config device rm dev02 http https
```