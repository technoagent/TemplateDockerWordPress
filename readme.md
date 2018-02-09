# DockerによるWordPress構築テンプレート

参考URL

[https://docs.docker.com/compose/wordpress/]
(https://docs.docker.com/compose/wordpress/)
## 1. 起動について

コンテナ群のバックグラウンド起動
※このリポジトリのルートディレクトリで実行する


```
docker-compose up -d
```

以下のURLで管理画面を表示できる

[http://localhost:8300/wp-admin](http://localhost:8300/wp-admin)


## 2. ファイルの共有について

各コンテナはホストに対し以下のようにマウントする

- wordpressコンテナ(webサーバ)のドキュメントルート(/var/www/html)はローカルのwordpressディレクトリ
- dbコンテナ(DBサーバ)のmysqlデータ(/var/lib/mysql)はローカルのdb_dataディレクトリ
- dbコンテナ(DBサーバ)の「/tmp/sqls」ディレクトリはローカルのsqlsディレクトリ（sqlファイル等をDBサーバで実行するため）

##　3. コマンド

DBサーバにログイン

```
docker exec -it templatedockerwordpress_db_1 /bin/bash
```
※　「templatedockerwordpress_db_1」が異なっている場合は、コンテナIDを指定

ローカルのsqlをコンテナ上で実行
```
cd /tmp/sqls
mysql -u wordpress -h db  -p wordpress < xxxxxxxxx.sql

```

## 3. 停止、削除について


コンテナ群の停止

```
docker-compose stop
```

コンテナ群の削除

```
docker-compose down
```

## 4. DBクライアントツールについて

localhost:33306でmysqlに接続できるので、[Sequel Pro](https://www.sequelpro.com/)等で接続できる


