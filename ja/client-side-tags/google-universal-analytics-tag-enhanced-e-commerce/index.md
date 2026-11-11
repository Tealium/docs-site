---
title: Google Universal Analyticsタグの拡張eコマース
description: この記事では、タグ管理でGoogle Universal Analyticsタグの拡張eコマーストラッキングを構成する方法の概要を説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/
---

<blockquote>
2023年7月1日をもって、Google Universal Analyticsプロパティではヒットの処理が停止されました。このタグは非推奨となり、タグマーケットプレイスでも利用できなくなりました。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)を参照してください。
</blockquote>


## 概要

拡張eコマースは、[Google Universal Analyticsを使用するeコマーストラッキングの高度なプラグイン](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)です。商品インプレッション、商品のクリック、商品詳細の表示、ショッピングカートへの商品の追加、決済プロセスの開始、トランザクション、払い戻しなど、Webサイト上の商品に対するユーザーの操作を追跡できます。

## 仕組み

拡張eコマーストラッキングは、[Google Universal Analyticsタグ](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/)で[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)と[データマッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を組み合わせて動作します。Eコマース拡張機能は一般的なeコマースデータを処理し、より高度なデータはタグ構成のデータマッピングを使用して送信されます。拡張eコマースのアクションも、タグ内でイベントとしてマッピングされます。

## 拡張eコマースのデータとアクション

Eコマース拡張機能の構成では、拡張eコマースの新機能の多くがカバーされています。ただし、Universal Data Object（UDO）が[拡張eコマースに必要なデータ](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data)に対応していない場合は、Webサイトのデータレイヤーに変数を追加する必要があります。

以下は、追加を推奨するデータレイヤー変数と、それに対応する拡張eコマースの変数の一覧です。


<blockquote>
Eコマース拡張機能列で変数が「n/a」と記載されている場合、その変数をデータマッピングとしてタグに追加する必要があります。
</blockquote>


## インプレッションデータ

インプレッションデータがマッピングされ、UDOに値が構成されると、`ec:addImpression`コマンドを使用してGoogle Analyticsに渡されます。

|データレイヤー変数| Googleキー| Eコマース<br>拡張機能|
|---| ---| ---|
|product\_impression\_id| id| n/a|
|product\_impression\_name| name| n/a|
|product\_impression\_list| list| n/a|
|product\_impression\_brand| brand| n/a|
|product\_impression\_category| category| n/a|
|product\_impression\_variant| variant| n/a|
|product\_impression\_position| position| n/a|
|product\_impression\_price| price| n/a|

## 商品データ

商品変数は、商品データを必要とするすべてのイベントで使用されます。拡張eコマースで必要となる商品データは、Eコマース拡張機能によって自動的にマッピングされます（以下の表を参照）。商品変数は、`ec:addProduct`コマンドを使用してGoogle Analyticsに渡されます。

|データレイヤー変数| Googleキー| Eコマース<br>拡張機能|
|---| ---| ---|
|product\_id| id| \_cprod|
|product\_name| name| \_cprodname|
|product\_brand| brand| \_cbrand|
|product\_category| category| \_ccat|
|product\_variant| variant| n/a|
|product\_price| price| \_cprice |
|product\_quantity| quantity| \_cquan|
|product\_promo\_code| coupon| \_cpdisc|
|product\_position| position| n/a|

## プロモーションデータ

プロモーションデータがマッピングされ、UDOに値が構成されると、`ec:addPromo`コマンドを使用してGoogle Analyticsに渡されます。

|データレイヤー変数| Googleキー| Eコマース<br>拡張機能|
|---| ---| ---|
|promotion\_id| id| n/a|
|promotion\_name| name| n/a|
|promotion\_creative| creative| n/a|
|promotion\_position| position| n/a|

## アクションデータ

アクション変数は、注文データを必要とするすべてのイベントで値が構成されます。拡張eコマースで必要となる注文データは、Eコマース拡張機能によって自動的にマッピングされます（以下の表を参照）。アクション変数は、`ec:setAction`コマンドを使用してGoogle Analyticsに渡されます。

|データレイヤー変数| Googleキー| Eコマース<br>拡張機能|
|---| ---| ---|
|order\_id| id| \_corder|
|order\_store| affiliation| \_cstore|
|order\_grand\_total| revenue| \_ctotal|
|order\_tax\_amount| tax| \_ctax|
|order\_shipping\_amount| shipping| \_cship|
|order\_promo\_code| coupon| \_cpromo|
|checkout\_step| step| n/a |
|shipping\_method、<br> shipping\_carrier、<br> payment\_method、<br> など <br>（各種決済オプション）| option| n/a |

## データマッピング

拡張eコマースのアクションは、データマッピングを使用してトリガーされます。イベントのデータマッピングでは、イベント変数の値を対応する拡張eコマースのアクションに一致させます。これらのマッピングによって、Google Analyticsの`ec:setAction`コマンドがトリガーされます。

データレイヤーで一般的に使用されるイベント変数は、`tealium_event`、`page_type`、`event_name`などです。

以下は、想定される拡張eコマースのアクションにマッピングするTealiumイベントの推奨例です。

|Tealiumイベント／ページタイプ| Googleアクション<br>（enh\_action）|
|---| ---|
|product\_click| click|
|product\_view| detail|
|cart\_add| add|
|cart\_remove| remove|
|checkout| checkout|
|checkout\_option| checkout\_option|
|purchase| purchase|
|refund | refund|
|promo\_click| promo\_click|

## 例

拡張eコマースのアクションをトリガーするには、データマッピングでイベント変数をイベントにマッピングします。

### 商品インプレッション

商品インプレッションアクションでは、以下のデータを送信できます。

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリエーションのリスト
* 商品リスト名

このイベントは、`utag_data`または`utag.view()`を使用してページ読み込み時に発生し、配列内の各項目についてGoogle Analyticsの`ec:addImpression`コマンドをトリガーします。

```js
// EXAMPLE CODE: Product Detail Page View
var utag_data = {
 "product_impression_id"       : ['P12345', 'P67890'],
 "product_impression_name"     : ['DV T-Shirt', 'DV Water Bottle'],
 "product_impression_brand"    : ['Tealium', 'Tealium'],
 "product_impression_variant"  : ['black', 'blue'],
 "product_impression_category" : ['Shirts', 'Home & Office'],
 "product_impression_list"     : ['Search Results', 'Search Results'],
 "product_impression_position" : [1, 2]
};
```

### 商品のクリック

商品の`click`アクションでは、以下のデータを送信します。

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリエーションのリスト
* 商品の位置

このイベントは`utag.link()`を使用して追跡され、Google Analyticsの`ec:addProduct`コマンドと`ec:setAction`（click）コマンドをトリガーします。

```js
// EXAMPLE CODE: Product Click
utag.link({
  "tealium_event"    : "product_click",
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_position" : [1]
});

```

### 商品の表示／詳細

商品の`detail`アクションでは、以下のデータを送信できます。

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリエーションのリスト

このイベントは、`utag_data`または`utag.view()`を使用してページ読み込み時に追跡され、Google Analyticsの`ec:addProduct`コマンドと`ec:setAction`（detail）コマンドをトリガーします。

```js
// EXAMPLE CODE: Product Detail Page View
var utag_data = {
  "tealium_event"    : "product_view",
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts']
};

```
### カートへの追加

カートの `add` アクションでは、次のデータを送信できます。

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリエーションのリスト
* 商品の位置

このイベントは `utag.link()` を使用してトラッキングされ、Google Analyticsで `ec:addProduct` コマンドと `ec:setAction`（add）コマンドをトリガーします。

```js
// EXAMPLE CODE: Product Add
utag.link({
  "tealium_event"    : 'cart_add',
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_price"    : ['23.49'],
  "product_quantity" : [1]
});

```

### カートからの削除

カートの `remove` アクションでは、次のデータを送信できます。

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリエーションのリスト

このイベントは `utag.link()` を使用してトラッキングされ、Google Analyticsで `ec:addProduct` コマンドと `ec:setAction`（remove）コマンドをトリガーします。

```js
// EXAMPLE CODE: Product Cart Removal
utag.link({
  "tealium_event"    : 'cart_remove',
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_price"    : ['23.49'],
  "product_quantity" : [1]
});

```

### チェックアウト

`checkout` アクションでは、次のデータを送信できます。

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* チェックアウトステップ
* チェックアウトオプション
* バリエーションのリスト
* 商品の位置

このイベントは、ページ読み込み時に `utag_data` または `utag.view()` を使用してトラッキングされ、Google Analyticsで `ec:addProduct` コマンドと `ec:setAction`（checkout）コマンドをトリガーします。

```js
// EXAMPLE CODE: Checkout
var utag_data = {
  "tealium_event"    : 'checkout',
  "product_id"       : ['P1235', 'P67890'],
  "product_name"     : ['DV T-Shirt', 'DV Water Bottle'],
  "product_brand"    : ['Tealium', 'Tealium'],
  "product_variant"  : ['black', 'blue'],
  "product_category" : ['Shirts', 'Home & Office'],
  "product_price"    : ['23.39', '11.00'],
  "product_quantity" : [1, 2],
  "product_position" : [1, 2],
  "checkout_step"    : "1",
  "shipping_carrier" : 'FedEx'
};

```


<blockquote>
Checkout steps can be assigned more descriptive names using the [Checkout Funnel Configuration](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#checkout-funnel) within your Google Analytics account.
</blockquote>


### チェックアウトオプション

チェックアウトオプションアクションを使用すると、最初のページビュー後、訪問がサイトを操作しているときのチェックアウト状態に関する情報を取得できます。

チェックアウトオプションアクションでは、次のデータを送信できます。

* チェックアウトステップ
* チェックアウトオプション

このイベントは `utag.link()` を使用してトラッキングされ、Google Analyticsで `ec:setAction`（checkout\_option）コマンドをトリガーします。

```js
// EXAMPLE CODE: Checkout Option
utag.link({
  "tealium_event"    : "checkout_option",
  "checkout_step"    : "2",
  "shipping_carrier" : "FedEx"
});
```

### 購入

`purchase` アクションでは、次のデータを送信できます。

* 注文ID
* 売上
* 税額
* 送料
* プロモーションコード
* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリエーションのリスト

このイベントは、ページ読み込み時に `utag_data` または `utag.view()` を使用してトラッキングされ、Google Analyticsで `purchase` コマンドをトリガーします。

```js
// EXAMPLE CODE: Checkout
// The following information should be in the data object on page load
var utag_data = {
  "tealium_event"         : 'purchase',
  "order_id"              : 'O1234567',
  "order_grand_total"     : '57.44',
  "order_tax_amount"      : '3.65',
  "order_shipping_amount" : '8.50',
  "order_promo_code"      : 'SALE20',
  "product_id"            : ['P1235', 'P67890'],
  "product_name"          : ['DV T-Shirt', 'DV Water Bottle'],
  "product_brand"         : ['Tealium', 'Tealium'],
  "product_variant"       : ['black', 'blue'],
  "product_category"      : ['Shirts', 'Home & Office'],
  "product_price"         : ['23.39', '11.00'],
  "product_quantity"      : [1, 2]
};

```

### プロモーションクリック

プロモーションクリックアクションでは、次のデータを送信できます。

* プロモーションID
* プロモーション名
* プロモーションのクリエイティブ
* プロモーションの位置

このイベントは `utag.link()` を使用してトラッキングされ、Google Analyticsで `ec:addPromo` コマンドと `ec:setAction`（promo\_click）コマンドをトリガーします。

```js
// EXAMPLE CODE: Promotion Click
utag.link({
  "tealium_event"      : "promo_click",
  "promotion_id"       : ['DV18-EARLY-REG'],
  "promotion_name"     : ['DV 2018 Early Registration'],
  "promotion_creative" : ['early_reg_promo1'],
  "promotion_position" : [1]
});

```

### 払い戻し

払い戻しアクションを実行するには、払い戻し対象トランザクションの注文IDが必要です。一部払い戻しの場合は、払い戻し対象商品の商品IDも必要です。

* 注文ID
* 商品IDのリスト（一部払い戻しの場合のみ）

* 数量のリスト

このイベントは、ページ読み込み時に `utag_data` または `utag.view()` を使用してトラッキングされ、Google Analyticsで `ec:addProduct` コマンドと `ec:setAction`（refund）コマンドをトリガーします。

```js
// EXAMPLE CODE: Refund
var utag_data = {
  "tealium_event"    : "refund",
  "order_id"         : 'O123456',
  "product_id"       : ['P12345'],
  "product_quantity" : [1]
};
```

## その他のリソース

* [拡張eコマースについて](https://support.google.com/analytics/answer/6014841?hl=en)（Google Analytics）
* [analytics.jsを使用して拡張eコマースデータを収集する方法](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)（Google Analytics）