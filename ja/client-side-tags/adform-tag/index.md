---
title: Adformタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdformタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adform-tag/
---
## タグのヒント

* 以下のE-Commerce変数を使用します
  * `_corder`
  * `_csubtotal`
  * `_ccurrency`
  * `_ccountry`
  * `_cprod`
  * `_ccat`
  * `_cquan`
  * `_cprice`

* Divider  
Adformにページ名を分割するために使用する文字を指示します。
  * デフォルト値はパイプ文字 `|` です。
  * マッピングにより上書き可能

* カスタム変数は、オーダーレベルまたはプロダクトレベルにマッピングできます。
  * 可能な値は `sv[n]`, `svn[n] `または `var[n] `で、`n` は `1` から `89` までの任意の整数です。

* 購入ステップはルックアップテーブルを使用してマッピングする必要があります。
  * ステップ1: 商品表示
  * ステップ2: バスケット
  * ステップ3: コンバージョン（サンキューページ）

* カスタムオーダー/プロダクト変数
  * `var` – データオブジェクト変数
  * `sv` – 文字列変数
  * `svn` – 数値変数

### タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Adformタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **トラッキング構成ID**
  * Adformシステムによって生成されたユニークなクライアントID番号。

* **ページ名**
  * トラッキングポイントのユニークな名前。
  * これを動的に構成するために変数マッピングを使用します。

### データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

#### スタンダード

| 変数         | 説明                   |
|:-------------|:------------------------------|
| `campaignid` | トラッキング構成ID/キャンペーンID |
| `page_name`  | トラッキングポイント名/ページ名 |
| `divider`    | ディバイダー                       |

#### E-Commerce

| 変数                  | 説明                                                                     |
|:----------------------|:--------------------------------------------------------------------------------|
| `order_id`            | <ul><li>オーダーID</li><li>`_corder`を上書きします。</li></ul>                         |
| `order_subtotal`      | <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul>                      |
| `order_status`        | <ul><li>オーダーステータス</li></ul>                                                  |
| `order_currency`      | <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul>                      |
| `customer_country`    | <ul><li>国</li><li>`_ccountry`を上書きします。</li></ul>                        |
| `customer_agegroup`   | <ul><li>年齢層</li></ul>                                                     |
| `customer_gender`     | <ul><li>性別</li></ul>                                                        |
| `product_id`          | <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
| `product_name`        | <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li></ul>  |
| `product_category`    | <ul><li>配列</li><li>カテゴリのリスト。</li><li>`_ccat`を上書きします。</li></ul>  |
| `product_category_id` | <ul><li>配列</li><li>カテゴリIDのリスト。</li></ul>                           |
| `product_quantity`    | <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
| `product_unit_price`  | <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul>    |
| `product_weight`      | <ul><li>配列</li><li>商品重量のリスト。</li></ul>                        |
| `step`                | <ul><li>ステップ</li><li>`1`/ `2`/ `3`の値。</li></ul>                         |

#### カスタムオーダー/商品

カスタム変数は、オーダーレベルまたは商品レベルにマッピングできます。可能な値は `sv[n]`, `svn[n] `または `var[n] `で、`n` は `1` から `89` までの任意の整数です。

| 変数     | 説明                                                      |
|:----------|:-----------------------------------------------------------------|
| `order`   | <ul><li>オーダー</li></ul>                                          |
| `product` | <ul><li>商品</li></ul>                                        |
| `var`     | <ul><li>`1`から`10`までのデータオブジェクト変数。</li></ul> |
| `sv`      | <ul><li>`1`から`89`までの文字列変数。</li></ul>     |
| `svn`     | <ul><li>`1`から`2`までの数値変数。</li></ul>      |

### ベンダーリソース

* [Adformテストとサポートセンター](http://creative.adform.com/support/)
* [Adformクリックとトラッキングピクセル](http://creative.adform.com/support/documentation/good-to-know/firing-adform-click-and-tracking-pixels/)
