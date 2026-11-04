---
title: インストール
description: JavaScript（Web）向けTealiumのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/javascript/install/
---
## インストール

### ユニバーサルデータオブジェクト（`utag_data`）

ユニバーサルデータオブジェクト（UDO）は、`utag_data`というJavaScriptオブジェクトです。Webページの動的データは、このオブジェクトを通じてTealiumタグに渡されます。このオブジェクトのプロパティには、ビジネスに固有で、特定のベンダーに依存しない一般的な用語を使用します。

以下は、ユニバーサルタグ`utag.js`を読み込む_前_に行う`utag_data`の宣言例です。

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

詳細：

* [データレイヤーの仕組み](https://docs.tealium.com/how-the-data-layer-works-for-websites/)
* [`utag_data`](https://docs.tealium.com/ja/platforms/javascript/about-utag-data/)

### ユニバーサルタグ（`utag.js`）

ユニバーサルタグは、`utag.js`という小さなJavaScriptコードです。サイトにサードパーティタグを読み込むために必要な、生成済みのコードがすべて含まれています。次のコードをページに挿入することで、タグ管理からタグを実行できるようになります。  

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

`utag.js`のファイルパスには、次の属性が含まれます。

| 属性 | 説明 | 例 |
| --- |  --- | --- |
| `account` | Tealiumアカウント名 | `companyXYZ` |
| `profile` | Tealiumプロファイル名 | `main` |
| `environment` | Tealium環境名 | `prod` |

たとえば、`example`アカウントの`sample`プロファイルにある`prod`環境の場合、スクリプトコードの`a=`行にある場所を次のコードに置き換えます。

```html
//tags.tiqcdn.com/utag/example/sample/prod/utag.js
```

`utag.sync.js`の詳細については、[`utag.sync.js`](https://docs.tealium.com/utag-sync/)を参照してください。

### コードの取得

アカウント名とプロファイル名が不明な場合は、Tealium管理者に問い合わせるか、アカウントで使用している権限システムに応じて、プラットフォームからコードスニペットを取得できます。

#### プラットフォーム権限

プラットフォーム権限を使用するアカウントでは、**タグ管理 > 環境を管理**に移動してコードスニペットを取得します。

1. クライアント側の管理メニューで、**環境を管理**をクリックします。**環境を管理**ダイアログが表示されます。
1. Webサイトで使用している環境の編集アイコンをクリックします。  
**環境を編集**画面が表示されます。
1. **コードスニペット**セクションで、**クリップボードにコピー**をクリックしてコードスニペットを選択します。
1. スクリプトコードの`a=`行にある場所を置き換えます。

詳細については、[manage-environments](https://docs.tealium.com/manage-environments/)を参照してください。

#### レガシー権限

レガシー権限を使用するアカウントでは、**タグ管理 > コードセンター**に移動してコードスニペットを取得します。

1. 管理メニューで、**コードセンター**をクリックします。**コードセンター**ダイアログが表示されます。
1. サイドパネルで環境を選択します。  
1. 次のいずれかの方法で、テキストボックスに表示されているコードを選択します。
    * クリックしてドラッグし、コード全体を選択します。
    * コードにマウスポインターを合わせると表示される**すべて選択**ボタンをクリックします。  
        ![](https://docs.tealium.com/images/iq-tag-management/iq-code-center-select-all.png)
1. コードをコピーします。
1. サイト作成ツールまたはバックエンドシステムにコードを貼り付けます。

詳細については、[code-center](https://docs.tealium.com/code-center/)を参照してください。

詳細については、を参照してください。

### コードの配置

Webサイトのすべてのページで、開始`<body>`タグの直後にユニバーサルタグのコードを貼り付けます。この位置に配置すると、最も多くのベンダーとの互換性が確保され、訪問が次のページに移動する前にサードパーティのトラッキングを完了できます。

次の例は、コードの配置場所を示しています。

```html
<head>
  <!-- code -->
</head>
<body>
  <TEALIUM CODE SNIPPET GOES HERE>
  <!-- code -->
</body>
```

ユニバーサルタグ`utag.js`がどのように読み込まれるかを理解するには、[処理順序](https://docs.tealium.com/order-of-operations/)の詳細を参照してください。


## インストールの検証

`utag.js`が正しくインストールされ、動作していることを検証するには、次のツールを使用します。

### ユニバーサルタグ（utag）デバッガー

ユニバーサルタグデバッガー（「utagデバッガー」）を使用すると、サイト内を移動しながら、データレイヤーとトラッキングコールをリアルタイムで簡単に検証できます。Web Companionと似ていますが、`utag.js`内の各トラッキングイベントで取得されたデータに重点を置いています。

![](https://docs.tealium.com/images/platforms/javascript/utag-monitor.png)

サイト内を移動したり、ページ内イベントをトリガーしたりすると、`utag.js`によるトラッキングコールがツールに表示され、更新されます。  

ユニバーサルタグデバッガーのインストール方法と使用方法については、[詳細を参照してください](https://docs.tealium.com/universal-tag-debugger/)。

### Web Companion

Web Companionは、タグ構成の確認、サイト上のデータの検査、および新しい構成の迅速かつ簡単な作成とテストを可能にするブラウザツールです。このツールを起動することで、`utag.js`ライブラリがサイトで正しく読み込まれていることをすばやく検証できます。

![](https://docs.tealium.com/images/platforms/javascript/web-companion.png)

**アカウント情報**  
ページで現在実行されているアカウント、プロファイル、バージョン、環境がこのタブに表示されます。

**ターゲット環境（デフォルトでは無効）**    
ページコードで検出された環境はオレンジ色の枠で示されます。現在表示している環境は青色で強調表示されます。環境を変更するには、読み込むターゲット環境をクリックしてから、**ページを更新**をクリックします。

- この機能を有効にするには、[パブリッシュ構成でWeb Companionの構成](https://docs.tealium.com/publish-configuration/)をオンにします。
- [環境を切り替える](https://docs.tealium.com/methods-to-switch-publish-environment/)その他の方法について確認してください。

**タグと拡張機能タブ**     
このタブには、読み込まれたタグと、リクエストが正常に送信されたかどうかが表示されます。正常に完了した拡張機能も表示されます。

**タイマー**  
各Tealium JavaScriptライブラリの読み込み時間と送信時間が、タブの下部に表示されます。

**変更の保存**  
Web Companionを通じてプロファイルに適用した変更はブックマークレットの下部にあるキューに追加され、**保存...**ボタンをクリックするまでコミットされません。変更をコミットしない場合は、該当する変更の横にある**X**ボタンをクリックして、その変更をキューから削除することもできます。

Web Companionのインストール方法と使用方法については、[詳細を参照してください](https://docs.tealium.com/web-companion/)。