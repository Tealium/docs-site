---
title: Eloquaタグ構成ガイド
description: この記事では、Eloquaタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/eloqua-tag-set-up-guide/
---
## タグのヒント

* **Wait = Yes**のデフォルト構成を保持して、Eloqua JavaScript (JS) ファイルがDOM Readyで実行されるようにします。
* フォームトラッキングのために、以下のパラメータの値を構成するためにマッピングを使用します：
  * `form_tracking` (on)
  * `elqFormName`
  * `elqFormGUIDElement`

## タグの構成

まず、Tealiumのタグマーケットプレイスに行き、Eloquaタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **タイトル**  
同じベンダーによる複数のタグを使用する場合は、一意の名前を割り当てます。
* **サイトID**  
サイトIDは通常、一連の数字です。
* **ファーストパーティクッキードメイン名**  
あなたのファーストパーティクッキーのドメイン名

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数                 | 説明                                                        |
|:---------------------|:-------------------------------------------------------------------|
| `form_tracking`      | &lt;ul&gt;&lt;li&gt;フォームトラッキング。&lt;/li&gt;&lt;li&gt;値は `on` または `off`。&lt;/li&gt;&lt;/ul&gt; |
| `elqFormName`        | &lt;ul&gt;&lt;li&gt;フォーム名。&lt;/li&gt;&lt;/ul&gt;                                       |
| `elqFormGUIDElement` | &lt;ul&gt;&lt;li&gt;フォーム要素。&lt;/li&gt;&lt;/ul&gt;                                    |
| `base_url`           | &lt;ul&gt;&lt;li&gt;JavaScriptファイルのURL。&lt;/li&gt;&lt;/ul&gt;                             |
| `elqDomainName`      | &lt;ul&gt;&lt;li&gt;ファーストパーティクッキードメイン名&lt;/li&gt;&lt;/ul&gt;                   |
