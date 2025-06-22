# Dockerについて

### 滅びの呪文
```bash
docker compose down --rmi all --volumes --remove-orphans
```

### Dockerコマンド
```bash
docker image ls
docker image rm [オプション] image_name


# httpd
docker image pull httpd
docker container run -d -p 8080:80 httpd
docker container ls
docker container stop a4698f54d68f

# DockerContainerの削除
docker ps -a
docker stop $(docker ps -q)
docker rm $(docker ps -aq)
```


### Docker vlumeについて
Dockerストレージは３種類ある
- ボリューム
  /var/lib/docker/volumes配下に作られる。名前付きと匿名ボリュームがある
- バインドマウント
  ホスト側のディレクトリをコンテナ内のディレクトリと共有する
- tmpfs
  オンメモリ

-vオプションについて
```bash
# 匿名ボリューム
docker container run -v /volume1 httpd
# 名前付きボリューム
docker container run -v name1:/volume1 httpd
# バインドマウント
docker container run -v /path/to/name1:/volume1 httpd

```