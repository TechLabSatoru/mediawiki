## 概要

- CSSをあてる方法について記載します.

## 全てのページにJavaScriptをあてる方法

- 登録したユーザでログインして下さい.

- `http://localhost/index.php/MediaWiki:Common.css`へアクセスして下さい.

- 画面右上の編集タブを押下して下さい.

- CSSを記載して、`ページを保存`ボタンを押下して下さい.

## 特定のページにCSSを当てる方法

1. テーマのカスタマイズを有効にするために、LocalSettings.phpファイルを開きます。

2. 次の行を追加します。

```php
$wgAllowUserCss = true;
```

これにより、各ユーザーが自分のユーザー名前前にある「User:」ページで自分のカスタムCSSを使用できるようになります。

3. 特定のページにCSSを適用するには、MediaWiki:Common.cssページを編集します。

4. 例えば、ページ名が「Example」の場合、以下のコードを追加します。

```css
body.page-Example {
  background-color: #fff;
  color: #000;
}
```
このCSSは、ページ名が「Example」の場合に適用されます。CSSの適用先は、ページ名に対応する「page-」プレフィックスで指定されます。

5. URLが`http://localhost/index.php/利用者:FSDS/example/`の場合は、以下のコードでCSSを当てることが可能です.

```shell
body.page-利用者_FSDS_example {
  /* CSS rules */
  /* ... */
}
```

6. 変更を保存し、特定のページにCSSが適用されることを確認してください。

注意：ページ名にスペースが含まれる場合は、「_」に置き換えてください。例えば、「Example Page」の場合は「Example_Page」として指定します。

## 参考資料

- [MediaWikiでCSSを編集する方法](https://kw-note.com/cms/edit-mediawiki-css/)
