---
title: APPRLタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAPPRLタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/apprl-tag/
---## タグのヒント

* 注文IDが入力されている場合、注文の追跡は自動的に行われます。
* 次のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 注文合計
  * 注文通貨
  * SKUのリスト
  * 数量のリスト
  * 価格のリスト

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要]()の記事を読んでください。


## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### タグ構成

|変数| 説明|
|---| ---|
|`base_url`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ベースURL&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_value`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;注文価値。&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;通貨。&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`sku`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;SKUのリスト。&lt;/li&gt;&lt;li&gt;`_csku`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

