---
title: Teads広告主タグ構成ガイド
description: この記事では、Teads広告主タグをTealium iQタグ管理アカウントに構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/teads-advertiser-tag/
---
## タグのヒント

* マッピングを使用してタグの構成を上書きまたは動的に構成します。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Teads広告主タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、データマッピングセクションの構成を行います。

## データマッピング

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### スタンダード

| 変数             | 説明                                                                                      |
|:-----------------|:-------------------------------------------------------------------------------------------------|
| `advertiserId`   | <ul><li>必須。</li><li>Teadsから提供される広告主ID。</li><li>例：`123456`</li></ul> |
| `conversionType` | <ul><li>オプション。</li><li>コンバージョンの名前またはタイプ。</li></ul>                              |
| `name` | 名前 |
| `price` | 価格 |
| `currency` | 通貨 |
