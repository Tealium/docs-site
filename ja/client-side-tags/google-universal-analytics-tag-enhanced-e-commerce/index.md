---
title: Google Universal Analytics タグ拡張 E-コマース
description: この記事は、Tealium iQ タグ管理で Google Universal Analytics タグの拡張 E コマース トラッキングを構成する概要です。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/
---

<blockquote>
2023年7月1日より、Google Universal Analytics プロパティはヒットの処理を停止しました。このタグは非推奨となり、タグマーケットプレイスではもはや利用できません。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)をご覧ください。
</blockquote>


## 概要

拡張 E コマースは、[Google Universal Analytics を使用した E コマース トラッキングのための高度なプラグイン](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)で、ウェブサイト上の製品とのユーザーのインタラクションを追跡します。これには、製品の印象、製品のクリック、製品詳細の表示、ショッピングカートへの製品の追加、チェックアウトプロセスの開始、トランザクション、および払い戻しが含まれます。

## 動作方法

拡張 E コマース トラッキングは、[E-コマース拡張機能](https://docs.tealium.com/e-commerce-extension/)と[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を組み合わせて[Google Universal Analytics タグ](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/)で動作します。E-コマース拡張機能は、最も一般的な E コマース データを処理し、より高度なデータはタグ構成でのデータマッピングを使用して送信されます。拡張 E コマースのアクションもタグ内でイベントとしてマッピングされます。

## 拡張 E コマース データとアクション

E-コマース拡張構成は、新しい拡張 E コマース機能の多くをカバーしています。しかし、ユニバーサルデータオブジェクト (UDO) が[拡張 E コマースに必要なデータ](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data)を収容していない場合は、ウェブサイトのデータレイヤーに変数を追加する必要があります。

以下は、データレイヤー変数を追加するための推奨リストと、拡張 E コマースでのそれに対応する変数です。


<blockquote>
変数が E-コマース拡張列で「n/a」とマークされている場合は、タグにデータマッピングとして追加する必要があります。
</blockquote>


## 印象データ

印象データが UDO にマッピングされ、入力されると、`ec:addImpression` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース<br> 拡張|
|---| ---| ---|
|product\_impression\_id| id| n/a|
|product\_impression\_name| name| n/a|
|product\_impression\_list| list| n/a|
|product\_impression\_brand| brand| n/a|
|product\_impression\_category| category| n/a|
|product\_impression\_variant| variant| n/a|
|product\_impression\_position| position| n/a|
|product\_impression\_price| price| n/a|

## 製品データ

製品変数は、製品データを期待するイベントで使用されます。拡張 E コマースに必要な製品データは、E-コマース拡張機能を通じて自動的にマッピングされます（下記の表を参照）。製品変数は、`ec:addProduct` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース<br> 拡張|
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

プロモーションデータが UDO にマッピングされ、入力されると、`ec:addPromo` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース<br> 拡張|
|---| ---| ---|
|promotion\_id| id| n/a|
|promotion\_name| name| n/a|
|promotion\_creative| creative| n/a|
|promotion\_position| position| n/a|

## アクションデータ

アクション変数は、注文データを期待するイベントで入力されます。拡張 E コマースに必要な注文データは、E-コマース拡張機能を通じて自動的にマッピングされます（下記の表を参照）。アクション変数は、`ec:setAction` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース<br> 拡張|
|---| ---| ---|
|order\_id| id| \_corder|
|order\_store| affiliation| \_cstore|
|order\_grand\_total| revenue| \_ctotal|
|order\_tax\_amount| tax| \_ctax|
|order\_shipping\_amount| shipping| \_cship|
|order\_promo\_code| coupon| \_cpromo|
|checkout\_step| step| n/a |
|shipping\_method,<br> shipping\_carrier,<br> payment\_method,<br> etc. <br> (various checkout options) | option| n/a |

## データマッピング

拡張 E コマースのアクションは、データマッピングを使用してトリガーされます。イベントの変数の値が対応する拡張 E コマースアクションにマッチするデータマッピングで、Google Analytics で `ec:setAction` コマンドをトリガーします。

データレイヤーにおける典型的なイベント変数は、`tealium_event`, `page_type`, または `event_name` です。

以下は、期待される拡張 E コマースアクションにマッピングされる Tealium イベントの提案です：

|Tealium イベント/ページタイプ| Google アクション<br> (enh\_action)|
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

拡張 E コマースアクションをトリガーするために、イベント変数をデータマッピングのイベントにマッピングします。

### 製品印象

製品印象アクションで以下のデータを送信できます：

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリアントのリスト
* 製品リスト名

このイベントはページロード時に `utag_data` を使用するか、`utag.view()` を使用してトリガーされ、配列内の各アイテムに対して Google Analytics で `ec:addImpression` コマンドをトリガーします。

```js
// 例：製品詳細ページビュー
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

### 製品クリック

製品 `click` アクションで以下のデータを送信します：

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリアントのリスト
* 製品位置

このイベントは `utag.link()` を使用して追跡され、Google Analytics で `ec:addProduct` および `ec:setAction` (click) コマンドをトリガーします。

```js
// 例：製品クリック
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

### 製品ビュー/詳細

製品 `detail` アクションで以下のデータを送信できます：

* IDのリスト（必須）
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* バリアントのリスト

このイベントはページロード時に `utag_data` を使用するか、`utag.view()` を使用して追跡され、Google Analytics で `ec:addProduct` および `ec:setAction` (detail) コマンドをトリガーします。

```js
// 例：製品詳細ページビュー
var utag_data = {
  "tealium_event"    : "product_view",
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts']
};

```
### カート追加

カートの `add` アクションで以下のデータを送信できます：

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリアントのリスト
* 商品位置

このイベントは `utag.link()` を使用して追跡され、Google Analyticsで `ec:addProduct` および `ec:setAction` (add) コマンドをトリガーします。

```js
// 例：商品追加
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

### カート削除

カートの `remove` アクションで以下のデータを送信できます：

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリアントのリスト

このイベントは `utag.link()` を使用して追跡され、Google Analyticsで `ec:addProduct` および `ec:setAction` (remove) コマンドをトリガーします。

```js
// 例：商品カート削除
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

`checkout` アクションで以下のデータを送信できます：

* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* チェックアウトステップ
* チェックアウトオプション
* バリアントのリスト
* 商品位置

このイベントはページロード時に `utag_data` または `utag.view()` を使用して追跡され、Google Analyticsで `ec:addProduct` および `ec:setAction` (checkout) コマンドをトリガーします。

```js
// 例：チェックアウト
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
Google Analyticsアカウント内の[チェックアウトファネル構成](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#checkout-funnel)を使用して、チェックアウトステップにより詳細な名前を割り当てることができます。
</blockquote>


### チェックアウトオプション

チェックアウトオプションアクションでは、初期ページビュー後に訪問がサイトと対話している状態に関する情報をキャプチャできます。

チェックアウトオプションアクションで以下のデータを送信できます：

* チェックアウトステップ
* チェックアウトオプション

このイベントは `utag.link()` を使用して追跡され、Google Analyticsで `ec:setAction` (checkout\_option) コマンドをトリガーします。

```js
// 例：チェックアウトオプション
utag.link({
  "tealium_event"    : "checkout_option",
  "checkout_step"    : "2",
  "shipping_carrier" : "FedEx"
});
```

### 購入

`purchase` アクションで以下のデータを送信できます：

* 注文ID
* 収益
* 税金
* 配送料
* プロモーションコード
* IDのリスト
* 名前のリスト
* ブランドのリスト
* カテゴリのリスト
* 数量のリスト
* 価格のリスト
* 割引のリスト
* バリアントのリスト

このイベントはページロード時に `utag_data` または `utag.view()` を使用して追跡され、Google Analyticsで `purchase` コマンドをトリガーします。

```js
// 例：購入
// ページロード時にデータオブジェクトに以下の情報が含まれるべきです
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

プロモクリックアクションでは、以下のデータを送信できます：

* プロモーションID
* プロモーション名
* プロモーションクリエイティブ
* プロモーション位置

このイベントは `utag.link()` を使用して追跡され、Google Analyticsで `ec:addPromo` および `ec:setAction` (promo\_click) コマンドをトリガーします。

```js
// 例：プロモーションクリック
utag.link({
  "tealium_event"      : "promo_click",
  "promotion_id"       : ['DV18-EARLY-REG'],
  "promotion_name"     : ['DV 2018 Early Registration'],
  "promotion_creative" : ['early_reg_promo1'],
  "promotion_position" : [1]
});

```

### 払い戻し

払い戻しアクションを発火するには、払い戻される取引の注文IDが必要です。部分払い戻しの場合は、払い戻される商品の商品IDも必要です。

* 注文ID
* 商品IDのリスト（部分払い戻しの場合のみ）

* 数量のリスト

このイベントはページロード時に `utag_data` または `utag.view()` を使用して追跡され、Google Analyticsで `ec:addProduct` および `ec:setAction` (refund) コマンドをトリガーします。

```js
// 例：払い戻し
var utag_data = {
  "tealium_event"    : "refund",
  "order_id"         : 'O123456',
  "product_id"       : ['P12345'],
  "product_quantity" : [1]
};
```

## 追加リソース

* [拡張Eコマースについて](https://support.google.com/analytics/answer/6014841?hl=ja) (Google Analytics)
* [analytics.jsを使用して拡張Eコマースデータを収集する方法](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) (Google Analytics)
