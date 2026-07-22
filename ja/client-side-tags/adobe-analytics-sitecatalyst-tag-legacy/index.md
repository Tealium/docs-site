---
title: Adobe Analytics（SiteCatalyst）タグ構成ガイド（レガシー）
description: この記事では、iQタグ管理アカウントでAdobe Analytics（レガシー）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-analytics-sitecatalyst-tag-legacy/
---

<blockquote>
これは新しい（推奨）バージョンのレガシーAdobeタグであり、タグマーケットプレイスから[Adobe AppMeasurement for JavaScriptタグ](https://docs.tealium.com/adobe-appmeasurement-for-js-tag/)が利用可能です。
</blockquote>


## 動作原理

Adobe Analytics（SiteCatalyst）は、AdobeのWebアナリティクスを提供するソフトウェア・アズ・ア・サービス（SaaS）アプリケーションです。

## 開始する前に

開始する前に、以下の項目を考慮してください：

* Adobe Experience Cloud IDサービスを使用する場合は、このタグを追加する**前に**Adobe Experience Cloud IDサービスタグを追加してください。
* S-Codeバージョンを変更する際は、正しいテンプレートを取り込むために既存のテンプレートを削除してください。
* 変数値に基づいてレポートスイートを構成するために`s_account`にマッピングしてください。これにより、デフォルト構成と動的アカウントリスト構成が上書きされます。
* `s_account`にマッピングする場合は、動的アカウント構成を**はい**に変更してください。
* **AAM**オプションを含むS-Codeバージョンを選択してください。これにはパートナー値が必要です。
* サードパーティトラッキングの場合、デフォルトのサーバー位置は**122**(`122.2o7.net`)です。
  * `112.2o7.net`データ収集サーバーの場合、**サーバー**と**サーバーセキュア**を直接構成してください。
  * 例：`mysite.112.2o7.net`

### 前提条件

* **`s_code.js`のローカルコピー**
  * このタグを構成するには、Adobeアカウントから生成された`s_code.js` JavaScriptファイルが必要です。
  * そのコードのセクションはTiQ構成にコピーされます。  

<blockquote>
JavaScriptライブラリファイルの名前は異なる場合があります。
</blockquote>

  * [s_code.jsについてもっと学ぶ](https://marketing.adobe.com/resources/help/en_US/sc/implement/impl_js_file.html).

* **ソリューションデザインリファレンス**
  * （オプション）このドキュメントは、Adobe Analyticsソリューションで追跡されるすべてのprops、eVars、およびイベントを定義します。
  * この情報は、TiQでAdobeタグを正確に構成するために必要です。

### サポートされるバージョン

* バージョンH.20 - H.27（Adobe Audience Managerを含むH.25 - H.27）

## タグ構成

まず、TealiumのタグマーケットプレイスにアクセスしてAdobe Analytics（レガシー）タグを追加します（[タグの追加方法について学ぶ](https://docs.tealium.com/manage-tags/)）。

タグを追加した後、次の構成を構成します：

* **S-Codeバージョン**
  * `s_code.js`ライブラリのバージョン。
  * バージョン25から27はAdobe Audience Managerをサポートしています。

* **レポートスイート**
  * 使用するデフォルトのレポートスイート。
  * 動的アカウントリストで構成された値に基づいて変更される場合があります。
  * 参照`s_code.js`: `s.account`

* **サーバー**
  * データ収集サーバー。
  * 参照`s_code.js`: `s.trackingServer`

* **サーバーセキュア**
  * "https"データ収集サーバー。
  * 参照`s_code.js`: `s.trackingServerSecure`

* **ネームスペース**
  * サーバーとサーバーセキュアが`2o7.net`で終わる場合にのみ、サードパーティクッキーに適用されます。
  * 参照`s_code.js`: `s.namespace`

* **エンタープライズクラウドID**
  * バージョンH.27以降でVisitor APIを使用する場合、ここにエンタープライズクラウドIDを入力します。
  * [Adobe Enterprise Cloud IDサービスについてもっと学ぶ](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-requirements.html).

* **自動リンクトラッキング**
  * 推奨値はデフォルト値の**はい**です。
  * **いいえ**に構成する場合は、[リンクトラッキングエクステンション](https://docs.tealium.com/link-tracking-extension/)などの他の方法を使用してすべての自動リンクトラッキングを複製する必要があります。

* **ダウンロードタイプ**
  * ダウンロードリンクとして追跡したいファイル拡張子のタイプをリストします。
  * 参照`s_code.js`: `s.linkDownloadFileTypes`

* **内部リンクフィルター**
  * リンククリックがAdobeレポートで退出クリックとして報告されないようにするために使用されます。
  * 参照`s_code.js:` `s.linkInternalFilters`

* **通貨コード**
  * 3文字の通貨コード、例えば`USD`はアメリカドルです。
  * 参照`s_code.js`: `s.currencyCode`

* **動的アカウント使用**
  * ドメインまたは他の動的値に基づいて異なるレポートスイートにデータを送信するために`はい`に構成します。

* **動的アカウントリスト**
  * ドメインまたは他の動的値に基づいてレポートスイートを動的に構成するために使用されます。
  * 例：`testreportsuite=testing.example.com,qa.example.com;prodreportsuite=www.example.com`
  * [SiteCatalystで動的アカウントリストを使用する方法について学ぶ](http://omniture.custhelp.com/app/answers/detail/a_id/1440).

* **S-Object名**
  * デフォルト名は`s`です。
  * ページ上で複数のレガシーAdobe AnalyticsタグまたはAdobe AppMeasurementタグを実行している場合は、異なる名前を構成します。

* **クリア変数**
  * 各トラッキングコール後にprops、eVars、およびイベントをクリアします。
  * デフォルト値は`いいえ`です。

* **パートナー**
  * Adobe Audience Managerを使用する場合は、パートナーIDを入力します。それ以外の場合は空白のままにしてください。
  * 参照`s_code.js:` `DIL.create()`

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

Adobe Analyticsの推奨ロードルール：**すべてのページ**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法の説明については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

データレイヤー変数（eVars、propsなど）はマッピングツールボックスを使用してマッピングできます。

1. データマッピングタブをクリックし、**+ 宛先を選択**をクリックします。  
マッピングツールボックスが表示されます。  
![](https://docs.tealium.com/images/client-side-tags/data-mappings-select-destination.jpg)
1. **+ カスタム宛先を追加**をクリックして別のpropまたはeVarをテキストボックスに入力することで、追加のマッピングをすばやく追加できます。  

<blockquote>
同じ変数の複数のpropsとeVarsはカンマ(`,`)で区切る必要があります。Adobeの構文に合わせてeVarに大文字の`V`を使用してください。
</blockquote>


### 利用可能なデータレイヤー変数

#### 標準

| 変数                | 説明           |
|:------------------------|:----------------------|
| `pageName`              | ページ名             |
| `channel`               | チャンネル               |
| `server`                | サーバー                |
| `hier1` から `hier3` | 階層                 |
| `visitorID`             | 訪問ID            |
| `s_account`             | レポートスイートの上書き |

#### イベント

| 変数                     | 説明 |
|:-----------------------------|:------------|
| `prodView`                   | prodView    |
| `scOpen`                     | scOpen      |
| `scAdd`                      | scAdd       |
| `scRemove`                   | scRemove    |
| `scView`                     | scView      |
| `scCheckout`                 | scCheckout  |
| `purchase`                   | purchase    |
| `event1` から `event1000` | イベント      |

#### 製品レベルのイベント

| 変数                                      | 説明     |
|:----------------------------------------------|:----------------|
| `PRODUCTS_event1` から `PRODUCTS_event100` | 製品イベント |

#### Props

`prop1` から `prop75`

#### eVars

| 変数                 | 説明  |
|:-------------------------|:-------------|
| `campaign`               | (eVar0)      |
| `eVar1` から `eVar75` | evars        |
| `contextData.myvar`      | コンテキストデータ |

#### マーチャンダイジングeVars

| 変数                          | 説明    |
|:----------------------------------|:---------------|
| `PRODUCTS_eVar1` から `eVar75` | 製品eVars |
#### コマース

| 変数                   | 説明                                              |
|:-----------------------|:--------------------------------------------------|
| `purchaseID`           | <ul><li>購入ID</li></ul>                          |
| `transactionID`        | <ul><li>トランザクションID</li></ul>               |
| `state`                | <ul><li>州</li></ul>                              |
| `zip`                  | <ul><li>郵便番号</li></ul>                        |
| `PRODUCTS_id`          | <ul><li>製品ID</li><li>配列</li></ul>             |
| `PRODUCTS_category`    | <ul><li>製品カテゴリ</li><li>配列</li></ul>       |
| `PRODUCTS_quantity`    | <ul><li>製品数量</li><li>配列</li></ul>           |
| `PRODUCTS_price`       | <ul><li>製品価格</li><li>配列</li></ul>           |

#### その他

| 変数                                 | 説明         |
|:-------------------------------------|:-------------|
| リンク追跡 - `doneAction` パラメータ | (H25のみ)    |
| `List 1` から `List 3`                | リスト       |

## E-コマース マッピング

Adobe製品の文字列を適切にフォーマットし、収益データをレポートスイートに送信するには、[E-コマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を追加して構成する必要があります。拡張機能で構成された変数は、タグ統合によって自動的に期待される構文にフォーマットされます。

たとえば、製品カテゴリ、製品ID、製品数量、製品価格の変数は、次の例のように製品文字列に変換されます。ここでは複数の製品が扱われています：

`s.products= product_category;product_id;product_quantity;product_price;;`

### マッピングイベント

マッピングツールボックスのイベントセクションを使用して、特定の変数の値に応じてイベントがトリガーされるタイミングを定義します。

変数を選択して左サイドバーの **イベント** をクリックすると、**値** と **トリガー** の2つのフィールドが表示されます。

* **値** ボックスでは、変数の値を定義します。
* **トリガー** ボックスでは、追跡するAdobeイベントを選択します。

この例では、変数 `page_type` が `product` および `cart` に等しい場合に、Adobeイベント `prodView` および `scView` をトリガーするように構成します：

![](https://docs.tealium.com/images/client-side-tags/data-mapping-events-value-and-trigger.jpg)

### マーチャンダイジング eVars

Adobeの実装では、`s.products` 文字列にeVar値を添付することで、製品にeVarを関連付けることができます。たとえば、製品文字列の各製品に関連付けたい配列変数 `product_discount` がある場合、マーチャンダイジングeVarマッピングは次のように `s.products` 文字列を作成します。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.product_discount = ["**12.34**", "**1.23**"];
```

次に、`product_discount` をマーチャンダイジング `eVar4` にマッピングすると、次のような `s.products` 文字列が得られます：

`s.products=";prodA;1;25.12;;**evar4=12.34**,;prodB;1;10.99;;**evar4=1.23**"`

配列でない変数（単一の値）をマーチャンダイジング `eVar` にマッピングする場合、その単一の値が各製品に適用されます。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.product_discount = "**1.99**";
```

上記と同じマッピングで、得られる `s.products` 文字列は次のようになります：

`s.products=";prodA;1;25.12;;**evar4=1.99**,;prodB;1;10.99;;**evar4=1.99**"`

### 製品レベルのイベント

製品レベルのイベントは、マーチャンダイジング `eVars` と同様に機能します。単一の値を使用して製品文字列のすべての製品に同じ変数を適用するか、値の配列を使用して製品文字列の各製品に異なる値を適用することができます。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.order_discount   = "**12.00**";
```

次に、`order_discount` を `product event15` にマッピングすると、次のような `s.products` 文字列が得られます。

`s.products=";prodA;1;25.12;**event15=12.00**;,;prodB;1;10.99;**event15=12.00**;"`

両方の製品に同じ注文割引が適用されていることに注意してください。


<blockquote>
マーチャンダイジング `eVars` および製品レベルのイベントの配列マッピングは、バージョンH.26以降で利用可能です。
</blockquote>


## doPluginsのための必要な拡張機能

`s_code.js` ファイルの次の2つのセクションのコードを、TiQ構成の拡張機能にコピーする必要があります：

* Do Plugins セクション
* プラグインとモジュール

### Do Plugins

**Do Plugins** セクションは常に **プラグインとモジュール** セクションの上にあります。このセクションは通常、次の行で始まります：

```
/* プラグイン構成 */
s.usePlugins=true;
```

これらの行から次の行までのすべてをコピーします：

```
s.doPlugins=s_doPlugins;
```

このコードブロックを [JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/) に貼り付け、Adobe Analyticsタグに適用し、拡張機能の名前を `Do Plugins Section` とします：

![](https://docs.tealium.com/images/client-side-tags/do-plugins-extension.jpg)

### プラグインとモジュール

`s_code` のプラグインとモジュールセクションは次の行で始まります：

```
/***********************PLUGINS SECTION ********************/
```

そして、この行の直前で終わります：

```
/************* この行以下は何も変更しないでください ! **************/
```

このコードセクション全体をコピーして、Adobe Analyticsタグに適用される別のJavaScript Code拡張機能に貼り付けます。この拡張機能の名前を `Plugins and Modules` とします：

![](https://docs.tealium.com/images/client-side-tags/plugins-and-modules.jpg)

次に、**プラグインとモジュール** JavaScript拡張機能を **Do Plugins** セクション JavaScript拡張機能の直上にドラッグします。

次の行で始まるコードセクション

```
/************* この行以下は何も変更しないでください ! **************/
```

は、TiQ内のタグテンプレートを通じてロードされるAdobe `s_code` ライブラリのコア部分です。

## 新しいバージョンへのアップグレード

Adobeタグの新しいベースコードにアップグレードするには、次の手順を使用します：

1. タグを開いて **編集** をクリックします。
1. **S-Codeバージョン** フィールドで、ドロップダウンリストから希望するバージョンを選択します。たとえば **H.27**。
![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-legacey-tag-select-upgrade-version.jpg)
タグテンプレートが更新される必要があることを示す警告モーダルが表示されます。
1. **OK** をクリックします。
![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-legacy-upgrade-message.jpg)
1. **詳細構成** までスクロールダウンし、クリックして展開します。
1. **テンプレートの編集** を選択します。
1. テキストフィールドに、バックアップとしてテキストファイルにテンプレート全体をコピーして貼り付けます。
1. 現在のテンプレートを選択してゴミ箱アイコンをクリックして削除します。
1. 変更を保存して公開します。
最新のタグバージョンがロードされます。

## 高度な構成

### s.eventsの構成

Adobeタグテンプレート内で、Tealiumは `s.event` 文字列を構成するのに役立つ `u.addEvent()` という関数を提供しています。この方法は、`s.events` の最後に新しい値を追加することで、すでに構成されているすべてのイベントを保持し、必要に応じて別のイベントを追加することができます。この方法を使用するには、構成に `sc_events` という変数が必要です。

`s.events` をカスタマイズするための次の手順を使用します：

1. [Set Data Values](https://docs.tealium.com/set-data-values-extension/) 拡張機能を追加します。
1. **Scope** を Adobe Analyticsタグに構成します。
1. **Set** メニューから **sc_events** を選択します。
1. **To** メニューから **JS Code** を選択します。
1. テキストフィールドに次のように入力します：`u.addEvent("CUSTOM_EVENT")`  
ここで、`CUSTOM_EVENT` は `s.events` 文字列に追加したいイベントです。たとえば **event10** です。
1. 一度に複数のイベントを追加するには、次のように `u.addEvent` に配列を渡します：  
`u.addEvent(["event1","event2","scView"]);`
### SiteCatalyst ダイナミック変数

Adobeは、複数のプロパティに現れる値を再利用することで、トラッキングピクセルのサイズを最小限に抑えるためのダイナミック変数と呼ばれる表記法をサポートしています。

TiQのAdobeタグは、ピクセルリクエストをAdobeに送信する際にこの表記法を自動的に適用します。これは、あなたの変数の中で `v3:D=c2` のような値を見るかもしれないことを意味します。この場合、`v3` は `eVar3` であり、`D=c2` は `s.prop2` からの値です。`s.prop2` の値を繰り返す代わりに、この短縮表記が `prop2` への参照として使用され、Adobeのサーバーで適切に解釈されます。結果として得られるトラッキングピクセルはより小さく、速くなり、一つのピクセルリクエストに最大量のデータを詰め込むことができます。

![](https://docs.tealium.com/images/client-side-tags/sitecatalyst-dynamic-variables.jpg)

[SiteCatalyst ダイナミック変数](http://omniture.custhelp.com/app/answers/detail/a_id/10099)についてもっと学びましょう。