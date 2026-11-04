---
title: Webサイト向けクイックスタートガイド
url: https://docs.tealium.com/ja/platforms/getting-started-web/quick-start/
---
このガイドでは、Webサイト向けTealiumタグ管理ソリューションのインストール方法について説明します。このインストールには、Universal Tag（`utag.js`）とUniversal Data Object（`utag_data`）の2つのコンポーネントが必要です。サイトのすべてのページに、これら両方のコンポーネントをインストールしてください。

## インストール

### Universal Tag

Universal Tagは、サイトにタグ管理構成を読み込むために必要な生成済みコードを含む、`utag.js`というJavaScriptファイルです。

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

`utag.js`のファイルパスは、アカウントごとに異なります。このガイド全体を通して、プレースホルダー値の`ACCOUNT`、`PROFILE`、`ENVIRONMENT`を、それぞれ実際のアカウント、プロファイル、環境に置き換えてください。

たとえば、アカウント名が`your-company`で、`main`という名前のデフォルトプロファイルを使用している場合、QAインスタンスのファイルパスは次のようになります。

```
//tags.tiqcdn.com/utag/your-company/main/qa/utag.js
```

詳しくは、[Universal Tag（utag.js）のインストール](https://docs.tealium.com/ja/platforms/javascript/install/#universal-tag-utag-js)を参照してください。

### コードの取得

アカウント名とプロファイル名がわからない場合は、Tealium管理者に問い合わせるか、アカウントで使用している権限システムに応じて、プラットフォームからコードスニペットを取得できます。

#### プラットフォーム権限

プラットフォーム権限を使用しているアカウントでは、**Tag Management > Manage Environments**に移動してコードスニペットを取得します。

1. クライアント側の管理メニューで、**Manage Environments**をクリックします。**Manage Environments**ダイアログが表示されます。
1. Webサイトで使用している環境の編集アイコンをクリックします。**Edit environment**画面が表示されます。
1. **Code Snippet**セクションで、**Copy to Clipboard**をクリックしてコードスニペットを選択します。
1. スクリプトコードの`a=`行にある場所を置き換えます。

詳しくは、[manage-environments](https://docs.tealium.com/manage-environments/)を参照してください。

#### 従来の権限

従来の権限を使用しているアカウントでは、**Tag Management > Code Center**に移動してコードスニペットを取得します。

1. 管理メニューで、**Code Center**をクリックします。  
**Code Center**ダイアログが表示されます。
1. サイドパネルで環境を選択します。  
1. 次のいずれかの方法で、テキストボックスに表示されているコードを選択します。
    * クリックしてドラッグし、すべてのコードを選択します。
    * コードにマウスポインターを合わせると表示される**Select All**ボタンをクリックします。  
        ![](https://docs.tealium.com/images/iq-tag-management/iq-code-center-select-all.png)
1. コードをコピーします。
1. サイト作成ツールまたはバックエンドシステムにコードを貼り付けます。

詳しくは、[code-center](https://docs.tealium.com/code-center/)を参照してください。

### 環境

適切なリリースサイクルをサポートするために、Dev、QA、Prodの3つの環境があります。これにより、非本番環境には`utag.js`のQAインスタンスを、本番稼働中のサイトにはProdインスタンスをインストールできます。この構成を使用すると、変更をProdにリリースする前にQAでテストできます。

環境パスによって、読み込むUniversal Tagのインスタンスが決まります。

* **QA**  
`//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/qa/utag.js`
* **Prod**  
`//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/prod/utag.js`

詳しくは、[manage-environments](https://docs.tealium.com/manage-environments/)を参照してください。

### コードの配置

サイトのすべてのページで、開始`<body>`タグの直後にUniversal Tagコードを貼り付けます。この位置に配置すると、最も多くのベンダーとの互換性が確保され、訪問が次のページに移動する前にサードパーティによるトラッキングを完了できます。

次の例は、コードの配置を示しています。

```html
<head>
  ...
</head>
<body>
<!-- Tealium Universal Tag -->
<script type="text/javascript">
  (function(a,b,c,d) {
      a='//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js';
      b=document;c='script';d=b.createElement(c);d.src=a;
      d.type='text/java'+c;d.async=true;
      a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a)})();
</script>
  ...
</body>
```

Universal Tagの読み込み方法を理解するには、[処理順序](https://docs.tealium.com/order-of-operations/)について詳しく確認してください。

## データレイヤー

データレイヤーは、サイト全体で収集されるすべての変数と、トラッキングされる訪問のインタラクションで構成される、Tealiumソリューションの基盤です。

Universal Data Object（UDO）は`utag_data`というJavaScriptオブジェクトで、サイトからの動的データをTealiumタグに渡すために使用されます。このオブジェクトのプロパティには、ビジネスに固有で、ベンダーに依存しない一般的な用語を使用して名前を付けます。  


<blockquote>
サイトのすべてのページでデータレイヤーオブジェクトを読み込み、各ページタイプに必要な変数に基づいて動的にデータを構成し、Universal Tagより前に読み込む必要があります。
</blockquote>


次に、検索結果ページに記述される可能性がある`utag_data`の宣言例を示します。  

```html
<script type="text/javascript">
  var utag_data={
      "tealium_event"  : "search",
      "page_name"      : "Search Results",
      "search_results" : "42",
      "search_keyword" : "Tealium shirt"
  };
</script>
```

詳細情報：

* [データレイヤーの概要](https://docs.tealium.com/an-introduction-to-the-data-layer/)
* [組み込みのデータレイヤー変数](https://docs.tealium.com/ja/platforms/javascript/data-layer/)
* [Tag Managementでのデータレイヤー変数の使用](https://docs.tealium.com/data-layer-variables/)
* [Universal Data Objectについて](https://docs.tealium.com/ja/platforms/javascript/about-utag-data/)

## トラッキング

### イベント

ページビュー以外のイベント、ページ内のインタラクション、その他の動的なページイベントをトラッキングするには、`utag.link()`関数を使用します。イベントトラッキングでは、ページ内での訪問のインタラクションに関する情報を収集します。

Tealiumでは、トラッキング対象イベントに名前を付けるためのデータレイヤー変数[`tealium_event`](#tealium-event-variable)を提供しています。この変数はJavaScriptイベントリスナー内で使用し、ユーザーによるボタンのクリックなど、Webサイト要素に対するインタラクションが発生したときにイベントをトラッキングします。

次の例では、ユーザーがソーシャル共有ボタンをクリックしたときにトラッキングします。

```html
<a href="#" name="share" onclick="utag.link({'tealium_event': 'social_share', 'social_network': 'LinkedIn'});">Share</a>
```

詳しくは、[イベントのトラッキング](https://docs.tealium.com/ja/platforms/javascript/track/#track-events)を参照してください。

### ビュー

`utag.view()`関数は、ページが読み込まれるたびに自動的にトリガーされます。この関数は、ページビュー、仮想ページビュー、Ajaxページフロー、シングルページアプリケーションをトラッキングします。この関数を呼び出すと、構成済みのベンダータグ内で、対応するページトラッキング機能がトリガーされます。

次に、訪問が「jeans」を検索したコンテンツサイトの例を示します。  

```javascript
utag.view({
    "tealium_event": "search",
    "search_keyword": "jeans",
    "search_results": "42"
});
```

次に、チェックアウトフローの1ステップをトラッキングするEコマースサイトの例を示します。  

```javascript
utag.view({
    "tealium_event": "page_view",
    "page_type": "checkout",
    "page_name": "Checkout: Payment Method",
    "cart_total_items": "2",
    "cart_total_value": "125.00"
});
```

詳細情報：

- [ビューのトラッキング](https://docs.tealium.com/ja/platforms/javascript/track/#track-views)
- [シングルページアプリケーション](https://docs.tealium.com/ja/platforms/javascript/single-page-applications/)
### Tealiumイベント変数

追跡する各インタラクションの種類を一意に識別するには、予約変数`tealium_event`を使用します。この変数は、ロードルール、拡張機能、データマッピングを構成するために、タグ管理全体で参照されます。その他すべてのイベントデータには、任意の変数名を使用してください。

推奨される`tealium_event`の値には、以下が含まれますが、これらに限定されません。

| `tealium_event`の値 | イベントの説明 |
| --- | --- |
| `page_view` | ページを表示 |
| `search` | 商品を検索 |
| `product_view` | 商品を表示 |
| `cart_add` | 商品をショッピングカートに追加 |
| `purchase` | 購入を完了 |
| `user_login` | ユーザーがログイン |
| `social_share` | ソーシャルサイトでリンクを共有 |

詳細：

* [`tealium_event`変数について](https://docs.tealium.com/ja/platforms/javascript/track/#tealium-event)
* [データレイヤー定義：小売](https://docs.tealium.com/retail/)
* [データレイヤー定義：パブリッシャー](https://docs.tealium.com/publisher/)
* [データレイヤー定義：動画トラッキング](https://docs.tealium.com/basic-video-tracking/)


### ベストプラクティス

データレイヤーの実装と管理に関するベストプラクティスは次のとおりです。

**変数の命名規則**

- 小文字、単数形、アンダースコア区切りの変数名を使用します。
- ベンダー固有の命名を避け、意味が明確な変数名を使用します。
- ブール変数名には`is_`または`has_`のプレフィックスを付けます。

**データ値**

- すべての変数に文字列値を使用します。
- ブール値には、`true`と`false`の代わりに文字列値`"1"`と`"0"`を使用します。
- 数値には、`1234.56`の代わりに`"1234.56"`のような文字列値を使用します。
- 配列には、`["prodID1", "prodID2", "prodID3"]`のようなカンマ区切りの文字列を使用します。

**ページタイプ識別子**  

サイトのすべてのページに、`page_type`という変数を含める必要があります。この変数は、ユーザーが表示しているページの種類を判別するために使用され、ロードルール、拡張機能、データマッピングの構成に役立ちます。

**サードパーティのデータレイヤーオブジェクト**

W3C Data Objectや独自のカスタムオブジェクトなど、データレイヤーオブジェクトがすでにサイトに実装されている場合があります。利用可能な[データレイヤーコンバーター](https://docs.tealium.com/set-up-data-layer-converter/)のいずれかを使用して、これらのオブジェクトをUniversal Data Object（UDO）`utag_data`に変換します。

**`utag.js`より前に`utag_data`を構成する**  
ページコードでは、Universal Data ObjectをUniversal Tagより前に宣言する必要があります。これにより、Universal Tagでロードルール、拡張機能、タグの評価に必要なすべてのデータレイヤー変数を確実に利用できます。

詳細については、[データレイヤーのベストプラクティス](https://docs.tealium.com/data-layer-best-practices/)を参照してください。

## テストと検証

以下のツールを使用して、インストールが正常に動作していることを検証します。

### Universal Tag Debugger

Universal Tag Debugger（「utag debugger」とも呼ばれます）を使用すると、サイト内を移動しながら、データレイヤーとトラッキング呼び出しをリアルタイムで簡単に検証できます。

![](https://docs.tealium.com/images/platforms/javascript/utag-monitor.png)

サイト内を移動したり、ページ内イベントをトリガーしたりすると、`utag.js`によるトラッキング呼び出しがツールに表示され、更新されます。  

詳細については、[Universal Tag Debugger](https://docs.tealium.com/universal-tag-debugger/)を参照してください。

### Web Companion

Web Companionは、タグ構成の確認、サイト上のデータの検査、新しい構成の迅速かつ簡単な作成とテストを行えるブラウザーツールです。このツールを起動すると、`utag.js`ライブラリがサイトに正常に読み込まれていることをすばやく検証できます。

![](https://docs.tealium.com/images/platforms/javascript/web-companion.png)

詳細：

- [Web Companion](https://docs.tealium.com/web-companion/)
- [パブリッシュ構成内のWeb Companion構成](https://docs.tealium.com/publish-configuration/)
- [環境の切り替え](https://docs.tealium.com/methods-to-switch-publish-environment/)

### Live Events

Event Streamingでは、Live Events機能を使用して、受信イベントをリアルタイムで管理および検査します。データソースから送信したイベントが受信されていることを確認します。


<blockquote>
Live Eventsを使用するには、タグ管理構成にTealium Collectタグを追加する必要があります。
</blockquote>


詳細：

* [Live Eventsとフィード](https://docs.tealium.com/about-live-events/)
* [タグ管理のデータソース](https://docs.tealium.com/data-sources-for-iq-tag-management/)
* [Tealium Collectタグ構成ガイド](https://docs.tealium.com/tealium-collect-tag/)