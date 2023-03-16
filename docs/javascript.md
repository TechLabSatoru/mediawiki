
## 概要

- JavaScriptをあてる方法について検証を行う.

## 実行方法

- 登録したユーザでログインして下さい.

- http://localhost/index.php/MediaWiki:Common.jsへアクセスして下さい.

    - 特定のページにあてたい場合は、`http://<ホスト名>/index.php/<ページ名>/MediaWiki:Common.js`を利用して下さい.

- 画面右上の編集タブを押下して下さい.

- CSSを記載して、`ページを保存`ボタンを押下して下さい.

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

## 特定のページにJSをあてる方法

- JSをあてるページである`http://localhost/index.php/Example`へアクセスします.

- `http://localhost/index.php/MediaWiki:Common.js`へアクセスします.

- 下記の中にJavaScriptを記載します.

```javascript
if (mw.config.get('wgPageName') === 'Example') {
  function importArticles() {
      var args = Array.prototype.slice.call(arguments),
          articles = [],
          i;
      for (i = 0; i < args.length; i++) {
          if (Array.isArray(args[i])) {
              articles = articles.concat(args[i]);
          } else if (typeof args[i] === 'string') {
              articles.push(args[i]);
          }
      }
      return mw.loader.load(articles);
  }

  // Load some MediaWiki modules using mw.loader.using
  mw.loader.using(['jquery', 'mediawiki.util'], function () {

      // Add some event listeners to the document when it is ready
      $(document).ready(function () {

          // Make the tabs at the top of the page clickable and show which one is selected
          var tabs = document.querySelectorAll('span[role="tab"]');
          for (var i = 0; i < tabs.length; i++) {
              tabs[i].addEventListener('click', function () {
                  var selectedTab = document.querySelector('span[role="tab"][aria-selected="true"]');
                  if (selectedTab) {
                      selectedTab.setAttribute('aria-selected', 'false');
                  }
                  this.setAttribute('aria-selected', 'true');
              });
          }

          // Load another JavaScript file that contains a library of functions used by the whole site
          mw.loader.load('MediaWiki:Gadget-site-lib.js');

      });

  });
}
```
