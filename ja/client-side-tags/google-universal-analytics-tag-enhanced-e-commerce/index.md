---
title: Google Universal Analytics タグ拡張 E-コマース
description: この記事は、Tealium iQ タグ管理で Google Universal Analytics タグの拡張 E コマース トラッキングを構成する概要です。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/
---
 2023年7月1日より、Google Universal Analytics プロパティはヒットの処理を停止しました。このタグは非推奨となり、タグマーケットプレイスではもはや利用できません。現在のタグについては、[Google Analytics 4]()をご覧ください。

## 概要

拡張 E コマースは、[Google Universal Analytics を使用した E コマース トラッキングのための高度なプラグイン](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)で、ウェブサイト上の製品とのユーザーのインタラクションを追跡します。これには、製品の印象、製品のクリック、製品詳細の表示、ショッピングカートへの製品の追加、チェックアウトプロセスの開始、トランザクション、および払い戻しが含まれます。

## 動作方法

拡張 E コマース トラッキングは、[E-コマース拡張機能]()と[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を組み合わせて[Google Universal Analytics タグ]()で動作します。E-コマース拡張機能は、最も一般的な E コマース データを処理し、より高度なデータはタグ構成でのデータマッピングを使用して送信されます。拡張 E コマースのアクションもタグ内でイベントとしてマッピングされます。

## 拡張 E コマース データとアクション

E-コマース拡張構成は、新しい拡張 E コマース機能の多くをカバーしています。しかし、ユニバーサルデータオブジェクト (UDO) が[拡張 E コマースに必要なデータ](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data)を収容していない場合は、ウェブサイトのデータレイヤーに変数を追加する必要があります。

以下は、データレイヤー変数を追加するための推奨リストと、拡張 E コマースでのそれに対応する変数です。

変数が E-コマース拡張列で「n/a」とマークされている場合は、タグにデータマッピングとして追加する必要があります。

## 印象データ

印象データが UDO にマッピングされ、入力されると、`ec:addImpression` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース&lt;br&gt; 拡張|
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

|データレイヤー変数| Google キー| E-コマース&lt;br&gt; 拡張|
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

|データレイヤー変数| Google キー| E-コマース&lt;br&gt; 拡張|
|---| ---| ---|
|promotion\_id| id| n/a|
|promotion\_name| name| n/a|
|promotion\_creative| creative| n/a|
|promotion\_position| position| n/a|

## アクションデータ

アクション変数は、注文データを期待するイベントで入力されます。拡張 E コマースに必要な注文データは、E-コマース拡張機能を通じて自動的にマッピングされます（下記の表を参照）。アクション変数は、`ec:setAction` コマンドを使用して Google Analytics に渡されます。

|データレイヤー変数| Google キー| E-コマース&lt;br&gt; 拡張|
|---| ---| ---|
|order\_id| id| \_corder|
|order\_store| affiliation| \_cstore|
|order\_grand\_total| revenue| \_ctotal|
|order\_tax\_amount| tax| \_ctax|
|order\_shipping\_amount| shipping| \_cship|
|order\_promo\_code| coupon| \_cpromo|
|checkout\_step| step| n/a |
|shipping\_method,&lt;br&gt; shipping\_carrier,&lt;br&gt; payment\_method,&lt;br&gt; etc. &lt;br&gt; (various checkout options) | option| n/a |

## データマッピング

拡張 E コマースのアクションは、データマッピングを使用してトリガーされます。イベントの変数の値が対応する拡張 E コマースアクションにマッチするデータマッピングで、Google Analytics で `ec:setAction` コマンドをトリガーします。

データレイヤーにおける典型的なイベント変数は、`tealium_event`, `page_type`, または `event_name` です。

以下は、期待される拡張 E コマースアクションにマッピングされる Tealium イベントの提案です：

|Tealium イベント/ページタイプ| Google アクション&lt;br&gt; (enh\_action)|
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
 &#34;product_impression_id&#34;       : [&#39;P12345&#39;, &#39;P67890&#39;],
 &#34;product_impression_name&#34;     : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
 &#34;product_impression_brand&#34;    : [&#39;Tealium&#39;, &#39;Tealium&#39;],
 &#34;product_impression_variant&#34;  : [&#39;black&#39;, &#39;blue&#39;],
 &#34;product_impression_category&#34; : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
 &#34;product_impression_list&#34;     : [&#39;Search Results&#39;, &#39;Search Results&#39;],
 &#34;product_impression_position&#34; : [1, 2]
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
  &#34;tealium_event&#34;    : &#34;product_click&#34;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_position&#34; : [1]
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
  &#34;tealium_event&#34;    : &#34;product_view&#34;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;]
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
  &#34;tealium_event&#34;    : &#39;cart_add&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_price&#34;    : [&#39;23.49&#39;],
  &#34;product_quantity&#34; : [1]
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
  &#34;tealium_event&#34;    : &#39;cart_remove&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_price&#34;    : [&#39;23.49&#39;],
  &#34;product_quantity&#34; : [1]
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
  &#34;tealium_event&#34;    : &#39;checkout&#39;,
  &#34;product_id&#34;       : [&#39;P1235&#39;, &#39;P67890&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;, &#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;, &#39;blue&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
  &#34;product_price&#34;    : [&#39;23.39&#39;, &#39;11.00&#39;],
  &#34;product_quantity&#34; : [1, 2],
  &#34;product_position&#34; : [1, 2],
  &#34;checkout_step&#34;    : &#34;1&#34;,
  &#34;shipping_carrier&#34; : &#39;FedEx&#39;
};

