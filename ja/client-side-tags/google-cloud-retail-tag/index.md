---
title: Google Cloud Retailタグ構成ガイド
description: この記事では、タグ管理アカウントでGoogle Cloud Retailタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cloud-retail-tag/
---
Google Cloud Retail APIは、機械学習モデルに基づいて、パーソナライズされた検索とレコメンデーションを実装するためのソリューションスイートです。リアルタイムのユーザーイベントを記録するには、Google Cloud Retailタグを実装します。Google Cloud Retail APIは、リアルタイムのユーザーイベントを使用してレコメンデーションと検索結果を生成します。

## タグに関するヒント

* データマッピングを使用してイベントトリガーを構成します。
* `tealium_visitor_id`は、マッピングによって上書きされない限り、`visitorId`として渡されます。
* 次のEコマース拡張機能パラメータをサポートしています。
    * 小計
    * 通貨
    * 商品IDのリスト
    * 商品価格のリスト
    * 商品数量のリスト

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **プロジェクト番号**：（必須）Google Cloud Retailのプロジェクト番号。
* **APIキー**：（必須）Google Cloud RetailのAPIキー。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `projectNumber` | 文字列 | プロジェクト番号 |
| `apiKey` | 文字列 | APIキー |
| `locationId` | 文字列 | ロケーションID |
| `catalogId` | 文字列 | カタログID |
| `cartId` | 文字列 | カートID |
| `pageCategories` | 文字列 | ページカテゴリー |
| `searchQuery` | 文字列 | 検索クエリ |
| `completionDetail.completionAttributionToken` | 文字列 | 検索補完トークン |
| `completionDetail.selectedSuggestion` | 文字列 | 検索で選択された候補 |
| `completionDetail.selectedPosition` | 文字列 | 検索で選択された位置 |
| `attributionToken` | 文字列 | アトリビューショントークン |
| `debug` | ブール値 | デバッグ |
| `custom.myvar` | | カスタム |

### ユーザーパラメータ

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `visitorId` | 文字列 | 訪問ID |
| `userInfo.userId` | 文字列 | ユーザーID |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `purchaseTransaction.id`（`_corder`を上書き） | 文字列 | トランザクションID |
| `purchaseTransaction.revenue`（`_csubtotal`を上書き） | 文字列 | 小計 |
| `purchaseTransaction.currencyCode`（`_ccurrency`を上書き） | 文字列 | 通貨コード |
| `productDetails.product.id`（`_cprod`を上書き） | 配列 | 商品IDのリスト |
| `productDetails.product.priceInfo.price`（`_cprice`を上書き） | 配列 | 価格のリスト |
| `productDetails.product.quantity`（`_cquan`を上書き） | 配列 | 数量のリスト |

### 属性

| 変数 | データ型 | 説明 |
|:---------|:------------|:------------|
| `attributes.myvar.text` | 配列 | 属性テキスト |
| `attributes.myvar.numbers` | 配列 | 属性数値 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの追加](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `add-to-cart` | カートに追加 |
| `category-page-view` | カテゴリーページの表示 |
| `detail-page-view` | 商品詳細ページの表示 |
| `home-page-view` | ホームページの表示 |
| `purchase-complete` | 購入 |
| `search` | 検索 |
| `shopping-cart-page-view` | ショッピングカートの表示 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの追加](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `cartId` | 文字列 | カートID |
| `pageCategories` | 文字列 | ページカテゴリー |
| `searchQuery` | 文字列 | 検索クエリ |
| `completionDetail.completionAttributionToken` | 文字列 | 検索補完トークン |
| `completionDetail.selectedSuggestion` | 文字列 | 検索で選択された候補 |
| `completionDetail.selectedPosition` | 文字列 | 検索で選択された位置 |
| `attributionToken` | 文字列 | アトリビューショントークン |
| `visitorId` | 文字列 | 訪問ID |
| `userInfo.userId` | 文字列 | ユーザーID |
| `purchaseTransaction.id` | 文字列 | トランザクションID |
| `purchaseTransaction.cost` | 文字列 | コスト |
| `purchaseTransaction.tax` | 文字列 | 税額 |
| `purchaseTransaction.revenue` | 文字列 | 小計（`_csubtotal`を上書き） |
| `purchaseTransaction.currencyCode` | 文字列 | 通貨コード（`_ccurrency`を上書き） |
| `productDetails.product.id` | 配列 | 商品IDのリスト（`_cprod`を上書き） |
| `productDetails.product.priceInfo.price` | 配列 | 価格のリスト（`_cprice`を上書き） |
| `productDetails.quantity` | 配列 | 数量のリスト（`_cquan`を上書き） |
| `attributes.myvar.text` | 配列 | 属性テキスト |
| `attributes.myvar.numbers` | 配列 | 属性数値 |
| `Custom_Parameter` | | カスタムパラメータ |
| `add-to-cart` | | カートに追加 |
| `category-page-view` | | カテゴリーページの表示 |
| `detail-page-view` | | 商品詳細ページの表示 |
| `home-page-view` | | ホームページの表示 |
| `purchase-complete` | | 購入 |
| `search` | | 検索 |
| `shopping-cart-page-view` | | ショッピングカートの表示 |