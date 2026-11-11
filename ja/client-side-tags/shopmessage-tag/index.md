---
title: ShopMessageタグ構成ガイド
description: この記事では、タグ管理アカウントでShopMessageタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/shopmessage-tag/
---
## タグに関するヒント

* 注文IDが存在する場合、PurchaseCompleteイベントが発生します。
* マッピングを使用すると、次のことができます。
  * 標準構成値を動的に上書きする
  * イベントトリガーを構成する
  * 必須、任意、およびカスタムのイベントパラメータを送信する
  * Eコマース拡張機能の値を上書きする
  * 一覧にない商品変数については、`custom`を送信する変数に置き換えて、**カスタム商品変数名**を使用する

* 次のEコマース拡張機能パラメータをサポートしています。
  * 注文ID
  * 注文合計
  * 注文小計
  * 配送料
  * 税額
  * 通貨
  * 顧客ID
  * 顧客の市区町村
  * 顧客の都道府県・州
  * 顧客の郵便番号
  * 顧客の国
  * 商品IDのリスト
  * 名前のリスト
  * SKUのリスト
  * カテゴリのリスト
  * 数量のリスト
  * 価格のリスト

* 実装ガイド：<https://help.shopmessage.me/en/articles/1443137-integrating-shopmessage-with-your-store>

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **アカウントID**：src URLに含まれる英数字の値
* **c_id**：src URL内の`initialize.js?c=`の後にある英数字の値
* **Facebookログイン**
* **Facebookオプトイン**

### データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

#### 標準

| 変数                         | 説明             |
|:-----------------------------|:-----------------|
| アカウントID                 | (`account_id`)   |
| `c_id`                       | (`c_id`)         |
| Facebookログイン（`fb_login`） | [`true`/`false`] |
| Facebookオプトイン（`fb_optin`） | [`true`/`false`] |

#### Eコマース

| 変数                                                         | 説明                                           |
|:-------------------------------------------------------------|:-----------------------------------------------|
| 注文ID                                                       | (`order_id`)（`_corder`を上書き）              |
| 注文合計                                                     | (`order_total`)（`_ctotal`を上書き）           |
| 注文小計                                                     | (`order_subtotal`)（`_csubtotal`を上書き）     |
| 配送料                                                       | (`order_shipping`)（`_cship`を上書き）         |
| 税額                                                         | (`order_tax`)（`_ctax`を上書き）               |
| 通貨                                                         | (`order_currency`)（`_ccurrency`を上書き）     |
| 顧客ID                                                       | (`customer_id`)（`_ccustid`を上書き）          |
| 顧客の市区町村                                               | (`customer_city`)（`_ccity`を上書き）          |
| 顧客の都道府県・州                                           | (`customer_state`)（`_cstate`を上書き）        |
| 顧客の郵便番号                                               | (`customer_zip`)（`_czip`を上書き）            |
| 顧客の国                                                     | (`customer_country`)（`_ccountry`を上書き）    |
| 商品IDのリスト（`product_id`）（`_cprod`を上書き）           | [配列]                                         |
| 名前のリスト（`product_name`）（`_cprodname`を上書き）       | [配列]                                         |
| SKUのリスト（`product_sku`）（`_csku`を上書き）              | [配列]                                         |
| カテゴリのリスト（`product_category`）（`_ccat`を上書き）    | [配列]                                         |
| 数量のリスト（`product_quantity`）（`_cquan`を上書き）       | [配列]                                         |
| 価格のリスト（`product_unit_price`）（`_cprice`を上書き）    | [配列]                                         |

#### イベントトリガー

| 変数               | 説明               |
|:-------------------|:-------------------|
| `ViewProduct`      | ViewProduct        |
| `UpdateCart`       | UpdateCart         |
| `PurchaseComplete` | PurchaseComplete   |

#### イベントデータ：ViewProduct

| 変数         | 説明                                                               |
|:-------------|:-------------------------------------------------------------------|
| タイトル     | (`ViewProduct.title`)（Eコマースの商品名を上書き）                 |
| 価格         | (`ViewProduct.price`)（Eコマースの商品単価を上書き）               |
| 商品ID       | (`ViewProduct.product_id`)（Eコマースの商品IDを上書き）            |
| 商品タイプ   | (`ViewProduct.product_type`)（Eコマースの商品カテゴリを上書き）    |
| 色           | (`ViewProduct.color`)                                               |
| スタイル     | (`ViewProduct.style`)                                               |
| 画像         | (`ViewProduct.image`)                                               |
| 商品URL      | (`ViewProduct.product_url`)                                         |
| タグ         | (`ViewProduct.tags`)                                                |
| ベンダー     | (`ViewProduct.vendor`)                                              |
#### イベントデータ：UpdateCart

| 変数                                                                                   | 説明                                                         |
|:---------------------------------------------------------------------------------------|:-------------------------------------------------------------|
| 合計価格                                                                               | (`UpdateCart.total_price`)（Eコマース注文合計を上書き）       |
| CTA URL                                                                                | (`UpdateCart.cta_url`)                                       |
| 商品タイトル (`UpdateCart.items.title`)（Eコマース商品名を上書き）                     | [配列]                                                       |
| 商品価格 (`UpdateCart.items.price`)（Eコマース商品の単価を上書き）                     | [配列]                                                       |
| 商品通貨 (`UpdateCart.items.currency`)（Eコマース通貨を上書き）                        | [配列]                                                       |
| 商品ID (`UpdateCart.items.product_id`)（Eコマース商品IDを上書き）                      | [配列]                                                       |
| バリアントID (`UpdateCart.items.variant_id`)                                           | [配列]                                                       |
| 商品SKU (`UpdateCart.items.sku`)                                                       | [配列]                                                       |
| 商品サイズ (`UpdateCart.items.size`)                                                   | [配列]                                                       |
| 商品カラー (`UpdateCart.items.color`)                                                  | [配列]                                                       |
| 商品画像 (`UpdateCart.items.image`)                                                    | [配列]                                                       |
| 商品URL (`UpdateCart.items.product_url`)                                               | [配列]                                                       |
| 商品数量 (`UpdateCart.items.quantity`)（Eコマース商品数量を上書き）                    | [配列]                                                       |
| 商品タグ (`UpdateCart.items.tags`)                                                     | [配列]                                                       |
| カスタム商品変数名 (`UpdateCart.items.custom`)                                         | [配列]                                                       |
#### イベントデータ：PurchaseComplete

