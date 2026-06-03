---
title: Teads広告主タグ構成ガイド
description: この記事では、Teads広告主タグをTealium iQタグ管理アカウントに構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/teads-advertiser-tag/
---
## タグのヒント

* マッピングを使用してタグの構成を上書きまたは動的に構成します。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Teads広告主タグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、データマッピングセクションの構成を行います。

## データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### スタンダード

| 変数             | 説明                                                                                      |
|:-----------------|:-------------------------------------------------------------------------------------------------|
| `advertiserId`   | &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;Teadsから提供される広告主ID。&lt;/li&gt;&lt;li&gt;例：`123456`&lt;/li&gt;&lt;/ul&gt; |
| `conversionType` | &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;コンバージョンの名前またはタイプ。&lt;/li&gt;&lt;/ul&gt;                              |
| `name` | 名前 |
| `price` | 価格 |
| `currency` | 通貨 |
