---
title: RToasterタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでRToasterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rtoaster-tag/
---
## タグのヒント

* カンマで区切ったリストとしてIDを入力することで、複数の要素IDを構成できます。
* マッピングを使用して、標準の構成値を上書きします。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Rtoasterタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **アカウントID**
  * あなたのRtoasterアカウントID。

* **推奨要素ID**
  * Rtoasterの推奨対象となる要素のID。
  * カンマで区切ったリストとして複数のIDを入力できます。

* **ポップアップ要素ID**
  * Rtoasterのポップアップ推奨対象となる要素のID。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`account_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;アカウントID&lt;/li&gt;&lt;/ul&gt; |
|`element_id`|  &lt;ul&gt;&lt;li&gt;文字列、配列&lt;/li&gt;&lt;li&gt;要素ID&lt;/li&gt;&lt;/ul&gt; |
|`popup_element_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ポップアップ要素ID&lt;/li&gt;&lt;/ul&gt; |
|`category`|  &lt;ul&gt;&lt;li&gt;文字列、配列&lt;/li&gt;&lt;li&gt;カテゴリ&lt;/li&gt;&lt;/ul&gt; |
|`price_min`|  &lt;ul&gt;&lt;li&gt;文字列、数値&lt;/li&gt;&lt;li&gt;最低価格&lt;/li&gt;&lt;/ul&gt; |
|`price_max`|  &lt;ul&gt;&lt;li&gt;文字列、数値&lt;/li&gt;&lt;li&gt;最高価格&lt;/li&gt;&lt;/ul&gt; |

### E-コマース

|変数| 説明|
|---| ---|
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料。&lt;/li&gt;&lt;li&gt;`_cship`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