```

Google Analyticsアカウント内の[チェックアウトファネル構成](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#checkout-funnel)を使用して、チェックアウトステップにより詳細な名前を割り当てることができます。

### チェックアウトオプション

チェックアウトオプションアクションでは、初期ページビュー後に訪問がサイトと対話している状態に関する情報をキャプチャできます。

チェックアウトオプションアクションで以下のデータを送信できます：

* チェックアウトステップ
* チェックアウトオプション

このイベントは `utag.link()` を使用して追跡され、Google Analyticsで `ec:setAction` (checkout\_option) コマンドをトリガーします。

```js
// 例：チェックアウトオプション
utag.link({
  &#34;tealium_event&#34;    : &#34;checkout_option&#34;,
  &#34;checkout_step&#34;    : &#34;2&#34;,
  &#34;shipping_carrier&#34; : &#34;FedEx&#34;
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
  &#34;tealium_event&#34;         : &#39;purchase&#39;,
  &#34;order_id&#34;              : &#39;O1234567&#39;,
  &#34;order_grand_total&#34;     : &#39;57.44&#39;,
  &#34;order_tax_amount&#34;      : &#39;3.65&#39;,
  &#34;order_shipping_amount&#34; : &#39;8.50&#39;,
  &#34;order_promo_code&#34;      : &#39;SALE20&#39;,
  &#34;product_id&#34;            : [&#39;P1235&#39;, &#39;P67890&#39;],
  &#34;product_name&#34;          : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
  &#34;product_brand&#34;         : [&#39;Tealium&#39;, &#39;Tealium&#39;],
  &#34;product_variant&#34;       : [&#39;black&#39;, &#39;blue&#39;],
  &#34;product_category&#34;      : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
  &#34;product_price&#34;         : [&#39;23.39&#39;, &#39;11.00&#39;],
  &#34;product_quantity&#34;      : [1, 2]
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
  &#34;tealium_event&#34;      : &#34;promo_click&#34;,
  &#34;promotion_id&#34;       : [&#39;DV18-EARLY-REG&#39;],
  &#34;promotion_name&#34;     : [&#39;DV 2018 Early Registration&#39;],
  &#34;promotion_creative&#34; : [&#39;early_reg_promo1&#39;],
  &#34;promotion_position&#34; : [1]
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
  &#34;tealium_event&#34;    : &#34;refund&#34;,
  &#34;order_id&#34;         : &#39;O123456&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_quantity&#34; : [1]
};
```

## 追加リソース

* [拡張Eコマースについて](https://support.google.com/analytics/answer/6014841?hl=ja) (Google Analytics)
* [analytics.jsを使用して拡張Eコマースデータを収集する方法](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) (Google Analytics)
