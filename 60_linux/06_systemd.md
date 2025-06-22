# Systemdについて

### サービス登録
```bash
# serviceファイル作成
sudo vim /etc/systemd/system/fastapi.service

# fastapi.serviceの内容
[Unit]
Description=FastAPI
After=syslog.target network.target

[Service]
Type=simple
WorkingDirectory=${PATH_TO_PROJECT_DIR}
ExecStart=${PATH_TO_PROJECT_DIR}/.venv/bin/uvicorn main:app --host=0.0.0.0 --port=8007
KillMode=process
Restart=always
User=${EXECUTE_USER}
Group=root

[Install]
WantedBy=multi-user.target
```


### サービスの有効化
```bash
sudo systemctl daemon-reload
sudo systemctl enable fastapi.service
sudo systemctl start fastapi.service
sudo systemctl status fastapi.service
```

### ログファイルの確認
```bash
# 全部のログ表示
journalctl
# 特定のサービスのログを表示
journalctl -u fastapi
# 特定のメッセージの優先度のみ表示。
# "emerg","alert","err","warning","notice","info","debug"が指定可能
journalctl -p err
# 日付指定
journalctl --until="today"
journalctl --since="yesterday"
```