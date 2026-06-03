---
title: True Fit統合タグの構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでTrue Fit統合タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/true-fit-integration-tag/
---
この記事では、True Fit統合タグの構成方法について説明します。

## タグのヒント

* 質問がある場合は、`support@truefit.com`にメールを送ってください。
* PDP統合: https://techdocs.truefitcorp.com/docs/product-detail-page-integration
* 注文確認統合: https://techdocs.truefitcorp.com/docs/order-confirmation-integration
* このタグはjQueryを必要とし、最新のjQueryバージョンと互換性がない場合があります。
* このタグは、ページ上のカスタムコールバック関数やdivを必要とする場合があります。
* 注文追跡のために、**registered**、**userid**、および**orderid**に値をマップします。
* マッピングを使用して以下のことを行います：
  * イベントトリガーの構成
  * 標準構成値の動的な上書き
  * E-Commerce拡張値の動的な上書き

* このタグは以下のE-Commerce拡張パラメータをサポートしています：
  * 注文ID
  * ユーザーID
  * 製品ID
  * 製品IDのリスト
  * 単価のリスト
  * 数量のリスト

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **Store Key**: これはあなたのストアの三文字の頭文字です。詳細はTrue Fitのプロジェクトマネージャーにお問い合わせください。
* **Environment**: この値を`staging`に構成してステージング/開発環境を構成し、`prod`に構成して製品環境を構成します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成

| 変数 | 説明 |
|:---------|:------------|
| Store Key `storeKey`  | 文字列 |
| Environment `environment`  | 文字列 |

### 標準

| 変数 | 説明 |
|:---------|:------------|
| Locale `locale`  | 文字列 |
| Product Size `size`  | [文字列の配列] |
| Product currency `currency`  | [文字列の配列] |
| Color ID `colorId`  | [文字列の配列] |
| Sales Group `salesGroup`  | [文字列の配列] |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| Order ID `orderId` (Overrides `_corder`)  | 文字列 |
| User ID `userId` (Overrides `_ccustid`)  | 文字列 |
| Product ID `productId` (Overrides `_cprod`)  | [文字列の配列] |
| Product Quantity `product_quantity` (Overrides `_cquan`)  | [数値の配列] |
| Product Unit Price `product_unit_price` (Overrides `_cprice`)  | [数値の配列] |
| Product Sku `product_sku` (Overrides `_csku`)  | [文字列の配列] |

### イベント
イベントをマップするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| Checkout (checkout) | チェックアウト |

### イベント固有のパラメータ
イベントをマップするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| Checkout (checkout) | チェックアウト |

