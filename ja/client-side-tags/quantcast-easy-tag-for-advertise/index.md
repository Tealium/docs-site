---
title: Quantcast Easy Tag for Advertise構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuantcast Easy Tag for Advertiseを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-easy-tag-for-advertise/
---
## タグのヒント

* マッピングを使用して：
  * アカウントの標準構成値を動的に上書きします。
  * E-Commerce拡張の値を動的に上書きします。
  * `_fp`ラベルを`_qevents`の一部として渡します。
  * 自由形式のラベル（`mylabel`）を渡します。
  * 自由形式のラベルへの配列のマッピングは、Quantcastのドキュメンテーションに従って処理されます。

* 以下のE-Commerce拡張パラメーターをサポートしています：
  * 注文ID（`_corder`）
  * 注文小計（`_csubtotal`）

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Quantcast Easy Tag for Advertiseタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **アカウントコード**
  * アカウントコード（P-code）。
  * `p-`で始まる13文字の大文字小文字を区別する英数字のコード。
  * 質問がある場合は、Quantcastの担当者にお問い合わせください。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`qacct`|  &lt;ul&gt;&lt;li&gt;アカウントコード（P-code）。&lt;/li&gt;&lt;li&gt;`p-`で始まる13文字の大文字小文字を区別する英数字のコード。&lt;/li&gt;&lt;/ul&gt; |
|`_fp.event`|  &lt;ul&gt;&lt;li&gt;イベント&lt;/li&gt;&lt;/ul&gt; |
|`_fp.channel`|  &lt;ul&gt;&lt;li&gt;チャンネル&lt;/li&gt;&lt;/ul&gt; |
|`_fp.subchannel`|  &lt;ul&gt;&lt;li&gt;サブチャンネル&lt;/li&gt;&lt;/ul&gt; |
|`_fp.customer`|  &lt;ul&gt;&lt;li&gt;顧客&lt;/li&gt;&lt;/ul&gt; |
|`_fp.pcat`|  &lt;ul&gt;&lt;li&gt;商品カテゴリー&lt;/li&gt;&lt;/ul&gt; |
|`mylabel`|  &lt;ul&gt;&lt;li&gt;カスタムラベル&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`orderid`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;E-Comm注文IDを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`revenue`|  &lt;ul&gt;&lt;li&gt;収益。&lt;/li&gt;&lt;li&gt;E-Comm注文小計を上書きします。&lt;/li&gt;&lt;/ul&gt; |
