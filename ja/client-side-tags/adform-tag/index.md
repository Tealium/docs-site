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

まず、Tealiumのタグマーケットプレイスに移動し、Adformタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **トラッキング構成ID**
  * Adformシステムによって生成されたユニークなクライアントID番号。

* **ページ名**
  * トラッキングポイントのユニークな名前。
  * これを動的に構成するために変数マッピングを使用します。

### データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

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
| `order_id`            | &lt;ul&gt;&lt;li&gt;オーダーID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                         |
| `order_subtotal`      | &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                      |
| `order_status`        | &lt;ul&gt;&lt;li&gt;オーダーステータス&lt;/li&gt;&lt;/ul&gt;                                                  |
| `order_currency`      | &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                      |
| `customer_country`    | &lt;ul&gt;&lt;li&gt;国&lt;/li&gt;&lt;li&gt;`_ccountry`を上書きします。&lt;/li&gt;&lt;/ul&gt;                        |
| `customer_agegroup`   | &lt;ul&gt;&lt;li&gt;年齢層&lt;/li&gt;&lt;/ul&gt;                                                     |
| `customer_gender`     | &lt;ul&gt;&lt;li&gt;性別&lt;/li&gt;&lt;/ul&gt;                                                        |
| `product_id`          | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_name`        | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt;  |
| `product_category`    | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト。&lt;/li&gt;&lt;li&gt;`_ccat`を上書きします。&lt;/li&gt;&lt;/ul&gt;  |
| `product_category_id` | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリIDのリスト。&lt;/li&gt;&lt;/ul&gt;                           |
| `product_quantity`    | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price`  | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt;    |
| `product_weight`      | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品重量のリスト。&lt;/li&gt;&lt;/ul&gt;                        |
| `step`                | &lt;ul&gt;&lt;li&gt;ステップ&lt;/li&gt;&lt;li&gt;`1`/ `2`/ `3`の値。&lt;/li&gt;&lt;/ul&gt;                         |

#### カスタムオーダー/商品

カスタム変数は、オーダーレベルまたは商品レベルにマッピングできます。可能な値は `sv[n]`, `svn[n] `または `var[n] `で、`n` は `1` から `89` までの任意の整数です。

| 変数     | 説明                                                      |
|:----------|:-----------------------------------------------------------------|
| `order`   | &lt;ul&gt;&lt;li&gt;オーダー&lt;/li&gt;&lt;/ul&gt;                                          |
| `product` | &lt;ul&gt;&lt;li&gt;商品&lt;/li&gt;&lt;/ul&gt;                                        |
| `var`     | &lt;ul&gt;&lt;li&gt;`1`から`10`までのデータオブジェクト変数。&lt;/li&gt;&lt;/ul&gt; |
| `sv`      | &lt;ul&gt;&lt;li&gt;`1`から`89`までの文字列変数。&lt;/li&gt;&lt;/ul&gt;     |
| `svn`     | &lt;ul&gt;&lt;li&gt;`1`から`2`までの数値変数。&lt;/li&gt;&lt;/ul&gt;      |

### ベンダーリソース

* [Adformテストとサポートセンター](http://creative.adform.com/support/)
* [Adformクリックとトラッキングピクセル](http://creative.adform.com/support/documentation/good-to-know/firing-adform-click-and-tracking-pixels/)
