---
title: iAdvizeタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでiAdvizeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/iadvize-tag/
---## タグのヒント

* 注文IDとカートの金額が入力されると、トランザクションの追跡が自動的に行われます。
* 次のeコマース拡張パラメーターをサポートしています：
  * 注文ID (`_corder`)
  * 注文の小計 (`_csubtotal`)
* CustomDataタグに追加のパラメーターを渡したい場合は、マッピングツールボックスにカスタムデスティネーションを追加します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[Tag Overview]()記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **サイトID**
  * あなたのiAdvizeサイトID。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応するデスティネーション変数にデータを送信するプロセスです。変数をタグのデスティネーションにマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### スタンダード

|変数| 説明|
|---| ---|
|`sid`|  &lt;ul&gt;&lt;li&gt;サイトID&lt;/li&gt;&lt;/ul&gt; |
|`lang`|  &lt;ul&gt;&lt;li&gt;言語&lt;/li&gt;&lt;/ul&gt; |

### E-コマース

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文/トランザクションID。&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計/カートの金額。&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

