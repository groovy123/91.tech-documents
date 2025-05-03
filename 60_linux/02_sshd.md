# SSH関連

### ssh.confとsshd.confの違い
- /etc/ssh配下にはssh.confとsshd.confがある
- ssh.confは外に接続するための設定
- sshd.confはsshデーモンの設定（受け付ける側）

### Host側で準備するのも
```bash
cd ${HOME}
mkdir .ssh
chmod 700 .ssh
vim .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
```

### コマンド
```bash
sudo sshd -t
sudo systemctl restart ssh
```


### 停止するもの
```bash
# sshd設定ファイル作成
vim /etc/ssh/sshd_config.d/01-basic.conf

PubkeyAuthentication yes
ChallengeResponseAuthentication no
PermitEmptyPasswords no
PermitRootLogin no
PasswordAuthentication no
KbdInteractiveAuthentication no
UsePAM no
X11Forwarding no
AllowUsers ${USER}

Port ${任意のポート}


```
※ UsePAMをnoにするとパスワードを設定していないユーザーはログインできなくなる
