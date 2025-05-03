# VPSの初期設定(Kagoya編)

### 環境情報
Ubuntu server 24.04

### 初回アクセス
```bash
# KEY=KAGOYAで作成したキー
chmod 600 ${KEY} 
ssh -i ${KEY} ubuntu@${IPアドレス} -p 22
```

### ufwの設定（HOST側）
```bash
sudo ufw status
sudo ufw enable
sudo ufw default DENY
sudo ufw limit ${任意のポート}
```


### sshdの変更（HOST側）
※ログアウトしてしまうとログインできなくなってしまうので注意
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

# ssh.socketの変更
sudo vim /usr/lib/systemd/system/ssh.socket

[Socket]
ListenStream=${任意のポート}

# Serviceの再起動
sudo systemctl daemon-reload
sudo systemctl restart ssh

# Post確認
ss -anlt

```

### ユーザー作成
```bash
adduser ${追加するユーザー}
gpasswd -a ${追加するユーザー} sudo
```

### SSHkey作成

```bash
# KEY作成
ssh-keygen -t ed25519 -f id_kagoya_20250415
```

### Public keyをコピー
- Remoteの~/.ssh/authorized_keysに作成したpublickeyを追加

### ssh config作成
```bash
vim ~/.ssh/config

# config
Host kagoya
HostName ${IPアドレス}
Port 22
User ${追加するユーザー}
IdentityFile ~/.ssh/id_kagoya_20250415
ServerAliveInterval 60

# 接続確認
ssh kagoya
```


### 不要なユーザーの削除
```bash
# rootのパスワードoff(lock)
sudo passwd -l root
# ubuntuユーザー削除
sudo deluser --remove-home ubuntu
```