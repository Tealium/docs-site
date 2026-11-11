---
title: Adara Media Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでAdara Media Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adara-media-pixel-tag/
---
## タグに関するヒント

URLで送信できるパラメーターがいくつかあります。動的変数を渡すには、マッピングツールボックスを使用します。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **パートナーID**：Adaraから提供されたAdaraパートナーID。
* **タグタイプ**：使用するタグのタイプ。指定可能な値は以下のとおりです。
    * `Image`：画像タグを使用してベンダーにデータを送信します。このタグタイプでは、追加のパラメーターはサポートされません。
    * `Script`：スクリプトタグを使用してベンダーにデータを送信します。このタグタイプでは、URLで送信可能な追加のパラメーターがサポートされます。パラメーターの詳細については、[Adara：Impactを使用したSEMおよびYouTubeトラッキング](https://docs.adara.com/impact/sem-and-youtube-tracking-with-impact#step-3-add-url-tracking-template-to-sem-campaigns)を参照してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | タイプ／値 | 説明 |
|:---------|:-----|:------------|
| `pid` | 文字列 | パートナーID。 |