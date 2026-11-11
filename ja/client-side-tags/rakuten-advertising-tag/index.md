---
title: Rakuten Advertisingタグ構成ガイド
description: この記事では、タグ管理アカウントでRakuten Advertisingタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rakuten-advertising-tag/
---
## タグに関するヒント

* **Extract From Code**フィールドに`affiliateConfig`オブジェクトを貼り付けると、タグによって`ranMID`、`discountType`、`includeStatus`パラメータが自動的に入力されます。
* 注文IDが構成されると、コンバージョンが発火します。
* アフィリエイト機能は、**Allow Commission**が`True`に構成されている場合にのみ利用できます。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 税額（`_ctax`）
  * 通貨（`_ccurrency`）
  * プロモーションコード（`_cpromo`）
  * 顧客ID（`_ccustid`）
  * 商品IDのリスト（`_cprod`）
  * 商品名のリスト（`_cprodname`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）
  * 割引のリスト（`_cpdisc`）

### タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **Tracking Key**：Rakuten Marketingの連携担当者から発行された、サイト固有のトラッキングキー。
* **Rakuten Affiliate Merchant ID**：4桁または5桁のマーチャントID。
* **Tax Rate**：パーセント値で指定する税率。たとえば、英国のVATが20%の場合は`20`と指定します。
* **Conversion Type**：デフォルト値は`sale`ですが、任意の値に構成できます。
* **Discount Type**：アフィリエイト販売の割引タイプ。デフォルト値は`order`ですが、`item`に構成することもできます。
* **Include Status**：注文ステータスをタグに含めるかどうか。デフォルト値は`false`です。

### データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

#### 標準

|変数| 説明|
|---| ---|
|`trackingKey`|  <ul><li>トラッキングキー</li></ul> |
|`conversionType`|  <ul><li>コンバージョンタイプ</li></ul> |
|`customerStatus`|  <ul><li>顧客ステータス</li></ul> |
|`discountAmount`|  <ul><li>割引額</li></ul> |
|`optionalData`|  <ul><li>オプションデータ</li></ul> |

#### Eコマース

配列変数（`product_id`、`product_name`、`product_quantity`、`product_unit_price`、`product_sku`）は、Rakutenの明細項目にマッピングされます。その後、Rakutenライブラリがこれらの明細項目から`skulist`、`namelist`、`qlist`、`amtlist`などのリスト形式のペイロードフィールドを構築します。

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税額。</li><li>`_ctax`を上書きします。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>`_ccurrency`を上書きします。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>`_cpromo`を上書きします。</li></ul> |
|`order_consumed`|  <ul><li>消費済み。</li></ul> |
|`order_shipped_country`|  <ul><li>注文の配送先国。</li></ul> |
|`order_status`|  <ul><li>注文ステータス。</li><li>値は次のとおりです。<ul><li>既存</li><li>リピーター</li><li>新規</li></ul> </li></ul> |
| `order_shipped` |  <ul><li>注文の発送状況。</li></ul> |
|`order_site_name`|  <ul><li>サイト名。</li></ul> |
|`customer_id`|  <ul><li>顧客ID。</li><li>`_ccustid`を上書きします。</li></ul> |
|`customer_score`|  <ul><li>顧客スコア。</li></ul> |
|`customer_country`|  <ul><li>顧客の国。</li><li>`_ccountry`を上書きします。</li><li>`order_shipped_country`が指定されていない場合、`order_shipped_country`の代わりに使用されます。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト。</li><li>`product_sku`が指定されていない場合、`product_sku`の代わりに使用されます。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>商品名のリスト。</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_sku`|  <ul><li>配列</li><li>SKUのリスト。</li><li>`_csku`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |
|`product_discount`|  <ul><li>配列</li><li>割引のリスト。</li><li>`_cpdisc`を上書きします。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドのリスト。</li><li>`_cbrand`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリーのリスト。</li><li>`_ccat`を上書きします。</li></ul> |
|`product_category_id`|  <ul><li>配列</li><li>カテゴリーIDのリスト。</li></ul> |
|`product_coupon`|  <ul><li>配列</li><li>クーポンのリスト。</li></ul> |
|`product_is_clearance`|  <ul><li>配列</li><li>クリアランスステータスのリスト。</li></ul> |
|`product_is_sale`|  <ul><li>配列</li><li>セールステータスのリスト。</li></ul> |
|`product_margin`|  <ul><li>配列</li><li>マージンのリスト。</li></ul> |

#### アフィリエイト

|変数| 説明|
|---| ---|
|`allowCommission`|  <ul><li>コミッションを許可</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.ranMID`|  <ul><li>ranMID</li></ul> |
| `affiliateConfig.taxRate` |  <ul><li>税率</li></ul> |
| `affiliateConfig.discountType` |  <ul><li>割引タイプ</li></ul> |
|`affiliateConfig.tagType`|  <ul><li>タグタイプ</li></ul> |
|`affiliateConfig.includeStatus`|  <ul><li>ステータスを含める</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.removeOrderTax`|  <ul><li>注文の税額を削除</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.removeTaxFromProducts`|  <ul><li>商品から税額を削除</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.removeTaxFromDiscount`|  <ul><li>割引から税額を削除。</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.centValues`|  <ul><li>セント単位の値。</li><li>値は`true`または`false`です。</li></ul> |
|`affiliateConfig.nonCentCurrencies`|  <ul><li>セント単位ではない通貨。</li><li>配列、または通貨をカンマ区切りで列挙した文字列を指定できます。</li></ul> |