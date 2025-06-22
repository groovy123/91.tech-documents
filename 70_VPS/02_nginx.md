# nginxについて

### インストール
公式ページに従う


### 起動、停止、確認
```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl reload nginx
sudo systemctl status nginx
```

### 注意点
#### スラッシュ問題
https://gigazine.net/news/20230708-nginx-alias-traversal/

- locationとaliasの末尾には両方/をつける！


### 各ディレクトリ
- /usr/sbin/nginx
- /etc/nginx
- /usr/shere/nginx/html
  - /var/www/プロジェクトコードに変更すべき⇛FHS3.0
- /var/log/nginx
- /etc/logrotate.d/nginx
- /usr/lib/nginx
  - 動的モジュール置き場。nginx -Vコマンドで確認できる。
- /var/lib/nginx
  - モジュール別の作業用ディレクトリ
- /etc/init.d/nginx
- /etc/ufw/applications.d/nginx

```bash
ln -s /etc/nginx nconf
ln -s /var/log/nginx nlog

```

### Cerbot

