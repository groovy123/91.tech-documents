# UFWのはなし

### 基本コマンド
```bash

sudo ufw status

# ufwの有効化
sudo ufw enable

# 外部からの通信をすべて拒否する
# すべてタイムアウトする設定
sudo ufw default DENY

# 接続頻度を制限してportを開く
sudo ufw limit 22

# Numberを表示して削除する
sudo ufw status numbered
sudo ufw delete 1

# ルールの追加
sudo ufw allow 80
sudo ufw deny 80
sudo ufw reject 80

# reload
sudo ufw reload

```