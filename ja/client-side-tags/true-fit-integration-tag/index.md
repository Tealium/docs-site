---
title: True Fit Integrationタグ構成ガイド
description: この記事では、タグ管理アカウントでTrue Fit Integrationタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/true-fit-integration-tag/
---
この記事では、True Fit Integrationタグを構成する方法について説明します。

## タグに関するヒント

* ご質問は、`support@truefit.com`までメールでお問い合わせください。
* PDP連携：https://techdocs.truefitcorp.com/docs/product-detail-page-integration
* 注文確認連携：https://techdocs.truefitcorp.com/docs/order-confirmation-integration
* このタグにはjQueryが必要であり、最近のバージョンのjQueryとは互換性がない場合があります。
* このタグでは、カスタムコールバック関数またはページ上のdivが必要になる場合があります。
* 注文トラッキングでは、値を**registered**、**userid**、および**orderid**にマッピングします。
* マッピングを使用して、次の操作を行います。
  * イベントトリガーを構成する
  * 標準構成値を動的に上書きする
  * Eコマース拡張機能の値を動的に上書きする

* このタグは、次のEコマース拡張機能パラメータをサポートしています。
  * 注文ID
  * ユーザーID
  * 製品ID
  * 製品IDのリスト
  * 単価のリスト
  * 数量のリスト

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **ストアキー**：ストアを表す3文字の略語です。サポートが必要な場合は、True Fitのプロジェクトマネージャーにお問い合わせください。
* **環境**：ステージング環境および開発環境ではこの値を`staging`に構成し、本番環境では`prod`に構成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 構成

| 変数 | 説明 |
|:---------|:------------|
| ストアキー `storeKey`  | 文字列 |
| 環境 `environment`  | 文字列 |

### 標準

| 変数 | 説明 |
|:---------|:------------|
| ロケール `locale`  | 文字列 |
| 製品サイズ `size`  | ［文字列の配列］ |
| 製品の通貨 `currency`  | ［文字列の配列］ |
| カラーID `colorId`  | ［文字列の配列］ |
| 販売グループ `salesGroup`  | ［文字列の配列］ |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| 注文ID `orderId`（`_corder`を上書き） | 文字列 |
| ユーザーID `userId`（`_ccustid`を上書き） | 文字列 |
| 製品ID `productId`（`_cprod`を上書き） | ［文字列の配列］ |
| 製品数量 `product_quantity`（`_cquan`を上書き） | ［数値の配列］ |
| 製品単価 `product_unit_price`（`_cprice`を上書き） | ［数値の配列］ |
| 製品SKU `product_sku`（`_csku`を上書き） | ［文字列の配列］ |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| チェックアウト（checkout） | checkout |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| チェックアウト（checkout） | checkout |