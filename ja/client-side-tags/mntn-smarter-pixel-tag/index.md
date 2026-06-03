---
title: MNTN スマーターピクセルタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMNTN（旧Steelhouse）スマーターピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mntn-smarter-pixel-tag/
---

## タグのヒント

* マッピングを使用してアカウントIDを動的に上書きするか、`additional`パラメータにデータを渡します。
* 注文IDが構成されると、コンバージョンタグが発火します。
* 以下のE-Commerce拡張パラメータをサポートしています：
  * 注文ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 製品IDのリスト (`_cprod`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)

## タグの構成

まず、タグマーケットプレイスに移動し、MNTNスマーターピクセルタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **アカウントID**
  * 例：`12345`

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`acct`| アカウントID|

### 追加変数

|変数| 説明|
|---| ---|
|`adv.track.myvar`|  追加トラッキング変数 |
|`adv.conv.myvar`|  アカウントコンバージョン変数 |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
