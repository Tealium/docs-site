---
title: ShopMessage タグの構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントに ShopMessage タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/shopmessage-tag/
---
## タグのヒント

* PurchaseComplete イベントは、注文IDが存在する場合に発生します。
* マッピングを使用して、以下の構成値を動的に上書きしたり、イベントトリガーを構成したり、必須、オプション、カスタムのイベントパラメータを送信したり、E-Commerce 拡張の値を上書きしたり、製品変数を使用したりすることができます。製品変数は、`custom` を置き換えて送信したい変数に対応します。

* 以下の E-Commerce 拡張パラメータをサポートしています：
  * 注文ID
  * 注文合計
  * 注文小計
  * 配送料金
  * 税金
  * 通貨
  * 顧客ID
  * 顧客の都市
  * 顧客の州
  * 顧客の郵便番号
  * 顧客の国
  * 製品IDのリスト
  * 名前のリスト
  * SKUのリスト
  * カテゴリのリスト
  * 数量のリスト
  * 価格のリスト

* 実装ガイド: &lt;https://help.shopmessage.me/en/articles/1443137-integrating-shopmessage-with-your-store&gt;

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、ShopMessageタグを追加します（タグの追加方法の詳細については、[タグの追加方法]()を参照してください）。

タグを追加した後、以下の構成を構成します：

* **アカウントID**：src URL内で見つかる英数字の値
* **c_id**：src URL内の`initialize.js?c=`の後に見つかる英数字の値
* **Facebookログイン**
* **Facebookオプトイン**

### データマッピング

マッピングとは、[データレイヤ変数]()からベンダータグの対応する変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法の詳細については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

#### 標準

| 変数                     | 説明      |
|:-----------------------------|:-----------------|
| アカウントID                   | (`account_id`)  |
| `c_id`                      | (`c_id`)        |
| Facebookログイン (`fb_login`) | [`true`/`false`] |
| Facebookオプトイン (`fb_optin`) | [`true`/`false`] |

#### E-Commerce

| 変数                                                   | 説明                                   |
|:-----------------------------------------------------------|:----------------------------------------------|
| 注文ID                                                   | (`order_id`) (Overrides `_corder`)          |
| 注文合計                                                | (`order_total`) (Overrides `_ctotal`)       |
| 注文小計                                             | (`order_subtotal`) (Overrides `_csubtotal`) |
| 配送料金                                            | (`order_shipping`) (Overrides `_cship`)         |
| 税金                                                 | (`order_tax`) (Overrides `_ctax`)               |
| 通貨                                                   | (`order_currency`) (Overrides `_ccurrency`)     |
| 顧客ID                                                | (`customer_id`) (Overrides `_ccustid`)          |
| 顧客の都市                                              | (`customer_city`) (Overrides `_ccity`)          |
| 顧客の州                                             | (`customer_state`) (Overrides `_cstate`)        |
| 顧客の郵便番号                                               | (`customer_zip`) (Overrides `_czip`)            |
| 顧客の国                                           | (`customer_country`) (Overrides `_ccountry`)    |
| 製品IDのリスト (`product_id`) (Overrides `_cprod`)      | [Array]                                       |
| 名前のリスト (`product_name`) (Overrides `_cprodname`)      | [Array]                                       |
| SKUのリスト (`product_sku`) (Overrides `_csku`)             | [Array]                                       |
| カテゴリのリスト (`product_category`) (Overrides `_ccat`)  | [Array]                                       |
| 数量のリスト (`product_quantity`) (Overrides `_cquan`) | [Array]                                       |
| 価格のリスト (`product_unit_price`) (Overrides `_cprice`) | [Array]                                       |

#### イベントトリガー

| 変数         | 説明      |
|:-----------------|:-----------------|
| `ViewProduct`      | ViewProduct      |
| `UpdateCart`       | UpdateCart       |
| `PurchaseComplete` | PurchaseComplete |

#### イベントデータ：ViewProduct

| 変数     | 説明                                                         |
|:-------------|:--------------------------------------------------------------------|
| タイトル        | (`ViewProduct.title`) (Overrides E-Commerce Product Name)             |
| 価格        | (`ViewProduct.price`) (Overrides E-Commerce Product Unit Price)       |
| 製品ID   | (`ViewProduct.product_id`) (Overrides E-Commerce Product ID)         |
| 製品タイプ | (`ViewProduct.product_type`) (Overrides E-Commerce Product Category) |
| カラー        | (`ViewProduct.color`)                                                 |
| スタイル        | (`ViewProduct.style`)                                                 |
| 画像        | (`ViewProduct.image`)                                                 |
| 製品URL  | (`ViewProduct.product_url`)                                          |
| タグ         | (`ViewProduct.tags`)                                                  |
| ベンダー       | (`ViewProduct.vendor`)                                                |

#### イベントデータ：UpdateCart

| 変数                                                                             | 説明                                                  |
|:-------------------------------------------------------------------------------------|:-------------------------------------------------------------|
| 合計価格                                                                          | (`UpdateCart.total_price`) (Overrides E-Commerce Order Total) |
| CTA URL                                                                              | (`UpdateCart.cta_url`)                                        |
| 製品タイトル (`UpdateCart.items.title`) (Overrides E-Commerce Product Name)           | [Array]                                                      |
| 製品価格 (`UpdateCart.items.price`) (Overrides E-Commerce Product Unit Price)     | [Array]                                                      |
| 製品通貨 (`UpdateCart.items.currency`) (Overrides E-Commerce Currency)         | [Array]                                                      |
| 製品ID (`UpdateCart.items.product_id`) (Overrides E-Commerce Product ID)          | [Array]                                                      |
| バリアントID (`UpdateCart.items.variant_id`)                                            | [Array]                                                      |
| 製品SKU (`UpdateCart.items.sku`)                                                   | [Array]                                                      |
| 製品サイズ (`UpdateCart.items.size`)                                                 | [Array]                                                      |
| 製品カラー (`UpdateCart.items.color`)                                               | [Array]                                                      |
| 製品画像 (`UpdateCart.items.image`)                                               | [Array]                                                      |
| 製品URL (`UpdateCart.items.product_url`)                                          | [Array]                                                      |
| 製品数量 (`UpdateCart.items.quantity`) (Overrides E-Commerce Product Quantity) | [Array]                                                      |
| 製品タグ (`UpdateCart.items.tags`)                                                 | [Array]                                                      |
| カスタム製品変数名 (`UpdateCart.items.custom`)                               | [Array]                                                      |

