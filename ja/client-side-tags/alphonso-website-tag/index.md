---
title: Alphonsoウェブサイトタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAlphonsoウェブサイトタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/alphonso-website-tag/
---## タグのヒント

* デフォルトの構成オプションを使用すると、タグはページに直接スニペットを配置するのと同じように動作します。
* セッションID、UTMソース、UTMメディアは自動的に入力されます。これらのオプションを自分で管理するには、これらのオプションをオフにします。
* **&#43; カスタムデスティネーションを追加** ボタンを使用してカスタム値を追加します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **顧客ID**
  * Alphonsoから提供される値。
* **デフォルトのセッション管理を使用する**
  * コードスニペットに含まれるAlphonsoのセッション管理を使用します。
  * **いいえ**に構成した場合、セッションIDをマップする必要があります。
* **デフォルトのUTM解析を使用する**
  * コードスニペットに含まれるAlphonsoのUTMパラメータ解析を使用します。
  * **いいえ**に構成した場合、キャンペーンソースとキャンペーンメディアをマップする必要があります。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|説明| 説明|
|---| ---|
|`cust`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;/ul&gt; |
|`ord`|  &lt;ul&gt;&lt;li&gt;キャッシュバスター&lt;/li&gt;&lt;/ul&gt; |
|`utm_src`|  &lt;ul&gt;&lt;li&gt;キャンペーンソース&lt;/li&gt;&lt;/ul&gt; |
|`utm_mdm`|  &lt;ul&gt;&lt;li&gt;キャンペーンメディア&lt;/li&gt;&lt;/ul&gt; |
|`url`|  &lt;ul&gt;&lt;li&gt;ページURL&lt;/li&gt;&lt;/ul&gt; |
|`title`|  &lt;ul&gt;&lt;li&gt;ページタイトル&lt;/li&gt;&lt;/ul&gt; |
|`session_id`|  &lt;ul&gt;&lt;li&gt;セッションID&lt;/li&gt;&lt;/ul&gt; |
|`sess_status`|  &lt;ul&gt;&lt;li&gt;セッションステータス&lt;/li&gt;&lt;/ul&gt; |
|`ref`|  &lt;ul&gt;&lt;li&gt;リファラーURL&lt;/li&gt;&lt;/ul&gt; |
|`event_type`|  &lt;ul&gt;&lt;li&gt;イベント名&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;イベント値&lt;/li&gt;&lt;/ul&gt; |
|`useDefaultSession`|  &lt;ul&gt;&lt;li&gt;デフォルトのセッション管理を使用する&lt;/li&gt;&lt;/ul&gt; |
|`useDefaultUtm`|  &lt;ul&gt;&lt;li&gt;デフォルトのUTM解析を使用する&lt;/li&gt;&lt;/ul&gt; |
|`useOnBeforeUnload`|  &lt;ul&gt;&lt;li&gt;OnBeforeUnloadピクセルを使用する&lt;/li&gt;&lt;/ul&gt; |

