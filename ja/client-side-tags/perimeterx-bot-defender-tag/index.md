---
title: PerimeterX Bot Defenderタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPerimeterX Bot Defenderタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/perimeterx-bot-defender-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **AppID**: あなたのユニークなアプリケーション識別子

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`appId`|  &lt;ul&gt;&lt;li&gt;AppID&lt;/li&gt;&lt;/ul&gt; |
|`_pxParam1`|  &lt;ul&gt;&lt;li&gt;カスタムパラメータ1&lt;/li&gt;&lt;/ul&gt; |
|`_pxParam2`|  &lt;ul&gt;&lt;li&gt;カスタムパラメータ2&lt;/li&gt;&lt;/ul&gt; |
|`_pxParam3`|  &lt;ul&gt;&lt;li&gt;カスタムパラメータ3&lt;/li&gt;&lt;/ul&gt; |
|`_pxParam4`|  &lt;ul&gt;&lt;li&gt;カスタムパラメータ4&lt;/li&gt;&lt;/ul&gt; |

