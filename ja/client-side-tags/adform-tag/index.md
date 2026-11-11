---
title: Adformタグ構成ガイド
description: この記事では、Adformタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adform-tag/
---
## タグに関するヒント

* 次のEコマース変数を使用します
  * `_corder`
  * `_csubtotal`
  * `_ccurrency`
  * `_ccountry`
  * `_cprod`
  * `_ccat`
  * `_cquan`
  * `_cprice`

* 区切り文字  
ページ名を分割するために使用する文字をAdformに指定します。
  * デフォルト値はパイプ文字 `|` です。
  * マッピングによって上書きできます

* カスタム変数は、注文レベルまたは商品レベルにマッピングできます。
  * 指定できる値は `sv[n]`、`svn[n] `、または `var[n] ` です。ここで、`n` は `89` 以下の任意の整数です。

* 購入ステップは、ルックアップテーブルを使用してマッピングする必要があります。
  * ステップ1：商品表示
  * ステップ2：買い物かご
  * ステップ3：コンバージョン（サンキューページ）

* カスタム注文／商品変数
  * `var` – データオブジェクト変数
  * `sv` – 文字列変数
  * `svn` – 数値変数

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **トラッキング構成ID**
  * Adformシステムによって生成される一意のクライアントID番号。

* **ページ名**
  * トラッキングポイントの一意の名前。
  * 変数マッピングを使用して動的に構成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込むタイミングを決定する条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

#### 標準

| 変数         | 説明                            |
|:-------------|:--------------------------------|
| `campaignid` | トラッキング構成ID／キャンペーンID |
| `page_name`  | トラッキングポイント名／ページ名 |
| `divider`    | 区切り文字                      |

#### Eコマース

| 変数                  | 説明                                                                                      |
|:----------------------|:------------------------------------------------------------------------------------------|
| `order_id`            | <ul><li>注文ID</li><li>`_corder` を上書きします。</li></ul>                                |
| `order_subtotal`      | <ul><li>小計</li><li>`_csubtotal` を上書きします。</li></ul>                               |
| `order_status`        | <ul><li>注文ステータス</li></ul>                                                           |
| `order_currency`      | <ul><li>通貨</li><li>`_ccurrency` を上書きします。</li></ul>                               |
| `customer_country`    | <ul><li>国</li><li>`_ccountry` を上書きします。</li></ul>                                  |
| `customer_agegroup`   | <ul><li>年齢層</li></ul>                                                                   |
| `customer_gender`     | <ul><li>性別</li></ul>                                                                     |
| `product_id`          | <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod` を上書きします。</li></ul>             |
| `product_name`        | <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname` を上書きします。</li></ul>          |
| `product_category`    | <ul><li>配列</li><li>カテゴリーのリスト。</li><li>`_ccat` を上書きします。</li></ul>         |
| `product_category_id` | <ul><li>配列</li><li>カテゴリーIDのリスト。</li></ul>                                       |
| `product_quantity`    | <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan` を上書きします。</li></ul>              |
| `product_unit_price`  | <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice` を上書きします。</li></ul>             |
| `product_weight`      | <ul><li>配列</li><li>商品重量のリスト。</li></ul>                                           |
| `step`                | <ul><li>ステップ</li><li>値は `1`／`2`／`3` です。</li></ul>                               |

#### カスタム注文／商品

カスタム変数は、注文レベルまたは商品レベルにマッピングできます。指定できる値は `sv[n]`、`svn[n] `、または `var[n] ` です。ここで、`n` は `89` 以下の任意の整数です。

| 変数      | 説明                                                    |
|:----------|:--------------------------------------------------------|
| `order`   | <ul><li>注文</li></ul>                                  |
| `product` | <ul><li>商品</li></ul>                                  |
| `var`     | <ul><li>`1` から `10` までのデータオブジェクト変数。</li></ul> |
| `sv`      | <ul><li>`1` から `89` までの文字列変数。</li></ul>       |
| `svn`     | <ul><li>`1` から `2` までの数値変数。</li></ul>          |

## ベンダーリソース

* [Adformテストおよびサポートセンター](http://creative.adform.com/support/)
* [Adformクリックおよびトラッキングピクセル](http://creative.adform.com/support/documentation/good-to-know/firing-adform-click-and-tracking-pixels/)