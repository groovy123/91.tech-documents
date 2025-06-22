# OCIに関すること

### チュートリアル
https://oracle-japan.github.io/ocitutorials/beginners/



### インスタンスに接続
```bash
ssh ubuntu@${インスタンスのIPアドレス}
```


### スワップファイル作成
```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo systemctl daemon-reload
sudo swapon /swapfile

echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### ネットワークセキュリティグループ変更
管理画面のNetworking -> Vritual Cloud Networks -> TutorialVCN -> Security
Instances -> 対象のインスタンス -> Networking -> Network security groups


### IPTablesについて
```bash
#INPU, FORWARD, OUTPUTチェインを確認する場合
sudo iptables -nL
sudo iptables -nL INPUT

sudo vim /etc/iptables/rules.v4
sudo iptables-restore < /etc/iptables/rules.v4

sudo service iptables restart
```


