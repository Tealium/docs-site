---
title: Knotchタグ構成ガイド
description: この記事では、Knotchタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/knotch-tag/
---
## タグのヒント

* 最小utag.jsバージョン: 4.36。 `utag.js`テンプレートの更新についての詳細は、当社のナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
* マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Knotchタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、データマッピングセクションの構成を行います。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数              | 説明                                                                                                                                         |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| `unit_id`         | &lt;ul&gt;&lt;li&gt;あなたのKnotch Unit ID。&lt;/li&gt;&lt;li&gt;例えば、`knotch_12ab3cd456ef789a0bc12345`&lt;/li&gt;&lt;/ul&gt;                                                    |
| `tag_type`        | &lt;ul&gt;&lt;li&gt;値は`js`または`iframe`です&lt;/li&gt;&lt;/ul&gt;                                                                                                |
| `target_element`  | &lt;ul&gt;&lt;li&gt;Knotchウィジェットが表示されるべき要素（すでにページ上に存在する）のDOM ID。&lt;/li&gt;&lt;/ul&gt;                                     |
| `widget_position` | &lt;ul&gt;&lt;li&gt;Knotchウィジェットのターゲット要素に対する位置。&lt;/li&gt;&lt;li&gt;値は`append_child`、`before`、または`after`です。&lt;/li&gt;&lt;/ul&gt; |
