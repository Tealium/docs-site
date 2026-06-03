---
title: Intent Media 広告主ピクセルタグ構成ガイド
description: この記事では、Tealium iQタグ管理（TiQ）アカウントでIntent Media広告主ピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intent-media-advertiser-pixel-tag/
---## タグのヒント

* 以下のE-Commerce変数を使用します
  * `_corder`
  * `_csubtotal`/`_ctotal`
  * `_ccurrency`
  * `_ccustid`
* ページビュータイプ/ページカテゴリはマッピングで上書き可能です

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **エンティティID**
  * Intent Media広告主ピクセルによって構成されます。
* **ページビュータイプ**
  * &#39;HOME&#39;, &#39;LIST&#39;, &#39;DETAILS&#39;, &#39;CART&#39;, &#39;EMAIL&#39;, &#39;EMAIL_CONFIRMATION&#39;, &#39;CONVERSION&#39;, &#39;UNKNOWN&#39;のいずれかでなければなりません。
* **製品カテゴリ**
  * &#39;HOME&#39;, &#39;FLIGHTS&#39;, &#39;CARS&#39;, &#39;HOTELS&#39;, &#39;PACKAGE&#39;, &#39;EMAIL&#39;, &#39;UNKNOWN&#39;のいずれかでなければなりません。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`Entity` ID|  &lt;ul&gt;&lt;li&gt;エンティティID。&lt;/li&gt;&lt;li&gt;Intent Media広告主ピクセルによって構成されます。&lt;/li&gt;&lt;/ul&gt; |
|`page_view_type`|  &lt;ul&gt;&lt;li&gt;ページビュータイプ。&lt;/li&gt;&lt;li&gt;以下のいずれかでなければなりません：  &lt;ul&gt;&lt;li&gt;HOME&lt;/li&gt;&lt;li&gt;LIST&lt;/li&gt;&lt;li&gt;DETAILS&lt;/li&gt;&lt;li&gt;CART&lt;/li&gt;&lt;li&gt;EMAIL&lt;/li&gt;&lt;li&gt;EMAIL\_CONFIRMATION&lt;/li&gt;&lt;li&gt;CONVERSION&lt;/li&gt;&lt;li&gt;UNKNOWN&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;製品カテゴリ。&lt;/li&gt;&lt;li&gt;以下のいずれかでなければなりません：  &lt;ul&gt;&lt;li&gt;HOME&lt;/li&gt;&lt;li&gt;FLIGHTS&lt;/li&gt;&lt;li&gt;CARS&lt;/li&gt;&lt;li&gt;HOTELS&lt;/li&gt;&lt;li&gt;PACKAGE&lt;/li&gt;&lt;li&gt;EMAIL&lt;/li&gt;&lt;li&gt;UNKNOWN&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`page_id`|  &lt;ul&gt;&lt;li&gt;ページID&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;デフォルトの`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;注文の小計。&lt;/li&gt;&lt;li&gt;デフォルトの`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;通貨。&lt;/li&gt;&lt;li&gt;デフォルトの`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`custid`|  &lt;ul&gt;&lt;li&gt;顧客ID。&lt;/li&gt;&lt;li&gt;デフォルトの`_ccustid`（`user_member_id`）を上書きします。&lt;/li&gt;&lt;/ul&gt; |

