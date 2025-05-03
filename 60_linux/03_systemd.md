# systemdまとめ

### systemdとは
- PIDが1のプロセス。一番最初に起動
- Unitという単位で管理される
- /etc/systemd/system
  - ユーザーが変更する場所
- /usr/bin/lib/systemd/system
  - デフォルト設定。変更しない

### Unitの操作
```bash
# Unitの一覧表示
systemctl list-unit-files
# Unitの自動起動
systemctl enable/disable <UNIT>
# Unitの手動制御
systemctl start/stop/restart <UNIT>
```


### 設定ファイルを変更させるには
例）eginxの場合

- 設定ファイル（/etc/nginx/nginx.conf）を変更した場合
  ```bash
  # 再起動だけでOK
  systemctl restart nginx
  ```

- Unitファイル（*.service や *.timer）を変更した場合
  ```bash
  # daemonのreload + 再起動が必要
  systemctl daemon-reload
  systemctl restart nginx
  ```