| 変数                                                                                   | 説明                                                                      |
|:-------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------|
| 注文ID                                                                                   | (`PurchaseComplete.order_id`)（Eコマースの注文IDを上書き）                     |
| チェックアウトトークン                                                                             | (`PurchaseComplete.checkout_token`)                                               |
| 作成日時                                                                                 | (`PurchaseComplete.created_at`)                                                   |
| 注文ステータスURL                                                                           | (`PurchaseComplete.order_status_url`)                                            |
| 通貨                                                                                   | (`PurchaseComplete.currency`)（Eコマースの通貨を上書き）                      |
| 合計金額                                                                                | (`PurchaseComplete.total_price`)（Eコマースの注文合計を上書き）               |
| 小計金額                                                                             | (`PurchaseComplete.subtotal_price`)（Eコマースの注文小計を上書き）         |
| 税額合計                                                                                  | (`PurchaseComplete.total_tax`)（Eコマースの税額を上書き）                  |
| 送料                                                                             | (`PurchaseComplete.shipping_price`)（Eコマースの送料を上書き）        |
| プラットフォーム                                                                                   | (`PurchaseComplete.platform`)                                                      |
| 住所1                                                                                  | (`PurchaseComplete.shipping_address.address1`)                                    |
| 住所2                                                                                  | (`PurchaseComplete.shipping_address.address2`)                                    |
| 名                                                                                 | (`PurchaseComplete.shipping_address.first_name`)                                 |
| 姓                                                                                  | (`PurchaseComplete.shipping_address.last_name`)                                  |
| 氏名                                                                                  | (`PurchaseComplete.shipping_address.full_name`)                                  |
| 市区町村                                                                                       | (`PurchaseComplete.shipping_address.city`)（Eコマースの顧客の市区町村を上書き）   |
| 都道府県                                                                                      | (`PurchaseComplete.shipping_address.state`)（Eコマースの顧客の都道府県を上書き） |
| 郵便番号                                                                                   | (`PurchaseComplete.shipping_address.zip`)（Eコマースの顧客の郵便番号を上書き）     |
| 電話番号                                                                               | (`PurchaseComplete.shipping_address.phone`)                                       |
| 商品名 (`PurchaseComplete.items.title`)（Eコマースの商品名を上書き）           | [配列]                                                                          |
| 商品価格 (`PurchaseComplete.items.price`)（Eコマースの商品単価を上書き）     | [配列]                                                                          |
| 商品ID (`PurchaseComplete.items.product_id`)（Eコマースの商品IDを上書き）          | [配列]                                                                          |
| バリエーションID (`PurchaseComplete.items.variant_id`)                                            | [配列]                                                                          |
| 商品SKU (`PurchaseComplete.items.sku`)（Eコマースの商品SKUを上書き）                | [配列]                                                                          |
| 商品サイズ (`PurchaseComplete.items.size`)                                                 | [配列]                                                                          |
| 商品カラー (`PurchaseComplete.items.color`)                                               | [配列]                                                                          |
| 商品画像 (`PurchaseComplete.items.image`)                                               | [配列]                                                                          |
| 商品URL (`PurchaseComplete.items.product_url`)                                          | [配列]                                                                          |
| 商品数量 (`PurchaseComplete.items.quantity`)（Eコマースの商品数量を上書き） | [配列]                                                                          |
| 商品タグ (`PurchaseComplete.items.tags`)                                                 | [配列]                                                                          |
| カスタム商品変数名 (`PurchaseComplete.items.custom`)                               | [配列]                                                                          |
| 顧客のメールアドレス                                                                             | (`PurchaseComplete.customer_properties.email`)                                    |
| 顧客ID                                                                                | (`PurchaseComplete.customer_properties.id`)（Eコマースの顧客IDを上書き）    |
| 顧客の名                                                                        | (`PurchaseComplete.customer_properties.first_name`)                              |
| 顧客の姓                                                                         | (`PurchaseComplete.customer_properties.last_name`)                               |

#### 訪問パラメーター

| 変数        | 説明                                               |
|:----------------|:----------------------------------------------------------|
| 顧客ID     | (`visitor.customer_id`)（Eコマースの顧客IDを上書き） |
| 住所1       | (`visitor.address1`)                                        |
| 住所2       | (`visitor.address2`)                                        |
| 名      | (`visitor.first_name`)                                     |
| 姓       | (`visitor.last_name`)                                      |
| 氏名       | (`visitor.full_name`)                                      |
| 性別          | (`visitor.gender`)                                          |
| 言語        | (`visitor.language`)                                        |
| 市区町村            | (`visitor.city`)（Eコマースの顧客の市区町村を上書き）       |
| 都道府県           | (`visitor.state`)（Eコマースの顧客の都道府県を上書き）     |
| 郵便番号        | (`visitor.zip`)（Eコマースの顧客の郵便番号を上書き）         |
| 電話番号    | (`visitor.phone`)                                           |
| プロフィール画像 | (`visitor.profile_pic`)                                    |