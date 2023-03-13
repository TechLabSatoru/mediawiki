## 概要

MediaWikiを使用する方法について記載したリポジトリです.

## 環境構築

```shell
$ cd docker

# dockerコンテナを作成します.
$ docker compose up -d

# http://localhostにアクセスして下さい.

# dockerコンテナを削除します.
$ docker compose down --rmi all --volumes --remove-orphans
```

## 参考資料

- [MediaWikiの環境をdocker-composeで簡易的に構築する](https://qiita.com/You_name_is_YU/items/98ad1ee121067c1cdf85)

- [MediaWikiでCSSを編集する方法](https://kw-note.com/cms/edit-mediawiki-css/)

- [docker composeでMediaWikiをインストールする手順](https://mebee.info/2020/08/26/post-13111/)

- [【GitHub】rjg21/mediawiki-mariadb-example](https://github.com/rjg21/mediawiki-mariadb-example)
