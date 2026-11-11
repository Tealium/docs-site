---
title: TV Scientificタグ構成ガイド
description: この記事では、TV Scientificタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tv-scientific-tag/
---
## タグ構成のヒント

マッピングを使用すると、標準の構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **ピクセルID**：アカウントにリンクされているピクセルの一意の識別子を指定します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `pixelId` | `String` | ピクセルID |
| `eventId` | `String` | イベントID |
| `orderAmount` | `Number` | 注文金額 |
| `referrerUrl` | `String` | 参照元URL |
| `orderId` | `String` | 注文ID |
| `lastTouchChannel` | `String` | ラストタッチチャネル |

### イベント固有のパラメーター

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `pixelId` | ピクセルID |
| `eventId` | イベントID |
| `orderAmount` | 注文金額 |
| `referrerUrl` | 参照元URL |
| `orderId` | 注文ID |
| `lastTouchChannel` | ラストタッチチャネル |