---
title: セッションAIタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでセッションAIタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/session-ai-tag/
---
TealiumのセッションAIタグは、ウェブサイトとセッションAIプラットフォームの統合を簡素化します。具体的には、セッションAI SDKの注入と初期化、訪問イベントの収集と送信、サインインユーザーの顧客識別子の構成を容易にします。

セッションAIタグに関する追加情報については、[Session AI Tealium Tag](https://devguide.zineone.com/docs/tealium) と [Ecommerce Event Schema](https://devguide.zineone.com/docs/ecommerce-event-schema-1) を参照してください。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を構成します：

* **アクセストークン**: セッションAIサーバーサイドツールによって生成されたアクセストークン。
* **ウィジェットコンテナの注入**: このウィジェットコンテナは、セッションAIによってトリガーされるユーザーエクスペリエンスコンテンツのレンダリングに使用されます。
* **公開場所**: 公開環境を選択し、これらの環境に対してAPIキーが有効であることを確認します。
* **バンドルフラグ**: ページパフォーマンスを最適化するために **ON** に構成します。
* **詳細構成**: 以下の構成についてはデフォルト値の使用を推奨します：
    * **送信フラグ**: セッションAIへのイベント送信を決定します。デフォルト値は **ON** です。
    * **タグタイミング**: タグを発火するタイミングを決定します。デフォルトは **DOM Ready** です。**DOM Ready** を選択すると、ページのレンダリングへの影響が最小限に抑えられます。
    * **同期ロードタイプ**: タグを同期的にロードするかどうかを決定します。デフォルトは **OFF** です。

## ロードルール

セッションAIは、適切なデータ収集と訪問のインタラクションのために、セッションAI SDKおよびタグのロードルールを**すべてのページとイベント**（デフォルト）に構成することを推奨します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | データタイプ | 説明 |
|---|---|---|
| `customerId`  | 文字列 |顧客ID（`_ccustid`を上書き） |
| `logged_in` | ブール | ログイン状態。 &lt;br&gt; 利用可能な値は **Y** または **N** です。 |

### E-コマース

E-コマースパラメータについての詳細は、セッションAIのドキュメント内の [Ecommerce Event Schema](https://devguide.zineone.com/docs/ecommerce-event-schema-1) を参照してください。

| 変数 | データタイプ | 説明 |
|---|---|---|
|  `category` | 文字列 |  カテゴリ|
| `product_id` | 文字列 | 商品ID |
|  `sku` | 文字列 |SKU  |
| `search_term` | 文字列 | 検索語  |
| `result_count` | 数値 | 結果数  |
|  `name` | 文字列 | 名前 |
|  `price` | 数値 | 価格 |
| `list_price` | 数値 | 定価 |
| `order_id`  | 文字列 |注文ID（`_corder`を上書き） |
| `order_total`  | 数値 | 注文合計（`_ctotal`を上書き） |
|  `discount` | 数値 | 割引 |
|  `currency` | 文字列 | 通貨 |
|  `taxes`  | 数値 | 税金（`_ctax`を上書き） |
|  `shipping` | 数値 | 配送料（`_cship`を上書き）  |
|  `item_total` | 数値 |商品合計  |
|  `filter` | 文字列 | フィルター |
| `sort_field` | 文字列 | ソートフィールド  |
|  `sort_order` | 文字列 | ソート順 |
| `coupons.code` | 配列 | クーポンコード（`_cpromo`を上書き）  |
| `coupons.value` | 配列 | クーポン値  |
| `coupons.currency` | 配列 | クーポン通貨  |
|  `coupons.type` | 配列 | クーポンタイプ |
| `coupons.threshold` | 配列 | クーポン閾値  |
| `coupons.method` | 配列 |  クーポン方法 |
| `referrer_id` | 文字列 | 紹介ID |
|  `items.quantity` | 配列 |商品数量（`_cquan`を上書き）  |
|  `items.price`  | 配列 | 商品価格（`_cprice`を上書き）|
| `items.list_price` | 配列 |商品定価   |
|  `items.sku`  | 配列 |商品SKU（`_csku`を上書き） |
|  `items.name`  | 配列 |  (オプション) 商品名（`_cprodname`を上書き）|
|  `items.productId`  | 配列 | 商品ID（`_cprod`を上書き）|
| `items.category` | 配列 | (オプション) 商品カテゴリ（`_ccat`を上書き） |
|  `items.currency`  | 配列 | (オプション) 商品通貨（`_ccurrency`を上書き）|
|  `items.item_coupon.code` | 配列 |(オプション) 商品クーポンコード  |
|  `items.item_coupon.value` | 配列 | (オプション) 商品クーポン値 |
| `items.item_coupon.currency` | 配列 |(オプション) 商品クーポン通貨   |
|  `items.item_coupon.type` | 配列 | (オプション) 商品クーポンタイプ |
|  `items.item_coupon.threshold` | 配列 | (オプション) 商品クーポン閾値 |
|  `items.item_coupon.method` | 配列 |(オプション) 商品クーポン方法  |
| `updated_items.quantity` | 配列 | 更新された商品数量（`_cquan`を上書き） |
| `updated_items.price` | 配列 | 更新された商品価格（`_cprice`を上書き） |
| `updated_items.list_price` | 配列 | 更新された商品定価 |
| `updated_items.sku` | 配列 | 更新された商品SKU（`_csku`を上書き） |
| `updated_items.name` | 配列 | 更新された商品名（`_cprodname`を上書き） |
| `updated_items.productId` | 配列 | 更新された商品ID（`_cprod`を上書き） |
| `updated_items.category` | 配列 | 更新された商品カテゴリ（`_ccat`を上書き） |
| `updated_items.currency` | 配列 | 更新された商品通貨（`_ccurrency`を上書き） |
| `updated_items.item_coupon.code` | 配列 | 更新された商品クーポンコード |
| `updated_items.item_coupon.value` | 配列 | 更新された商品値 |
| `updated_items.item_coupon.currency` | 配列 | 更新された商品通貨 |
| `updated_items.item_coupon.type` | 配列 | 更新された商品タイプ |
| `updated_items.item_coupon.threshold` | 配列 | 更新された商品閾値 |
| `updated_items.item_coupon.method` | 配列 | 更新された商品方法 |

### 初期化

| 変数 | データタイプ | 説明 |
|:---|:---| :---|
| `email`  | 文字列 | ユニークなメールアドレス |
|`phone`  | 文字列 | ユニークな電話番号 |
| `fb`  | 文字列 |  Facebook ID|

### イベントトリガー
イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|---|---|
| `view_home` | ホームを表示 |
| `view_category` | カテゴリを表示 |
| `view_product` | 商品を表示 |
| `update_cart` | カートを更新 |
| `search` | 検索 |
| `apply_filter` | フィルターを適用 |
| `select_sku` | SKUを選択 |
| `view_cart` | カートを表示 |
| `add_to_cart` | カートに追加 |
| `begin_checkout` | チェックアウトを開始 |
| `add_shipping_info` | 配送情報を追加 |
| `add_payment_info` | 支払情報を追加 |
| `purchase` | 購入 |
| `user_login` | ユーザーログイン |
| `user_logout` | ユーザーログアウト |
| `user_register` | ユーザー登録 |
| `add_wishlist` | お気に入りリストに追加 |
| `view_wishlist` | お気に入りリストを表示 |
| `update_wishlist` | お気に入りリストを更新 |
| `view_review` | レビューを表示 |
| `add_review` | レビューを追加 |
| `view_product_question` | 商品の質問を表示 |
| `add_product_question` | 商品の質問を追加 |
| `view_landingpage` | ランディングページを表示 |
| `view_faq` | FAQを表示 |
| `set_storelocation` | 店舗の場所を構成 |
| `setCustomerId` | 顧客IDを構成 |
| `addCustomerInfo` | 顧客情報を追加 |
| `registerWidget` | ウィジェットを登録 |
| `Custom` | カスタム |
### イベント固有のパラメータ
イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | データタイプ | 説明 |
|:---------|:----------|:------------|
| `email`  | 文字列 | ユニークなメールアドレス |
|`phone`  | 文字列 | ユニークな電話番号 |
| `fb`  | 文字列 | Facebook ID |
| `logged_in` | ブール値 | ログイン状態。&lt;br&gt; 利用可能な値は **Y** または **N**。 |
| `category` | 文字列 | カテゴリ |
| `product_id` | 文字列 | 商品ID |
| `sku` | 文字列 | SKU |
| `search_term` | 文字列 | 検索語 |
| `result_count` | 数値 | 結果数 |
| `name` | 文字列 | 名前 |
| `price` | 数値 | 価格 |
| `list_price` | 数値 | 定価 |
| `order_id` | 文字列 | 注文ID |
| `order_total` | 数値 | 注文合計 |
| `discount` | 数値 | 割引 |
| `currency` | 文字列 | 通貨 |
| `taxes` | 数値 | 税金 |
| `shipping` | 数値 | 配送料 |
| `item_total` | 数値 | 商品合計 |
| `filter` | JSONオブジェクト | (オプション) フィルター |
| `sort_field` | 文字列 | (オプション) ソートフィールド |
| `sort_order` | 文字列 | (オプション) ソート順 |
| `coupons.code` | 配列 | (オプション) クーポンコード（`_cpromo`を上書き） |
| `coupons.value` | 配列 | (オプション) クーポン値 |
| `coupons.currency` | 配列 | (オプション) クーポン通貨 |
| `coupons.type` | 配列 | (オプション) クーポンタイプ |
| `coupons.threshold` | 配列 | (オプション) クーポン閾値 |
| `coupons.method` | 配列 | (オプション) クーポン方法 |
| `referrer_id` | 文字列 | 紹介者ID |
| `items.quantity` | 配列 | 商品数量（`_cquan`を上書き） |
| `items.price` | 配列 | 商品価格（`_cprice`を上書き） |
| `items.list_price` | 配列 | 商品定価 |
| `items.sku` | 配列 | 商品SKU（`_csku`を上書き） |
| `items.name` | 配列 | 商品名（`_cprodname`を上書き） |
| `items.productId` | 配列 | 商品ID（`_cprod`を上書き） |
| `items.category` | 配列 | 商品カテゴリ（`_ccat`を上書き） |
| `items.currency` | 配列 | 商品通貨（`_ccurrency`を上書き） |
| `items.item_coupon.code` | 配列 | 商品クーポンコード |
| `items.item_coupon.value` | 配列 | 商品クーポン値 |
| `items.item_coupon.currency` | 配列 | 商品クーポン通貨 |
| `items.item_coupon.type` | 配列 | 商品クーポンタイプ |
| `items.item_coupon.threshold` | 配列 | 商品クーポン閾値 |
| `items.item_coupon.method` | 配列 | 商品クーポン方法 |
| `updated_items.quantity` | 配列 | 更新された商品数量（`_cquan`を上書き） |
| `updated_items.price` | 配列 | 更新された商品価格（`_cprice`を上書き） |
| `updated_items.list_price` | 配列 | 更新された商品定価 |
| `updated_items.sku` | 配列 | 更新された商品SKU（`_csku`を上書き） |
| `updated_items.name` | 配列 | 更新された商品名（`_cprodname`を上書き） |
| `updated_items.productId` | 配列 | 更新された商品ID（`_cprod`を上書き） |
| `updated_items.category` | 配列 | 更新された商品カテゴリ（`_ccat`を上書き） |
| `updated_items.currency` | 配列 | 更新された商品通貨（`_ccurrency`を上書き） |
| `updated_items.item_coupon.code` | 配列 | 更新された商品クーポンコード |
| `updated_items.item_coupon.value` | 配列 | 更新された商品値 |
| `updated_items.item_coupon.currency` | 配列 | 更新された商品通貨 |
| `updated_items.item_coupon.type` | 配列 | 更新された商品タイプ |
| `updated_items.item_coupon.threshold` | 配列 | 更新された商品閾値 |
| `updated_items.item_coupon.method` | 配列 | 更新された商品方法 |
| `customerId` | 文字列 | 顧客ID |
| `attrName` | 文字列 | 属性名 |
| `attrValue` | 文字列 | 属性値 |
| `Custom_Parameter` | イベント | カスタムパラメータ |
| `onitialize` | イベント | 初期化 |
| `view_home` | イベント | ホーム表示 |
| `view_category` | イベント | カテゴリ表示 |
| `view_product` | イベント | 商品表示 |
| `update_cart` | イベント | カート更新 |
| `search` | イベント | 検索 |
| `apply_filter` | イベント | フィルタ適用 |
| `select_sku` | イベント | SKU選択 |
| `view_cart` | イベント | カート表示 |
| `add_to_cart` | イベント | カートに追加 |
| `begin_checkout` | イベント | チェックアウト開始 |
| `add_shipping_info` | イベント | 配送情報追加 |
| `add_payment_info` | イベント | 支払情報追加 |
| `purchase` | イベント | 購入 |
| `user_login` | イベント | ユーザーログイン |
| `user_logout` | イベント | ユーザーログアウト |
| `user_register` | イベント | ユーザー登録 |
| `add_wishlist` | イベント | ほしい物リストに追加 |
| `view_wishlist` | イベント | ほしい物リスト表示 |
| `update_wishlist` | イベント | ほしい物リスト更新 |
| `view_review` | イベント | レビュー表示 |
| `add_review` | イベント | レビュー追加 |
| `view_product_question` | イベント | 商品質問表示 |
| `add_product_question` | イベント | 商品質問追加 |
| `view_landingpage` | イベント | ランディングページ表示 |
| `view_faq` | イベント | FAQ表示 |
| `set_storelocation` | イベント | 店舗位置構成 |
| `setCustomerId` | イベント | 顧客ID構成 |
| `addCustomerInfo` | イベント | 顧客情報追加 |
| `Custom_Event` | イベント | カスタムイベント |
