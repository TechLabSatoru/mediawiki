## 概要

MediaWikiにおいて、ユーザがカスタマイズされたテーマをページ上で指定する方法について検証します.条件は以下です.

- 管理者はカスタムテーマを記載するだけであり、ユーザ自身で指定することができる様にします.

    - 管理者がユーザごとに指定することは可能ですが、ユーザからの依頼に適時CSSやJavaScriptを記載する必要があり管理が煩雑になるため、管理者依存は避ける必要があります.

- 基本的に管理者が編集できる場所は、MediaWiki:Common.cssとMediaWiki:Common.jsの2点です.

    - LocalSettings.phpに静的な記載を行うことは可能ですが、動的に記載する方法は推奨されていません.

## 対応案

上記対応案について、いくつか記載します.全てを検証してはないですが、他の実装方法もあるということを頭の片隅にでも留めておいて下さい.

- `MediaWiki:Common.css`と`MediaWiki:Common.js`にユーザごとの設定を記載する.

    - Pros
        
        - 1つのCSS・JavaScriptファイルに集約させることが出来ます.

    - Cons

        - ユーザ特定のCSSやJavaScriptを使用したい際は管理ユーザとコンタクトを取る必要があります.

- `/var/www/html/skins`配下に作成したスキンを追加します.`LocalSettings.php`に`wfLoadSkin( '<スキン名>' );`を挿入することで作成したスキンを選択することが出来ます.

    - Pros

        - **概要**で記載した要件を満たしており、個人的には最も素晴らしい実現方法です.

        - [スキンコードコレクション](https://phabricator.wikimedia.org/source/skins/)にコードが記載されています.

    - Cons

        - 技術要件が高すぎるため、気軽にスキンを作成することが不可能です.

        - 簡単なスキンを実装するには向いていないと思います.

- <font color="#EF858C">今回、採用した方法です.</font>`MediaWiki:Common.css`と`MediaWiki:Common.js`を変数化・関数化とすることで、`User:<ユーザ名>:common.css`と`User:<ユーザ名>:common.js`で特定のクラスや関数を再利用可能にします.`MediaWiki:Common.css`・`MediaWiki:Common.js`は管理ユーザが指定することが可能であり、全ページに適用されるCSSとJavaScriptです.`User:<ユーザ名>:common.css`・`User:<ユーザ名>:common.js`は、利用ユーザごとに用意されているCSSとJavaScriptであり、ユーザ自身のページのみで適用されるCSSとJavaScriptです.

    - Pros

        - **概要**で記載した要件を満たしている.

        - 簡単なカスタム要素を作成する際には適している.

    - Cons

        - 複雑なスキンを作成するには向いていない気がします.

        - 簡単とはいえ、技術要件は中程度ですが、CSSやJavaScriptを学びながら実装を行うことは可能だと思います.

## 簡単な実装案（目標）

- CSSを使用して、bodyタグのバックグラウンドカラーを変更します.

- JavaScriptを使用して、全ての内容が`Hello World`という文字列に変換されます.

## 簡単な実装案（具体例）

### 事前準備

- LocalSettings.phpに以下のコードを記載する必要があります.

    - 記載する場所はどこでも良いですが、保守性の観点からファイル最下部に記載することをおすすめします.

```php
# ユーザ独自にCSSとJavaScriptをあてることができる様にします.
$wgAllowUserCss = true;
$wgAllowUserJs = true;
```

### CSS

- `MediaWiki:Common.css`で以下のコードを記載して下さい.

    - 下記コードはグラデーションカラーを変数として定義しています.

```css
:root {
  --main-color: #7117ea;
  --sub-color:  #ea6060;
  --bg-gradation: linear-gradient(135deg, var(--main-color) 0%, var(--sub-color) 100%) fixed;
}
```

- `User:<ユーザ名>:common.css`に以下のコードを記載して下さい.

    - `body`タグに`MediaWiki:Common.css`で定義したグラデーションカラーを適用します.

    - ここで定義したものは、ユーザ自身のページでしか適用されません.

```css
body {
  background: var(--bg-gradation);
}
```

以上、よろしくお願いします.

### JavaScript

- `MediaWiki:Common.js`で以下のコードを記載して下さい.

    - 下記関数は、MediaWikiに記載した内容が`Hello World`に変換されます.

```javascript
function changeText(className) {
  var elements = document.getElementsByClassName(className);
  for (var i = 0; i < elements.length; i++) {
    elements[i].textContent = "Hello World";
  }
}
```

- `User:<ユーザ名>:common.js`に以下のコードを記載して下さい.

    - `mw-content-ltr`クラスで指定されたものは、たとえどの様な内容であっても`Hello World`と変換されます.

    - ここで定義したものは、ユーザ自身のページでしか適用されません.

```javascript
changeText("mw-content-ltr");
```

## まとめ

- 高度な技術お持ちの方は、カスタムスキンを作成して`/var/www/html/skins`配下に配置して下さい.

- 簡単に独自カスタムを実行して見たい場合は、今回ご紹介した方法で行うのが良いと思います.

- 個人的にもフロントエンドが得意ではないこともあり少しばかり苦戦しましたが、普段あまり触れない場所であり、初めてのMediaWikiだったので、楽しく検証を行うことが出来ました.

- 他にも良い方法がありましたら`issues`などで教えて頂けると幸いです.
