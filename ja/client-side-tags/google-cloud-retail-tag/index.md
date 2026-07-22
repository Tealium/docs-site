---
title: Google Cloud Retail タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGoogle Cloud Retailタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cloud-retail-tag/
---
Google Cloud Retail APIは、機械学習モデルに基づいたパーソナライズされた検索と推奨を実装するためのソリューションスイートです。Google Cloud Retailタグを実装して、リアルタイムのユーザーイベントを記録します。Google Cloud Retail APIは、リアルタイムのユーザーイベントを使用して推奨と検索結果を生成します。

## タグのヒント

* データマッピングを使用してイベントトリガーを構成します。
* `tealium_visitor_id`は、マッピングを介して上書きされない限り`visitorId`として渡されます。
* 以下のE-Commerce拡張パラメータをサポートしています：
    * 小計
    * 通貨
    * 商品IDのリスト
    * 商品価格のリスト
    * 商品数量のリスト

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **プロジェクト番号**：必須。Google Cloud Retailプロジェクトの番号。
* **APIキー**：必須。あなたのGoogle Cloud Retail APIキー。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 |  タイプ | 説明 |
|:---------|:------------|:------------|
| `projectNumber`  | 文字列 |プロジェクト番号 |
| `apiKey`  | 文字列 |APIキー |
| `locationId`  | 文字列 |  ロケーションID|
| `catalogId`  | 文字列 |カタログID|
| `cartId`  | 文字列 |カートID |
| `pageCategories`  | 文字列 |ページカテゴリ |
| `searchQuery`  | 文字列 |検索クエリ |
| `completionDetail.completionAttributionToken`  | 文字列 |検索完了トークン |
| `completionDetail.selectedSuggestion`  | 文字列 |選択された検索提案 |
| `completionDetail.selectedPosition`  | 文字列 |選択された検索位置 |
| `attributionToken`  | 文字列 |アトリビューショントークン |
| `debug`  | ブール |デバッグ |
| `custom.myvar` | |カスタム|

### ユーザーパラメータ

| 変数 |  タイプ | 説明|
|:---------|:------------|:------------|
|`visitorId`  | 文字列 | 訪問ID |
|`userInfo.userId`  | 文字列 | ユーザーID |

### E-Commerce

| 変数 |  タイプ | 説明|
|:---------|:------------|:------------|
|`purchaseTransaction.id` (Overrides `_corder`)  | 文字列 | トランザクションID  |
|`purchaseTransaction.revenue` (Overrides `_csubtotal`)  | 文字列 | 小計 |
|`purchaseTransaction.currencyCode` (Overrides `_ccurrency`)  | 文字列 | 通貨コード |
|`productDetails.product.id` (Overrides `_cprod`)  | 配列 | 商品IDのリスト |
|`productDetails.product.priceInfo.price` (Overrides `_cprice`)  | 配列 | 価格のリスト |
|`productDetails.product.quantity` (Overrides `_cquan`)  | 配列 | 数量のリスト |

### 属性

| 変数 | データタイプ | 説明|
|:---------|:------------|:------------|
|`attributes.myvar.text`  | 配列 | 属性テキスト |
|`attributes.myvar.numbers`  | 配列 | 属性数値 |

### イベント

イベントをマップするには、[イベントマッピングの追加](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `add-to-cart`| カートに追加 |
| `category-page-view` | カテゴリページビュー | 
| `detail-page-view` | 商品詳細ページビュー  | 
| `home-page-view` | ホームページビュー | 
| `purchase-complete` | 購入 | 
| `search` |検索 | 
| `shopping-cart-page-view` | ショッピングカートビュー | 

### イベント固有のパラメータ

イベントをマップするには、[イベントマッピングの追加](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | タイプ | 説明|
|:---------|:------------|:------------|
| `cartId` |  文字列 | カートID|
| `pageCategories` |文字列 | ページカテゴリ|
| `searchQuery` |文字列 | 検索クエリ|
| `completionDetail.completionAttributionToken` |文字列 | 検索完了トークン  |
| `completionDetail.selectedSuggestion` |文字列| 選択された検索提案  |
| `completionDetail.selectedPosition` |文字列| 選択された検索位置  |
| `attributionToken` |文字列 | アトリビューショントークン |
| `visitorId` |文字列| 訪問ID  |
| `userInfo.userId` |文字列| ユーザーID|
| `purchaseTransaction.id` | 文字列 | トランザクションID |
| `purchaseTransaction.cost` | 文字列 | コスト |
| `purchaseTransaction.tax` | 文字列 | 税金 |
| `purchaseTransaction.revenue` |文字列| 小計 (Overrides `_csubtotal`)  |
| `purchaseTransaction.currencyCode` |文字列| 通貨コード  (Overrides `_ccurrency`) |
| `productDetails.product.id` |配列| 商品IDのリスト (Overrides `_cprod`) |
| `productDetails.product.priceInfo.price` |配列| 価格のリスト  (Overrides `_cprice`) |
| `productDetails.quantity` |配列| 数量のリスト (Overrides `_cquan`) |
| `attributes.myvar.text` |配列| 属性テキスト |
| `attributes.myvar.numbers` |配列| 属性数値 |
| `Custom_Parameter` | |カスタムパラメータ|
| `add-to-cart` | | カートに追加 |
| `category-page-view` | | カテゴリページビュー| 
| `detail-page-view`| | 商品詳細ページビュー  | 
| `home-page-view`| |ホームページビュー | 
| `purchase-complete`| | 購入  | 
| `search` | | 検索  | 
| `shopping-cart-page-view` | |ショッピングカートビュー  | 



