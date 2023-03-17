## 概要

- JavaScriptをあてる方法について記載します.

## 全てのページにJavaScriptをあてる方法

- 登録したユーザでログインして下さい.

- http://localhost/index.php/MediaWiki:Common.jsへアクセスして下さい.

- 画面右上の編集タブを押下して下さい.

- JavaScriptを記載して、`ページを保存`ボタンを押下して下さい.

## 特定のページにJavaScriptを当てる方法

MediaWikiで特定のページにJavaScriptを適用するには、以下の手順を実行します。

1. テーマのカスタマイズを有効にするために、LocalSettings.phpファイルを開きます。

2. 次の行を追加します。

```php
$wgAllowUserJs = true;
```

これにより、各ユーザーが自分のユーザー名前前にある「User:」ページで自分のカスタムJavaScriptを使用できるようになります。

3. 特定のページにJavaScriptを適用するには、MediaWiki:Common.jsページを編集します。

4. 例えば、ページ名が「Example」の場合、以下のコードを追加します。

```javascript
if (mw.config.get('wgPageName') === 'Example') {
  // JavaScript code for the Example page
  // ...
}
```

このJavaScriptは、ページ名が「Example」の場合に適用されます。条件文でページ名を取得するために、mw.config.get('wgPageName')を使用します。

5. 変更を保存し、特定のページにJavaScriptが適用されることを確認してください。

注意：ページ名にスペースが含まれる場合は、「_」に置き換えてください。例えば、「Example Page」の場合は「Example_Page」として指定します。また、特定のページだけでなく、全てのページにJavaScriptを適用したい場合は、MediaWiki:Common.jsを編集してください。
