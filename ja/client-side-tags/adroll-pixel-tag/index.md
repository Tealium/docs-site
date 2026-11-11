---
title: AdRoll Pixelタグ構成ガイド
description: この記事では、AdRoll Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adroll-pixel-tag/
---
AdRollは、Eコマースブランドがディスプレイ広告、ソーシャルメディア広告、メールを簡単に展開できる単一のプラットフォームを提供します。これにより、既存顧客とのエンゲージメントを高め、新規顧客を獲得し、収益を拡大できます。

## タグに関するヒント

* 以下の項目でE-Commerce拡張機能をサポートしています。
  * 小計／コンバージョン値
  * 注文通貨／コンバージョン通貨
  * 注文ID／トランザクションID
  * 商品IDのリスト
  * カテゴリのリスト
  * 数量のリスト
  * 価格のリスト
* マッピングを使用すると、標準構成値とE-Commerce拡張機能の値を動的に上書きできます。
* 注文IDが入力されると、購入トラッキングが自動的に実行されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の項目を構成します。

* **広告主ID**：AdRollの広告主ID（`adroll_adv_id`）。
* **ピクセルID**：AdRollのピクセルID（`adroll_pix_id`）。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。

### タグの構成

| 変数 | 型 | 説明 |
|:---------|---|:------------|
|`adroll_adv_id`  | 文字列 | 広告主ID |
|`adroll_pix_id`  | 文字列 | ピクセルID |

### 標準

| 変数 | 型 | 説明 |
|:---------|---| :------------|
| `total`  | 文字列 | 合計 |
| `cartValue`  | 文字列 | カートの金額 |
| `product_group`  | 文字列 | 商品グループ |
|`site_type`  | 文字列 | サイトタイプ |
| `keywords`  | 文字列 | キーワード |

### E-Commerce

| 変数 | データ型 | 説明 |
|:----------|:----------|:---------------------------------------|
| `conversion_value` | 文字列 | 注文小計／コンバージョン値（`_csubtotal`を上書き） |
| `currency` | 文字列 | 注文通貨／コンバージョン通貨（`_ccurrency`を上書き） |
| `order_id` | 文字列 | 注文ID／トランザクションID（`_corder`を上書き） |
| `product_id` | 配列 | 商品ID（`_cprod`を上書き） |
| `category` | 配列 | 商品カテゴリ（`_ccat`を上書き） |
| `quantity`| 配列 | 商品数量（`_cquan`を上書き） |
| `price` | 配列 | 商品価格（`_cprice`を上書き） |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:------------|:---------|
| `productView` | 商品表示 |
| `homeView` | ホーム表示 |
| `productSearch` | 商品検索 |
| `addToCart` | カートに追加 |
| `purchase` | 購入 |
| `pageView` | ページ表示 |
| `custom` | カスタム |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:-----------|:------------|
| `productView` | 商品表示 |
| `homeView`    | ホーム表示 |
| `productSearch` | 商品検索 |
| `addToCart`  | カートに追加 |
| `purchase`   | 購入 |
| `pageView`   | ページ表示 |
| `custom`     | カスタム |