---
title: TV Scientificタグ構成ガイド
description: この記事では、TV Scientificタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tv-scientific-tag/
---
## タグのヒント

マッピングを使用して、標準の構成値を動的に上書きします。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **ピクセルID**：アカウントにリンクされたピクセルの一意の識別子を指定します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `pixelId` | `String` | ピクセルID |
| `eventId` | `String` | イベントID |
| `orderAmount` | `Number` | 注文金額 |
| `referrerUrl` | `String` | リファラーURL |
| `orderId` | `String` | 注文ID |
| `lastTouchChannel` | `String` | 最後に触れたチャンネル |

### イベント固有のパラメータ

イベントをマップするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `pixelId` | ピクセルID |
| `eventId` | イベントID |
| `orderAmount` | 注文金額 |
| `referrerUrl` | リファラーURL |
| `orderId` | 注文ID |
| `lastTouchChannel` | 最後に触れたチャンネル |
