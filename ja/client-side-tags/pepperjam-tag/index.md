---
title: Pepperjamタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPepperjamタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pepperjam-tag/
---## タグのヒント

* 以下のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 小計
  * プロモーションコード
  * 商品IDのリスト
  * 価格のリスト
  * 数量のリスト
  * カテゴリのリスト
* &#34;Standard Integration Type&#34;の値は、タグの統合値が&#34;Standard&#34;の場合にのみ適用されます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[Tag Overview]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Program ID**  
Pepperjamから提供されたID。
* **Integration**
* **Standard Integration Type**  
この選択は、このタグのStandard統合にのみ影響します。

## データマッピング

マッピングは、[data layer variable]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### Standard

|変数| 説明|
|---| ---|
|`base_url`|  &lt;ul&gt;&lt;li&gt;ベースURL&lt;/li&gt;&lt;/ul&gt; |
|`pid`|  &lt;ul&gt;&lt;li&gt;プログラムID&lt;/li&gt;&lt;/ul&gt; |
|`integration`|  &lt;ul&gt;&lt;li&gt;統合&lt;/li&gt;&lt;li&gt;値は次の通りです：&lt;ul&gt;&lt;li&gt;STANDARD&lt;/li&gt;&lt;li&gt;DYNAMIC&lt;/li&gt;&lt;li&gt;ITEMIZED&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`type`|  &lt;ul&gt;&lt;li&gt;Standard統合タイプ&lt;/li&gt;&lt;li&gt;値は**1**または**2**です。&lt;/li&gt;&lt;/ul&gt; |
|`new_to_file`|  &lt;ul&gt;&lt;li&gt;新規ファイル&lt;/li&gt;&lt;li&gt;値は**1**です。&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモーションコード&lt;/li&gt;&lt;li&gt;`_cpromo`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト&lt;/li&gt;&lt;li&gt;`_ccat`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

