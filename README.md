## 概要

MediaWikiを使用する方法について記載したリポジトリです.

## 環境構築

```shell
$ cd docker

# dockerコンテナを作成します.
$ docker compose up -d

# http://localhostにアクセスして下さい.
# エラーが発生する場合は以下コマンドを実行してコンテナの中に入りコマンドを実行して下さい.
# スキンを追加したのでエラーが発生します.
# コマンドを打つのが面倒くさい場合は、LocalSettings.phpのl.136を削除して下さい.
$ docker exec -it mediawiki bash 
mediawiki# tar -xzf /var/www/html/images/Splash-REL1_39-05b1b03.tar.gz  -C /var/www/html/skins/

# dockerコンテナを削除します.
$ docker compose down --rmi all --volumes --remove-orphans
```

## 参考資料

- [MediaWikiの環境をdocker-composeで簡易的に構築する](https://qiita.com/You_name_is_YU/items/98ad1ee121067c1cdf85)

- [MediaWikiでCSSを編集する方法](https://kw-note.com/cms/edit-mediawiki-css/)

- [docker composeでMediaWikiをインストールする手順](https://mebee.info/2020/08/26/post-13111/)

- [【GitHub】rjg21/mediawiki-mariadb-example](https://github.com/rjg21/mediawiki-mariadb-example)
