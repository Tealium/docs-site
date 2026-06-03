---
title: CJアフィリエイト（旧Commission Junction）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでCJアフィリエイトコンバージョンタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/cj-affiliate-formerly-commission-junction-tag/
---
## タグのヒント

* このタグはE-Commerce Extension（`_corder`、`_cprod`、`_cquan`、`_cprice`）が必要です。
* **ITEM**、**AMT**、**QTY**、**DCNT**のE-Commerce Extensionの値を上書きするためにマッピングを使用します。
* 注文レベルの割引として**DISCOUNT**に変数をマップし、製品レベルの割引として**DCNT**に配列をマップします。
* ページ上で通貨が構成されていない場合、通貨は**USD**にデフォルト構成されます。
* イベントID変数を**CJEVENT**にマップして、イベントをアフィリエイトリファラルとして登録します。2018年10月以降のテンプレートを使用している場合、タグはデフォルトで`cjevent`クエリパラメータを使用しようとしますが、これを上書きするためにマッピングを使用することもできます。

### タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアントID**
  * 広告主アカウント番号
* **セールタグタイプ**
  * **スタンダード**：**CID**、**OID**、**TYPE**、**CURRENCY**が送信されます。
  * **アドバンスド**：追加の値**ITEM**、**AMT**、**QTY**、**DCNT**を送信します。
* **アクションID**
  * TYPEクエリストリングパラメータを構成します。
  * e-commerce extension `_ctype`の値を使用するために空白のままにします。
* **コンテナタグID**
  * 任意。
  * 画像タグを使用するために空白のままにします。
  * この値が構成されている場合、IMGタグの代わりにiframe（コンテナ）タグが使用されます。
* **CJリファラル期間**
  * 任意。
  * `CJEVENT`クッキーの期間を構成します。
  * 1から120までの数字を使用して日数を指定するか、セッションベースの期間を使用するデフォルトの動作を使用するために空白のままにします。
  * この構成オプションが有効になるためには、2018年10月以降のタグテンプレートを使用する必要があります。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|**宛先名**| **説明**|
|---| ---|
|`cid`|  &lt;ul&gt;&lt;li&gt;クライアントID&lt;/li&gt;&lt;li&gt;この変数にマップしてクライアントIDを動的に構成します。&lt;/li&gt;&lt;/ul&gt; |
|`aid`|  &lt;ul&gt;&lt;li&gt;アクションID&lt;/li&gt;&lt;li&gt;この変数にマップしてアクションIDを動的に構成します。これはクエリストリングの`TYPE`パラメータです。&lt;/li&gt;&lt;/ul&gt; |
|`containerid`|  &lt;ul&gt;&lt;li&gt;コンテナタグID&lt;/li&gt;&lt;li&gt;この変数にマップしてコンテナタグIDを動的に構成します。&lt;/li&gt;&lt;/ul&gt; |
|`name`|  &lt;ul&gt;&lt;li&gt;名前&lt;/li&gt;&lt;li&gt;この変数にマップして名前を動的に構成します。これはあなたのコンバージョンタグを一意に識別します。&lt;/li&gt;&lt;/ul&gt; |
|`CJEVENT`|  &lt;ul&gt;&lt;li&gt;CJイベント&lt;/li&gt;&lt;/ul&gt; |
|`referralperiod`|  &lt;ul&gt;&lt;li&gt;リファラル期間&lt;/li&gt;&lt;/ul&gt; |


### E-Commerce

|変数| 説明|
|---| ---|
|`OID`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;この変数に注文のIDをマップします。&lt;/li&gt;&lt;/ul&gt; |
|`AMOUNT`|  &lt;ul&gt;&lt;li&gt;注文合計。&lt;/li&gt;&lt;li&gt;この変数にマップして注文に適用される小計を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`CURRENCY`|  &lt;ul&gt;&lt;li&gt;注文通貨。&lt;/li&gt;&lt;li&gt;この変数にマップして注文に適用される通貨を上書きします。&lt;/li&gt;&lt;li&gt;デフォルトは**USD**です。&lt;/li&gt;&lt;/ul&gt; |
|`DISCOUNT`|  &lt;ul&gt;&lt;li&gt;注文割引。&lt;/li&gt;&lt;li&gt;この変数にマップして注文に適用される割引を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`COUPON`|  &lt;ul&gt;&lt;li&gt;注文クーポン。&lt;/li&gt;&lt;li&gt;この変数に注文に適用されるクーポン名をマップします。&lt;/li&gt;&lt;/ul&gt; |
|`ITEM`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品アイテム&lt;/li&gt;&lt;li&gt;この変数にマップして製品IDを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`AMT`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品価格。&lt;/li&gt;&lt;li&gt;この変数にマップして製品価格を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`QTY`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品数量。&lt;/li&gt;&lt;li&gt;この変数にマップして製品数量を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`DCNT`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品割引。&lt;/li&gt;&lt;li&gt;この変数にマップして注文に適用される割引を上書きします。&lt;/li&gt;&lt;/ul&gt; |

### アドバンスド

これらの変数は、あなたの担当のCJクライアント統合エンジニアから指示された場合にのみ使用してください。

|**宛先名**| **説明**|
|---| ---|
|`CHANNEL`|  &lt;ul&gt;&lt;li&gt;チャネル&lt;/li&gt;&lt;li&gt;この変数に最後のクリックに帰属するチャネルをマップします。&lt;/li&gt;&lt;/ul&gt; |
|`CHANNEL_TS`|  &lt;ul&gt;&lt;li&gt;チャネルTS&lt;/li&gt;&lt;li&gt;この変数に最後のクリックに帰属する日時スタンプをマップします。&lt;/li&gt;&lt;/ul&gt; |

## ベンダーのドキュメンテーション

* [CJ用語集](http://www.cj.com/glossary)
* [アフィリエイトマーケティングとは何ですか？](http://www.cj.com/what-is-affiliate-marketing)
* [CJサポートセンターとFAQ](http://www.cj.com/support-center#most-popular-topics)

