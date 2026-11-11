---
title: SalesViewerタグ構成ガイド
description: この記事では、タグ管理アカウントでSalesViewerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salesviewer-tag/
---
## タグ構成のヒント

* マッピングを使用して、SalesViewer IDを動的に構成できます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **SalesViewer ID**：SalesViewerから提供されたID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `salesviewer_id` | SalesViewer ID。 |