---
title: Session AIタグ構成ガイド
description: この記事では、タグ管理アカウントでSession AIタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/session-ai-tag/
---
Session AI用のTealiumタグを使用すると、WebサイトとSession AIプラットフォームを簡単に統合できます。具体的には、Session AI SDKの挿入と初期化、訪問イベントの収集と送信、ログイン済みユーザーに対する顧客識別子の構成が可能になります。

Session AIタグの詳細については、Session AIのドキュメントにある[Session AI Tealiumタグ](https://devguide.zineone.com/docs/tealium)および[Eコマースイベントスキーマ](https://devguide.zineone.com/docs/ecommerce-event-schema-1)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **アクセストークン**：Session AIのサーバーサイドツールによって生成されたアクセストークン。
* **ウィジェットコンテナを挿入**：このウィジェットコンテナは、Session AIによってトリガーされるユーザーエクスペリエンスコンテンツのレンダリングに使用されます。
* **パブリッシュ先**：パブリッシュ環境を選択し、APIキーがそれらの環境で有効であることを確認します。
* **バンドルフラグ**：ページパフォーマンスを最適化するには、**オン**に構成します。
* **詳細構成**：次の構成にはデフォルト値を使用することを推奨します。
    * **送信フラグ**：イベントをSession AIに送信するかどうかを指定します。デフォルト値は**オン**です。
    * **タグのタイミング**：タグを実行するタイミングを指定します。デフォルトは**DOM Ready**です。**DOM Ready**を選択すると、ページのレンダリングへの影響を最小限に抑えられます。
    * **同期読み込みタイプ**：タグを同期的に読み込むかどうかを指定します。デフォルトは**オフ**です。

## ロードルール

データを適切に収集し、訪問とのインタラクションを実現するため、Session AIでは、Session AI SDKおよびタグのロードルールを**すべてのページとイベント**（デフォルト）に構成することを推奨しています。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | データ型 | 説明 |
|---|---|---|
| `customerId` | 文字列 | 顧客ID（`_ccustid`を上書き） |
| `logged_in` | ブール値 | ログイン状態。<br>使用可能な値は**Y**または**N**です。 |

### Eコマース

Eコマースパラメータの詳細については、Session AIドキュメントの[Eコマースイベントスキーマ](https://devguide.zineone.com/docs/ecommerce-event-schema-1)を参照してください。

| 変数 | データ型 | 説明 |
|---|---|---|
| `category` | 文字列 | カテゴリー |
| `product_id` | 文字列 | 商品ID |
| `sku` | 文字列 | SKU |
| `search_term` | 文字列 | 検索語句 |
| `result_count` | 数値 | 検索結果数 |
| `name` | 文字列 | 名前 |
| `price` | 数値 | 価格 |
| `list_price` | 数値 | 定価 |
| `order_id` | 文字列 | 注文ID（`_corder`を上書き） |
| `order_total` | 数値 | 注文合計（`_ctotal`を上書き） |
| `discount` | 数値 | 割引額 |
| `currency` | 文字列 | 通貨 |
| `taxes` | 数値 | 税額（`_ctax`を上書き） |
| `shipping` | 数値 | 送料（`_cship`を上書き） |
| `item_total` | 数値 | 商品合計 |
| `filter` | 文字列 | フィルター |
| `sort_field` | 文字列 | 並べ替えフィールド |
| `sort_order` | 文字列 | 並べ替え順序 |
| `coupons.code` | 配列 | クーポンコード（`_cpromo`を上書き） |
| `coupons.value` | 配列 | クーポンの値 |
| `coupons.currency` | 配列 | クーポンの通貨 |
| `coupons.type` | 配列 | クーポンの種類 |
| `coupons.threshold` | 配列 | クーポンのしきい値 |
| `coupons.method` | 配列 | クーポンの適用方法 |
| `referrer_id` | 文字列 | 参照元ID |
| `items.quantity` | 配列 | 商品の数量（`_cquan`を上書き） |
| `items.price` | 配列 | 商品の価格（`_cprice`を上書き） |
| `items.list_price` | 配列 | 商品の定価 |
| `items.sku` | 配列 | 商品のSKU（`_csku`を上書き） |
| `items.name` | 配列 | （任意）商品の名前（`_cprodname`を上書き） |
| `items.productId` | 配列 | 商品の商品ID（`_cprod`を上書き） |
| `items.category` | 配列 | （任意）商品のカテゴリー（`_ccat`を上書き） |
| `items.currency` | 配列 | （任意）商品の通貨（`_ccurrency`を上書き） |
| `items.item_coupon.code` | 配列 | （任意）商品のクーポンコード |
| `items.item_coupon.value` | 配列 | （任意）商品のクーポン値 |
| `items.item_coupon.currency` | 配列 | （任意）商品のクーポン通貨 |
| `items.item_coupon.type` | 配列 | （任意）商品のクーポン種類 |
| `items.item_coupon.threshold` | 配列 | （任意）商品のクーポンしきい値 |
| `items.item_coupon.method` | 配列 | （任意）商品のクーポン適用方法 |
| `updated_items.quantity` | 配列 | 更新された商品の数量（`_cquan`を上書き） |
| `updated_items.price` | 配列 | 更新された商品の価格（`_cprice`を上書き） |
| `updated_items.list_price` | 配列 | 更新された商品の定価 |
| `updated_items.sku` | 配列 | 更新された商品のSKU（`_csku`を上書き） |
| `updated_items.name` | 配列 | 更新された商品の名前（`_cprodname`を上書き） |
| `updated_items.productId` | 配列 | 更新された商品の商品ID（`_cprod`を上書き） |
| `updated_items.category` | 配列 | 更新された商品のカテゴリー（`_ccat`を上書き） |
| `updated_items.currency` | 配列 | 更新された商品の通貨（`_ccurrency`を上書き） |
| `updated_items.item_coupon.code` | 配列 | 更新された商品のクーポンコード |
| `updated_items.item_coupon.value` | 配列 | 更新された商品のクーポン値 |
| `updated_items.item_coupon.currency` | 配列 | 更新された商品のクーポン通貨 |
| `updated_items.item_coupon.type` | 配列 | 更新された商品のクーポン種類 |
| `updated_items.item_coupon.threshold` | 配列 | 更新された商品のクーポンしきい値 |
| `updated_items.item_coupon.method` | 配列 | 更新された商品のクーポン適用方法 |

### 初期化

| 変数 | データ型 | 説明 |
|:---|:---|:---|
| `email` | 文字列 | 一意のメールアドレス |
| `phone` | 文字列 | 一意の電話番号 |
| `fb` | 文字列 | Facebook ID |

### イベントトリガー

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|---|---|
| `view_home` | ホームを表示 |
| `view_category` | カテゴリーを表示 |
| `view_product` | 商品を表示 |
| `update_cart` | カートを更新 |
| `search` | 検索 |
| `apply_filter` | フィルターを適用 |
| `select_sku` | SKUを選択 |
| `view_cart` | カートを表示 |
| `add_to_cart` | カートに追加 |
| `begin_checkout` | チェックアウトを開始 |
| `add_shipping_info` | 配送情報を追加 |
| `add_payment_info` | 支払い情報を追加 |
| `purchase` | 購入 |
| `user_login` | ユーザーログイン |
| `user_logout` | ユーザーログアウト |
| `user_register` | ユーザー登録 |
| `add_wishlist` | ウィッシュリストに追加 |
| `view_wishlist` | ウィッシュリストを表示 |
| `update_wishlist` | ウィッシュリストを更新 |
| `view_review` | レビューを表示 |
| `add_review` | レビューを追加 |
| `view_product_question` | 商品に関する質問を表示 |
| `add_product_question` | 商品に関する質問を追加 |
| `view_landingpage` | ランディングページを表示 |
| `view_faq` | FAQを表示 |
| `set_storelocation` | 店舗の場所を構成 |
| `setCustomerId` | 顧客IDを構成 |
| `addCustomerInfo` | 顧客情報を追加 |
| `registerWidget` | ウィジェットを登録 |
| `Custom` | カスタム |
### イベント固有のパラメータ
イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | データ型 | 説明 |
|:---------|:----------|:------------|
| `email`  | 文字列 | 一意のメールアドレス |
| `phone`  | 文字列 | 一意の電話番号 |
| `fb`  | 文字列 | Facebook ID |
| `logged_in` | ブール値 | ログイン状態。<br>使用可能な値は **Y** または **N** です。 |
| `category` | 文字列 | カテゴリ |
| `product_id` | 文字列 | 商品ID |
| `sku` | 文字列 | SKU |
| `search_term` | 文字列 | 検索語句 |
| `result_count` | 数値 | 結果件数 |
| `name` | 文字列 | 名前 |
| `price` | 数値 | 価格 |
| `list_price` | 数値 | 定価 |
| `order_id` | 文字列 | 注文ID |
| `order_total` | 数値 | 注文合計 |
| `discount` | 数値 | 割引 |
| `currency` | 文字列 | 通貨 |
| `taxes` | 数値 | 税金 |
| `shipping` | 数値 | 送料 |
| `item_total` | 数値 | 商品合計 |
| `filter` | JSONオブジェクト | （任意）フィルター |
| `sort_field` | 文字列 | （任意）並べ替えフィールド |
| `sort_order` | 文字列 | （任意）並べ替え順序 |
| `coupons.code` | 配列 | （任意）クーポンコード（`_cpromo`を上書き） |
| `coupons.value` | 配列 | （任意）クーポンの値 |
| `coupons.currency` | 配列 | （任意）クーポンの通貨 |
| `coupons.type` | 配列 | （任意）クーポンの種類 |
| `coupons.threshold` | 配列 | （任意）クーポンのしきい値 |
| `coupons.method` | 配列 | （任意）クーポンの方式 |
| `referrer_id` | 文字列 | 参照元ID |
| `items.quantity` | 配列 | 商品の数量（`_cquan`を上書き） |
| `items.price` | 配列 | 商品の価格（`_cprice`を上書き） |
| `items.list_price` | 配列 | 商品の定価 |
| `items.sku` | 配列 | 商品のSKU（`_csku`を上書き） |
| `items.name` | 配列 | 商品名（`_cprodname`を上書き） |
| `items.productId` | 配列 | 商品ID（`_cprod`を上書き） |
| `items.category` | 配列 | 商品カテゴリ（`_ccat`を上書き） |
| `items.currency` | 配列 | 商品の通貨（`_ccurrency`を上書き） |
|| `items.item_coupon.code` | 配列 | 商品クーポンコード |
| `items.item_coupon.value` | 配列 | 商品クーポンの値 |
| `items.item_coupon.currency` | 配列 | 商品クーポンの通貨 |
| `items.item_coupon.type` | 配列 | 商品クーポンの種類 |
| `items.item_coupon.threshold` | 配列 | 商品クーポンのしきい値 |
| `items.item_coupon.method` | 配列 | 商品クーポンの方式 |
| `updated_items.quantity` | 配列 | 更新された商品の数量（`_cquan`を上書き） |
| `updated_items.price` | 配列 | 更新された商品の価格（`_cprice`を上書き） |
| `updated_items.list_price` | 配列 | 更新された商品の定価 |
| `updated_items.sku` | 配列 | 更新された商品のSKU（`_csku`を上書き） |
| `updated_items.name` | 配列 | 更新された商品名（`_cprodname`を上書き） |
| `updated_items.productId` | 配列 | 更新された商品のID（`_cprod`を上書き） |
| `updated_items.category` | 配列 | 更新された商品のカテゴリ（`_ccat`を上書き） |
| `updated_items.currency` | 配列 | 更新された商品の通貨（`_ccurrency`を上書き） |
| `updated_items.item_coupon.code` | 配列 | 更新された商品のクーポンコード |
| `updated_items.item_coupon.value` | 配列 | 更新された商品の値 |
| `updated_items.item_coupon.currency` | 配列 | 更新された商品の通貨 |
| `updated_items.item_coupon.type` | 配列 | 更新された商品の種類 |
| `updated_items.item_coupon.threshold` | 配列 | 更新された商品のしきい値 |
| `updated_items.item_coupon.method` | 配列 | 更新された商品の方式 |
| `customerId` | 文字列 | 顧客ID |
| `attrName` | 文字列 | 属性名 |
| `attrValue` | 文字列 | 属性値 |
| `Custom_Parameter` | イベント | カスタムパラメータ |
| `onitialize` | イベント | 初期化 |
| `view_home` | イベント | ホームを表示 |
| `view_category` | イベント | カテゴリを表示 |
| `view_product` | イベント | 商品を表示 |
| `update_cart` | イベント | カートを更新 |
| `search` | イベント | 検索 |
| `apply_filter` | イベント | フィルターを適用 |
| `select_sku` | イベント | SKUを選択 |
| `view_cart` | イベント | カートを表示 |
| `add_to_cart` | イベント | カートに追加 |
| `begin_checkout` | イベント | チェックアウトを開始 |
| `add_shipping_info` | イベント | 配送情報を追加 |
| `add_payment_info` | イベント | 支払い情報を追加 |
| `purchase` | イベント | 購入 |
| `user_login` | イベント | ユーザーログイン |
| `user_logout` | イベント | ユーザーログアウト |
| `user_register` | イベント | ユーザー登録 |
| `add_wishlist` | イベント | ウィッシュリストに追加 |
| `view_wishlist` | イベント | ウィッシュリストを表示 |
| `update_wishlist` | イベント | ウィッシュリストを更新 |
| `view_review` | イベント | レビューを表示 |
| `add_review` | イベント | レビューを追加 |
| `view_product_question` | イベント | 商品に関する質問を表示 |
| `add_product_question` | イベント | 商品に関する質問を追加 |
| `view_landingpage` | イベント | ランディングページを表示 |
| `view_faq` | イベント | FAQを表示 |
| `set_storelocation` | イベント | 店舗所在地を構成 |
| `setCustomerId` | イベント | 顧客IDを構成 |
| `addCustomerInfo` | イベント | 顧客情報を追加 |
| `Custom_Event` | イベント | カスタムイベント |