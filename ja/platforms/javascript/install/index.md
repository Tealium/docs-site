---
title: インストール
description: JavaScript（Web）用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/javascript/install/
---
## インストール

### ユニバーサルデータオブジェクト (`utag_data`)

ユニバーサルデータオブジェクト（UDO）は、`utag_data`というJavaScriptオブジェクトで、ウェブページからTealiumタグに動的データが渡されます。このオブジェクトのプロパティは、ビジネスに特有のプレーンでベンダーニュートラルな用語を使用して命名されます。

以下は、ユニバーサルタグ `utag.js` の読み込み _前_ に `utag_data` を宣言する例です：

```html
<!-- Tealium Universal Data Object -->
<script type="text/javascript">
  var utag_data={
      "page_type"     : "section",
      "site_section"  : "men",
      "page_name"     : "Men's Fashion | Acme Inc.",
      "country_code"  : "US",
      "currency_code" : "USD"};
</script>
```
詳細はこちら：

* [データレイヤーの仕組み](https://docs.tealium.com/how-the-data-layer-works-for-websites/)
* [`utag_data`](https://docs.tealium.com/ja/platforms/javascript/about-utag-data/)

### ユニバーサルタグ (`utag.js`)

ユニバーサルタグは、`utag.js`と呼ばれる小さなJavaScriptコードで、サイトにサードパーティのタグを読み込むために必要なすべての生成コードを含んでいます。Tealium iQタグ管理がタグを発火させるために、以下のコードをページに挿入します：

```html
<!-- Tealium Universal Tag -->
<script type="text/javascript">
  (function(a,b,c,d) {
      a='//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js';
      b=document;c='script';d=b.createElement(c);d.src=a;
      d.type='text/java'+c;d.async=true;
      a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a)})();
</script>
```

`utag.js`ファイルパスには以下の属性が含まれます：

| 属性  | 説明 | 例 |
| --- |  --- | --- |
| `account` |Tealiumアカウント名 |  `companyXYZ` |
| `profile` |Tealiumプロファイル名 |  `main` |
| `environment` |Tealium環境名 |  `prod` |

例えば、`prod`環境で`sample`プロファイル、`example`アカウントを使用する場合、スクリプトコードの`a=`行の場所を以下のコードに置き換えます：

```html
//tags.tiqcdn.com/utag/example/sample/prod/utag.js
```

`utag.sync.js`についての詳細は、[`utag.sync.js`](https://docs.tealium.com/utag-sync/)をご覧ください。

### コードの取得

アカウント名やプロファイル名がわからない場合は、Tealium管理者に尋ねるか、プラットフォームからコードスニペットを取得できます。アカウントが使用している権限システムによって異なります：

#### プラットフォーム権限

プラットフォーム権限を使用しているアカウントの場合、**タグ管理 > 環境管理**にアクセスしてコードスニペットを取得します：

1. クライアント側の管理メニューで**環境管理**をクリックします。**環境管理**ダイアログが表示されます。
1. 使用しているウェブサイトの環境の編集アイコンをクリックします。
環境編集画面が表示されます。
1. **コードスニペット**セクションで**クリップボードにコピー**をクリックしてコードスニペットを選択します。
1. スクリプトコードの`a=`行の場所を置き換えます。

詳細は、[manage-environments](https://docs.tealium.com/manage-environments/)をご覧ください。

#### レガシー権限

レガシー権限を使用しているアカウントの場合、**タグ管理 > コードセンター**にアクセスしてコードスニペットを取得します：

1. 管理メニューで**コードセンター**をクリックします。**コードセンター**ダイアログが表示されます。
1. サイドパネルで環境を選択します。
1. テキストボックスに表示されたコードを次のいずれかの方法で選択します：
    * クリックしてドラッグしてすべてのコードを選択します。
    * コードの上にマウスを移動すると表示される**すべて選択**ボタンをクリックします。
        ![](https://docs.tealium.com/images/iq-tag-management/iq-code-center-select-all.png)
1. コードをコピーします。
1. サイトのオーサリングツールまたはバックエンドシステムにコードを貼り付けます。

詳細は、[code-center](https://docs.tealium.com/code-center/)をご覧ください。

詳細は、をご覧ください。

### コードの配置

ウェブサイトのすべてのページで、開始タグ `<body>` の直後にユニバーサルタグコードを貼り付けます。この位置は、最も多くのベンダーとの互換性を提供し、訪問が次のページに移動する前にサードパーティのトラッキングが完了することを可能にします。

以下の例は、コードの配置を示しています：

```html
<head>
  <!-- code -->
</head>
<body>
  <TEALIUM CODE SNIPPET GOES HERE>
  <!-- code -->
</body>
```

ユニバーサルタグ `utag.js` の読み込み順序についての詳細は、[操作の順序](https://docs.tealium.com/order-of-operations/)をご覧ください。


## インストールの検証

以下のツールを使用して、`utag.js`のインストールが正しく機能しているかを検証します。

### ユニバーサルタグ (utag) デバッガ

ユニバーサルタグデバッガ（または「utagデバッガ」）は、サイトをナビゲートする際にリアルタイムでデータレイヤーとトラッキングコールを検証する簡単な方法を提供します。Web Companionに似ていますが、`utag.js`内の各トラッキングイベントでキャプチャされたデータに焦点を当てています。

![](https://docs.tealium.com/images/platforms/javascript/utag-monitor.png)

`utag.js`によって行われたトラッキングコールは、ページをナビゲートまたはページ内イベントをトリガーするとツールに表示され、更新されます。

[ユニバーサルタグデバッガのインストールと使用方法](https://docs.tealium.com/universal-tag-debugger/)について詳しく学びましょう。

### Web Companion

Web Companionは、タグ構成を確認し、サイト上のデータを検査し、新しい構成を迅速かつ簡単に作成してテストするためのブラウザツールです。このツールをすぐに起動することで、`utag.js`ライブラリがサイト上で適切に読み込まれていることを確認できます。

![](https://docs.tealium.com/images/platforms/javascript/web-companion.png)

**アカウント情報**  
このタブには、ページが実行されている現在のアカウント、プロファイル、バージョン、環境が表示されます。

**ターゲット環境（デフォルトでは無効）**    
ページコードで検出された環境はオレンジ色でアウトラインが引かれ、現在表示されている環境は青で強調表示されます。環境を変更するには、読み込みたいターゲット環境をクリックし、**ページを更新**をクリックします。

- この機能を有効にするには、公開構成で[Web Companion構成をオンにする](https://docs.tealium.com/publish-configuration/)。
- [公開環境を切り替える他の方法](https://docs.tealium.com/methods-to-switch-publish-environment/)について学びましょう。

**タグ & 拡張タブ**     
このタブでは、どのタグが読み込まれ、リクエストが正常に送信されたかが表示されます。成功裏に完了した拡張も表示されます。

**タイマー**  
各Tealium JavaScriptライブラリの読み込み時間と送信時間がタブの下部に表示されます。

**変更の保存**  
プロファイルに適用された変更はブックマークレットの下部にキューされ、**保存...**ボタンをクリックするまでコミットされません。変更をコミットしたくない場合は、該当する変更の横にある**X**ボタンをクリックしてその変更をキューから削除することもできます。

[Web Companionのインストールと使用方法](https://docs.tealium.com/web-companion/)について詳しく学びましょう。