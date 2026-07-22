---
title: AdRoll Pixelタグ構成ガイド
description: この記事では、AdRoll Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adroll-pixel-tag/
---
AdRollは、既存の顧客とのエンゲージメントを深め、新規顧客を引き付け、収益を増加させるためのディスプレイ広告、ソーシャルメディア広告、メールを簡単に立ち上げることができる一体型プラットフォームを提供しています。

## タグのヒント

* E-Commerce拡張に対応しています:
  * 小計/コンバージョン値
  * 注文通貨/コンバージョン通貨
  * 注文ID/トランザクションID
  * 商品IDのリスト
  * カテゴリのリスト
  * 数量のリスト
  * 価格のリスト
* 標準の構成値とE-Commerce拡張の値を動的に上書きするためにマッピングを使用します。
* 注文IDが入力されると、購入の追跡が自動的に行われます。

## タグの構成

新しいタグを追加するために、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います:

* **広告主ID**: Adrollの広告主ID (`adroll_adv_id`)。
* **ピクセルID**: AdrollのピクセルID (`adroll_pix_id`)。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです:

### タグ構成

| 変数 | タイプ |説明 |
|:---------|---|:------------|
|`adroll_adv_id`  | 文字列 | 広告主ID |
|`adroll_pix_id`  | 文字列 |  ピクセルID |

### 標準

| 変数 | タイプ | 説明 |
|:---------|---| :------------|
| `total`  | 文字列 |合計 |
| `cartValue`  | 文字列 |カートの値 |
| `product_group`  | 文字列 | 商品グループ |
|`site_type`  | 文字列 |  サイトタイプ |
| `keywords`  | 文字列 | キーワード |

### E-Commerce

| 変数 | データタイプ | 説明                            |
|:----------|:----------|:---------------------------------------|
| `conversion_value` | 文字列    | 注文小計/コンバージョン値 (`_csubtotal`を上書き) |
| `currency` | 文字列    | 注文通貨/コンバージョン通貨 (`_ccurrency`を上書き) |
| `order_id` | 文字列    | 注文ID/トランザクションID (`_corder`を上書き) |
| `product_id` | 配列     | 商品ID (`_cprod`を上書き) |
| `category` | 配列     | 商品カテゴリ (`_ccat`を上書き) |
| `quantity`| 配列     | 商品数量 (`_cquan`を上書き) |
| `price` | 配列     | 商品価格 (`_cprice`を上書き) |



### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

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

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数   | 説明 |
|:-----------|:------------|
| `productView` | 商品表示 |
| `homeView`    | ホーム表示    |
| `productSearch` | 商品検索 |
| `addToCart`  | カートに追加   |
| `purchase`   | 購入      |
| `pageView`   | ページ表示     |
| `custom`     | カスタム        |

