---
title: Pixiboコンバージョンタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでpixibo.conversionタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pixibo-conversion-tag/
---## タグのヒント

* マッピングを使用して：
  * クライアントIDの標準構成値を動的に上書きします
  * 注文と製品詳細の値を動的に上書きします
* サポートされているE-Commerce拡張パラメータ：
  * 注文ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 通貨 (`_ccurrency`)
  * 顧客ID (`_ccusti` )
  * SKUのリスト (`_csku`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[Tag Overview]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアントID**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`clientId`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;クライアントID&lt;/li&gt;&lt;/ul&gt; |
|`size`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品サイズのリスト&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;SKUのリスト&lt;/li&gt;&lt;li&gt;`_csku`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |


