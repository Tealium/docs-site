---
title: Adobe Analytics（SiteCatalyst）タグ構成ガイド（レガシー）
description: この記事では、タグ管理アカウントで Adobe Analytics（レガシー）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-analytics-sitecatalyst-tag-legacy/
---

<blockquote>
これは旧バージョンの Adobe タグです。新しい（推奨）バージョンである [Adobe AppMeasurement for JavaScript タグ](https://docs.tealium.com/adobe-appmeasurement-for-js-tag/)は、タグマーケットプレイスから利用できます。
</blockquote>


## 仕組み

Adobe Analytics（SiteCatalyst）は、Web 分析機能を提供する Adobe の Software as a Service（SaaS）アプリケーションです。

## はじめる前に

開始する前に、以下の項目を確認してください。

* Adobe Experience Cloud ID Service を使用する場合は、このタグを追加する**前に** Adobe Experience Cloud ID Service タグを追加してください。
* S-Code のバージョンを変更するときは、既存のテンプレートを削除して、正しいテンプレートを取得してください。
* 変数値に基づいてレポートスイートを構成するには、`s_account` にマッピングします。これにより、デフォルト構成と動的アカウントリスト構成が上書きされます。
* `s_account` にマッピングする場合は、Use Dynamic Account 構成を **Yes** に変更してください。
* Adobe Audience Manager を含めるには、**AAM** オプションが付いた S-Code バージョンを選択してください。これにはパートナー値が必要です。
* サードパーティートラッキングの場合、デフォルトのサーバーロケーションは **122**（`122.2o7.net`）です。
  * `112.2o7.net` データ収集サーバーの場合は、**Server** と **Server Secure** を直接構成してください。
  * 例：`mysite.112.2o7.net`

### 前提条件

* **`s_code.js` のローカルコピー**
  * このタグを構成するには、Adobe アカウントから生成された `s_code.js` JavaScript ファイルが必要です。
  * そのコードの各セクションを TiQ 構成にコピーします。  

<blockquote>
JavaScript ライブラリファイルの名前は異なる場合があります。
</blockquote>

  * [s_code.js の詳細](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/h-code/overview)。

* **ソリューション設計リファレンス**
  * （任意）このドキュメントでは、Adobe Analytics ソリューションで追跡されるすべての prop、eVar、イベントを定義します。
  * TiQ で Adobe タグを正確に構成するには、この情報が必要です。

### サポート対象バージョン

* バージョン H.20～H.27（Adobe Audience Manager 対応は H.25～H.27）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、以下の構成を行います。

* **S-Code Version**
  * ` s_code.js` ライブラリのバージョン。
  * バージョン 25～27 は Adobe Audience Manager をサポートしています。

* **Report Suite**
  * 使用するデフォルトのレポートスイート。
  * Dynamic Acct List に構成された値に基づいて変更される場合があります。
  * `s_code.js` の参照箇所：`s.account`

* **Server**
  * データ収集サーバー。
  * `s_code.js` の参照箇所：`s.trackingServer`

* **Server Secure**
  * 「https」データ収集サーバー。
  * `s_code.js` の参照箇所：`s.trackingServerSecure`

* **Namespace**
  * Server と Server Secure が `2o7.net` で終わる場合に、サードパーティー Cookie にのみ適用されます。
  * `s_code.js` の参照箇所：`s.namespace`

* **Enterprise Cloud ID**
  * バージョン H.27 以降で Visitor API を使用する場合は、ここに Enterprise Cloud ID を入力します。
  * [Adobe Enterprise Cloud ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/intro/overview) の詳細を参照してください。

* **Auto Link Tracking**
  * 推奨値はデフォルト値の **Yes** です。
  * **No** に構成した場合は、[Link Tracking Extension](https://docs.tealium.com/link-tracking-extension/)などの別の方法を使用して、自動リンクトラッキングをすべて再現する必要があります。

* **Download Types**
  * ダウンロードリンクとして追跡するファイル拡張子の種類を一覧で指定します。
  * `s_code.js` の参照箇所：`s.linkDownloadFileTypes`

* **Internal Link Filters**
  * リンクのクリックが離脱クリックとして Adobe レポートに記録されないようにするために使用します。
  * `s_code.js:` の参照箇所：`s.linkInternalFilters`

* **Currency Code**
  * 米ドルを表す `USD` など、3 文字の通貨コード。
  * `s_code.js` の参照箇所：`s.currencyCode`

* **Use Dynamic Acct**
  * ドメインやその他の動的な値に基づいて異なるレポートスイートへデータを送信できるようにするには、`Yes` に構成します。

* **Dynamic Acct List**
  * ドメインやその他の動的な値に基づいて、レポートスイートを動的に構成するために使用します。
  * 例：`testreportsuite=testing.example.com,qa.example.com;prodreportsuite=www.example.com`
  * [SiteCatalyst での動的アカウントリストの使用方法](http://omniture.custhelp.com/app/answers/detail/a_id/1440)の詳細を参照してください。

* **S-Object Name**
  * デフォルト名は `s` です。
  * レガシー Adobe Analytics タグまたは Adobe AppMeasurement タグの複数のインスタンスをページ上で実行する場合は、別の名前を構成してください。

* **Clear Vars**
  * 各トラッキング呼び出しの後に、prop、eVar、イベントをクリアします。
  * デフォルト値は `No` です。

* **Partner**
  * Adobe Audience Manager で使用するパートナー ID を入力します。使用しない場合は空白のままにしてください。
  * `s_code.js:` の参照箇所：`DIL.create()`

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、サイト上のどの場所で、いつこのタグのインスタンスを読み込むかを決定します。

Adobe Analytics の推奨読み込みルール：**すべてのページ**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

データレイヤー変数（eVar、prop など）は、マッピングツールボックスを使用してマッピングできます。

1. Data Mappings タブをクリックし、**+ Select Destination** をクリックします。  
マッピングツールボックスが表示されます。  
![](https://docs.tealium.com/images/client-side-tags/data-mappings-select-destination.jpg)
1. **+ Add Custom Destination** をクリックし、テキストボックスに別の prop または eVar を入力すると、追加のマッピングをすばやく追加できます。  

<blockquote>
同じ変数に対する複数の prop と eVar は、カンマ（`,`）で区切ってください。Adobe で想定される構文と一致するように、eVar では大文字の `V` を使用してください。
</blockquote>


### 利用可能なデータレイヤー変数

#### 標準

| 変数                    | 説明                       |
|:------------------------|:---------------------------|
| `pageName`              | ページ名                   |
| `channel`               | チャネル                   |
| `server`                | サーバー                   |
| `hier1` through `hier3` | 階層                       |
| `visitorID`             | 訪問 ID                  |
| `s_account`             | レポートスイートの上書き   |

#### イベント

| 変数                         | 説明       |
|:-----------------------------|:-----------|
| `prodView`                   | prodView   |
| `scOpen`                     | scOpen     |
| `scAdd`                      | scAdd      |
| `scRemove`                   | scRemove   |
| `scView`                     | scView     |
| `scCheckout`                 | scCheckout |
| `purchase`                   | purchase   |
| `event1` through `event1000` | イベント   |

#### 製品レベルのイベント

| 変数                                          | 説明               |
|:----------------------------------------------|:-------------------|
| `PRODUCTS_event1` through `PRODUCTS_event100` | 製品イベント       |

#### Prop

`prop1` through `prop75`

#### eVar

| 変数                     | 説明               |
|:-------------------------|:-------------------|
| `campaign`               | (eVar0)            |
| `eVar1` through `eVar75` | eVar               |
| `contextData.myvar`      | コンテキストデータ |

#### マーチャンダイジング eVar

| 変数                              | 説明         |
|:----------------------------------|:-------------|
| `PRODUCTS_eVar1` through `eVar75` | 製品 eVar    |
#### コマース

| 変数           | 説明                                        |
|:-------------------|:---------------------------------------------------|
| `purchaseID`         | <ul><li>購入 ID</li></ul>                      |
| `transactionID`      | <ul><li>トランザクション ID</li></ul>                   |
| `state`              | <ul><li>州</li></ul>                            |
| `zip`                | <ul><li>郵便番号</li></ul>                      |
| `PRODUCTS_id`       | <ul><li>製品 ID</li><li>配列</li></ul>        |
| `PRODUCTS_category` | <ul><li>製品カテゴリー</li><li>配列</li></ul> |
| `PRODUCTS_quantity` | <ul><li>製品数量</li><li>配列</li></ul>   |
| `PRODUCTS_price`    | <ul><li>製品価格</li><li>配列</li></ul>     |

#### その他

| 変数                         | 説明 |
|:---------------------------------|:------------|
| リンクトラッキング - `doneAction` パラメーター | （H25 のみ）  |
| `List 1`～`List 3`            | リスト       |

## E コマースのマッピング

Adobe の製品文字列を正しくフォーマットし、収益データをレポートスイートに送信するには、[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を追加して構成する必要があります。拡張機能で構成された変数は、タグ統合によって想定される構文に自動的にフォーマットされます。

たとえば、製品カテゴリー、製品 ID、製品数量、および製品価格の変数は、複数の製品を処理する次の例のように製品文字列へ変換されます。

`s.products= product_category;product_id;product_quantity;product_price;;`

### イベントのマッピング

マッピングツールボックスの「Events」セクションを使用して、特定の変数の値に応じてイベントをトリガーするタイミングを定義します。

変数を選択して左側のサイドバーで **Events** をクリックすると、**Value** と **Trigger** の 2 つのフィールドが表示されます。

* **Value** ボックスでは、変数の値を定義します。
* **Trigger** ボックスでは、追跡する Adobe イベントを選択します。

この例では、変数 `page_type` がそれぞれ `product` および `cart` と等しい場合に、Adobe イベント `prodView` および `scView` がトリガーされるように構成します。

![](https://docs.tealium.com/images/client-side-tags/data-mapping-events-value-and-trigger.jpg)

### マーチャンダイジング eVar

Adobe の実装では、eVar 値を `s.products` 文字列にエンリッチメントすることで、eVar を製品に関連付けることができます。たとえば、製品文字列内の各製品に関連付けたい `product_discount` という名前の配列変数がある場合、マーチャンダイジング eVar のマッピングによって、それに応じた `s.products` 文字列が作成されます。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.product_discount = ["**12.34**", "**1.23**"];
```

次に、`product_discount` をマーチャンダイジング `eVar4` にマッピングすると、次の `s.products` 文字列が生成されます。

`s.products=";prodA;1;25.12;;**evar4=12.34**,;prodB;1;10.99;;**evar4=1.23**"`

配列ではない変数（単一の値）をマーチャンダイジング `eVar` にマッピングすると、その単一の値が各製品に適用されます。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.product_discount = "**1.99**";
```

上記と同じマッピングを使用した場合、生成される `s.products` 文字列は次のようになります。

`s.products=";prodA;1;25.12;;**evar4=1.99**,;prodB;1;10.99;;**evar4=1.99**"`

### 製品レベルのイベント

製品レベルのイベントは、マーチャンダイジング `eVars` と同様に機能します。単一の値を使用して製品文字列内のすべての製品に同じ変数を適用することも、値の配列を使用して製品文字列内の各製品に異なる値を適用することもできます。

#### 例：

```
utag_data.product_id       = ["prodA", "prodB"];
utag_data.product_price    = ["25.12", "10.99"];
utag_data.order_discount   = "**12.00**";
```

次に、`order_discount` を `product event15` にマッピングすると、次の `s.products` 文字列が生成されます。

`s.products=";prodA;1;25.12;**event15=12.00**;,;prodB;1;10.99;**event15=12.00**;"`

両方の製品に同じ注文割引が適用されていることに注意してください。


<blockquote>
Mapping arrays for merchandising `eVars` and product-level events is available in version H.26 and newer.
</blockquote>


## doPlugins に必要な拡張機能

`s_code.js` ファイル内の次の 2 つのコードセクションを、TiQ 構成の拡張機能にコピーする必要があります。

* Do Plugins セクション
* Plugins and Modules

### Do Plugins

**Do Plugins** セクションは、`s_code.js` 内で常に **Plugins and Modules** セクションより前にあります。通常、このセクションは次の行から始まります。

```
/* Plugin Config */
s.usePlugins=true;
```

これらの行から、次の行までをすべてコピーします。

```
s.doPlugins=s_doPlugins;
```

このコードブロックを、Adobe Analytics タグをスコープとする [JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/) に貼り付け、拡張機能に `Do Plugins Section` という名前を付けます。

![](https://docs.tealium.com/images/client-side-tags/do-plugins-extension.jpg)

### Plugins and Modules

`s_code` の Plugins and Modules セクションは、次の行から始まります。

```
/***********************PLUGINS SECTION ********************/
```

そして、次の行の直前で終わります。

```
/************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
```

このコードセクション全体をコピーし、Adobe Analytics タグをスコープとする 2 つ目の JavaScript Code 拡張機能に貼り付けます。この拡張機能に `Plugins and Modules` という名前を付けます。

![](https://docs.tealium.com/images/client-side-tags/plugins-and-modules.jpg)

次に、**Plugins and Modules** JavaScript 拡張機能を、**Do Plugins** セクションの JavaScript 拡張機能のすぐ上にドラッグします。

次の行で始まるコードセクションは、

```
/************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
```

Adobe のコア `s_code` ライブラリであり、TiQ 内のタグテンプレートを通じて読み込まれます。

## 新しいバージョンへのアップグレード

次の手順で、Adobe タグを新しいベースコードにアップグレードします。

1. タグを開き、**Edit** をクリックします。
1. **S-Code Version** フィールドで、ドロップダウンリストから目的のバージョン（例：**H.27**）を選択します。  
![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-legacey-tag-select-upgrade-version.jpg)  
タグテンプレートの更新が必要であることを示す警告モーダルが表示されます。
1. **OK** をクリックします。  
![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-legacy-upgrade-message.jpg)
1. **Advanced Settings** まで下にスクロールし、クリックして展開します。
1. **Edit Templates** を選択します。
1. テキストフィールド内のテンプレート全体をコピーし、バックアップとしてテキストファイルに貼り付けます。
1. 現在のテンプレートを選択し、ゴミ箱アイコンをクリックして削除します。
1. 変更を保存してパブリッシュします。  
これで、最新バージョンのタグが読み込まれます。

## 詳細構成

### s.events の構成

Adobe タグテンプレート内で、Tealium は `s.event` 文字列の構成を支援する `u.addEvent()` という関数を提供しています。このメソッドは `s.events` の末尾に新しい値を追加するため、構成済みのイベントをすべて維持しながら、必要に応じて別のイベントを追加できます。このメソッドを使用するには、構成内に `sc_events` という変数が必要です。

`u.addEvent` を使用して `s.events` をカスタマイズするには、次の手順を実行します。

1. [Set Data Values](https://docs.tealium.com/set-data-values-extension/) 拡張機能を追加します。
1. **Scope** を Adobe Analytics タグに構成します。
1. **Set** メニューから **sc_events** を選択します。
1. **To** メニューから **JS Code** を選択します。
1. テキストフィールドに `u.addEvent("CUSTOM_EVENT")` と入力します。  
ここで `CUSTOM_EVENT` は、**event10** など、`s.events` 文字列に追加するイベントです。
1. 1 つの手順で複数のイベントを追加するには、次のように配列を `u.addEvent` に渡します。  
`u.addEvent(["event1","event2","scView"]);`
### SiteCatalyst の動的変数

Adobe は、複数のプロパティに出現する値を再利用してトラッキングピクセルのサイズを最小限に抑える「動的変数」という表記法をサポートしています。

TiQ の Adobe タグは、ピクセルリクエストを Adobe に送信する際に、この表記法を自動的に適用します。そのため、変数のいずれかに `v3:D=c2` のような値が表示される場合があります。この場合、`v3` は `eVar3` を表し、`D=c2` は `s.prop2` の値を表します。`s.prop2` の値を繰り返す代わりに、この短縮表記が `prop2` への参照として使用され、Adobe のサーバーで適切に解釈されます。これにより、生成されるトラッキングピクセルがより小さく高速になり、1 回のピクセルリクエストに最大限のデータを格納できます。

![](https://docs.tealium.com/images/client-side-tags/sitecatalyst-dynamic-variables.jpg)

詳しくは、[SiteCatalyst の動的変数](http://omniture.custhelp.com/app/answers/detail/a_id/10099)を参照してください。