#### イベントデータ：PurchaseComplete

| 変数                                                                                   | 説明                                                                      |
|:-------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------|
| 注文ID                                                                                   | (`PurchaseComplete.order_id`) (Overrides E-Commerce Order ID)                     |
| チェックアウトトークン                                                                             | (`PurchaseComplete.checkout_token`)                                               |
| 作成日                                                                                 | (`PurchaseComplete.created_at`)                                                   |
| 注文ステータスURL                                                                           | (`PurchaseComplete.order_status_url`)                                            |
| 通貨                                                                                   | (`PurchaseComplete.currency`) (Overrides E-Commerce Currency)                      |
| 合計価格                                                                                | (`PurchaseComplete.total_price`) (Overrides E-Commerce Order Total)               |
| 小計価格                                                                             | (`PurchaseComplete.subtotal_price`) (Overrides E-Commerce Order Subtotal)         |
| 税金                                                                                  | (`PurchaseComplete.total_tax`) (Overrides E-Commerce Tax Amount)                  |
| 配送料金                                                                             | (`PurchaseComplete.shipping_price`) (Overrides E-Commerce Shipping Amount)        |
| プラットフォーム                                                                                   | (`PurchaseComplete.platform`)                                                      |
| 住所1                                                                                  | (`PurchaseComplete.shipping_address.address1`)                                    |
| 住所2                                                                                  | (`PurchaseComplete.shipping_address.address2`)                                    |
| 名前                                                                                  | (`PurchaseComplete.shipping_address.first_name`)                                 |
| 姓                                                                                  | (`PurchaseComplete.shipping_address.last_name`)                                  |
| フルネーム                                                                                  | (`PurchaseComplete.shipping_address.full_name`)                                  |
| 都市                                                                                       | (`PurchaseComplete.shipping_address.city`) (Overrides E-Commerce Customer City)   |
| 州                                                                                      | (`PurchaseComplete.shipping_address.state`) (Overrides E-Commerce Customer State) |
| 郵便番号                                                                                   | (`PurchaseComplete.shipping_address.zip`) (Overrides E-Commerce Customer Zip)     |
| 電話番号                                                                               | (`PurchaseComplete.shipping_address.phone`)                                       |
| 製品タイトル (`PurchaseComplete.items.title`) (Overrides E-Commerce Product Name)           | [Array]                                                                          |
| 製品価格 (`PurchaseComplete.items.price`) (Overrides E-Commerce Product Unit Price)     | [Array]                                                                          |
| 製品ID (`PurchaseComplete.items.product_id`) (Overrides E-Commerce Product ID)          | [Array]                                                                          |
| バリアントID (`PurchaseComplete.items.variant_id`)                                            | [Array]                                                                          |
| 製品SKU (`PurchaseComplete.items.sku`) (Overrides E-Comemrce Product SKU)                | [Array]                                                                          |
| 製品サイズ (`PurchaseComplete.items.size`)                                                 | [Array]                                                                          |
| 製品カラー (`PurchaseComplete.items.color`)                                               | [Array]                                                                          |
| 製品画像 (`PurchaseComplete.items.image`)                                               | [Array]                                                                          |
| 製品URL (`PurchaseComplete.items.product_url`)                                          | [Array]                                                                          |
| 製品数量 (`PurchaseComplete.items.quantity`) (Overrides E-Commerce Product Quantity) | [Array]                                                                          |
| 製品タグ (`PurchaseComplete.items.tags`)                                                 | [Array]                                                                          |
| カスタム製品変数名 (`PurchaseComplete.items.custom`)                               | [Array]                                                                          |
| 顧客のメールアドレス                                                                             | (`PurchaseComplete.customer_properties.email`)                                    |
| 顧客ID                                                                                | (`PurchaseComplete.customer_properties.id`) (Overrides E-Commerce Customer ID)    |
| 顧客の名前                                                                        | (`PurchaseComplete.customer_properties.first_name`)                              |
| 顧客の姓                                                                         | (`PurchaseComplete.customer_properties.last_name`)                               |

#### 訪問パラメータ

| 変数        | 説明                                               |
|:----------------|:----------------------------------------------------------|
| 顧客ID     | (`visitor.customer_id`) (Overrides E-Commerce Customer ID) |
| 住所1       | (`visitor.address1`)                                        |
| 住所2       | (`visitor.address2`)                                        |
| 名前      | (`visitor.first_name`)                                     |
| 姓       | (`visitor.last_name`)                                      |
| フルネーム       | (`visitor.full_name`)                                      |
| 性別          | (`visitor.gender`)                                          |
| 言語        | (`visitor.language`)                                        |
| 都市            | (`visitor.city`) (Overrides E-Commerce Customer City)       |
| 州           | (`visitor.state`) (Overrides E-Commerce Customer State)     |
| 郵便番号        | (`visitor.zip`) (Overrides E-Commerce Customer Zip)         |
| 電話番号    | (`visitor.phone`)                                           |
| プロフィール写真 | (`visitor.profile_pic`)                                    |
