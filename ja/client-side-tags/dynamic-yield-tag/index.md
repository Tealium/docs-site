---
title: Dynamic Yieldタグ構成ガイド
description: この記事では、Dynamic Yieldタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dynamic-yield-tag/
--- 
## タグに関するヒント

* 名前とプロパティを構成できます。
* マッピングツールボックスの［カスタムイベントデータ］タブで、カスタムイベントのパラメータをマッピングします。
* 注文IDが構成されると、コンバージョンが発生します。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 注文合計（`_ctotal`）
  * 小計（`_csubtotal`）
  * 通貨（`_ccurrency`）
  * 商品IDのリスト（`_cprod`）
  * 商品名のリスト（`_cprodname`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）
* 商品リストに複数の商品が含まれている場合、AddToCartとRemoveFromCartには変更対象の商品が必要です。［パラメータ］タブで商品ID（`productId`）にマッピングしてください。マッピングしない場合、イベントは送信されません。
* ハッシュ化されたメールアドレスの値は、SHA-256ハッシュである必要があります。タグはこの値を、タイプが`he`の顧客IDとしてDynamic Yieldに送信します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **サイトID**：Dynamic Yieldから提供されたサイトID、またはサイトID（`scsec`）。
* **Dynamic Yieldデータセンター**：使用するDynamic Yieldデータセンターを選択します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|   `scsec` | 文字列 | サイトID | 
|   `cdn` | 文字列 | 使用するDynamic Yieldデータセンター | 
|  `evt_list`  | [CSV/配列] | 発生させるイベントのリスト | 
|   `context.type` | 文字列 | コンテキストタイプ | 
|  `context.data`  | 配列 | コンテキストデータ | 
|  `context.lng`  | 文字列 | コンテキストの言語（例：`en_GB`） | 
|  `spa_mode`  | 文字列 | ページ読み込みまたはSPAイベントの検出を使用するDynamic Yieldセクションの場合にのみ、`legacy`に構成します | 

### Eコマース

| 変数             | タイプ | 説明 |
|:-----------|:------------------------------------|:------------------------------------|
| `order_id`    | 文字列 | 注文ID（`_corder`を上書き） | 
| `order_total`  | 数値 | 注文合計（`_ctotal`を上書き） |
| `order_subtotal`     | 数値 | 小計（`_csubtotal`を上書き） |
| `order_currency`     | 文字列 | 通貨（`_ccurrency`を上書き） |                       
| `product_id`         | 配列 | 商品IDのリスト（`_cprod`を上書き） |
| `product_name`       | 配列 | 商品名のリスト（`_cprodname`を上書き） |
| `product_quantity`   | 配列 | 数量のリスト（`_cquan`を上書き） |
| `product_unit_price` | 配列 | 価格のリスト（`_cprice`を上書き） |

### イベント

| 変数         | 説明    |
|:-----------------|:---------------|
| `AddToCart`      | カートへの追加 |
| `RemoveFromCart` | カートからの削除 |
| `Search`         | 検索 |
| `EmailSignup`    | メール登録 |
| `VideoWatch`     | 動画視聴 |
| `SyncCart`       | カートの同期 |
| `AddToWishlist`  | ウィッシュリストへの追加 |
| `PromoCode`      | プロモーションコード |
| `ChangeAttribute` | 属性の変更 |
| `FilterItems`    | アイテムの絞り込み |
| `SortItems`      | アイテムの並べ替え |
| `Login`          | ログイン |
| `Signup`         | 登録 |
| `IdentifyUser`   | ユーザーの識別 |
| `Custom`         | カスタム |

### パラメータ

| 変数                     | 説明              |
|:-----------------------------|:-------------------------|
| サイズ（`size`）                | `properties.size`        |
| 検索キーワード（`keywords`） | `properties.keywords`    |
| 検索キーワード（`searchKeywords`） | `properties.searchKeywords` |
| ハッシュ化されたメールアドレス（`hashedEmail`） | `properties.hashedEmail` |
| 顧客ID（`cuid`） | `properties.cuid` |
| 顧客IDタイプ（`cuidType`） | `properties.cuidType` |
| セカンダリ識別子（`secondaryIdentifiers`）［配列］ | `properties.secondaryIdentifiers` |
| 商品ID（`productId`） | `properties.productId` |
| 数量（`quantity`） | `properties.quantity` |
| 商品価格（`itemPrice`） | `properties.itemPrice` |
| 値（`value`） | `properties.value` |
| 通貨（`currency`） | `properties.currency` |
| トランザクションID（`uniqueTransactionId`） | `properties.uniqueTransactionId` |
| プロモーションコード（`code`） | `properties.code` |
| 属性タイプ（`attributeType`） | `properties.attributeType` |
| 属性値（`attributeValue`） | `properties.attributeValue` |
| フィルタータイプ（`filterType`） | `properties.filterType` |
| フィルターの数値（`filterNumericValue`） | `properties.filterNumericValue` |
| フィルターの文字列値（`filterStringValue`） | `properties.filterStringValue` |
| 並べ替え基準（`sortBy`） | `properties.sortBy` |
| 並べ替え順序（`sortOrder`）［`ASC`/`DESC`］ | `properties.sortOrder` |
| カスタム                       | カスタム                   |

### 動画パラメータ

| 変数                               | 説明                  |
|:---------------------------------------|:-----------------------------|
| アイテムID                                | `properties.itemId`          |
| カテゴリー（`categories`）              | `properties.categories`      |
| 自動再生（`autoplay`）［`true`/`false`］ | `properties.autoplay`        |
| 進捗（`progress`）                  | `properties.progress`        |
| 進捗率（`progressPercent`）   | `properties.progressPercent` |
| カスタム                                 | カスタム                       |
