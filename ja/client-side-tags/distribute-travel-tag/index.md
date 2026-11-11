---
title: Distribute Travelタグ構成ガイド
description: この記事では、Distribute Travelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/distribute-travel-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、Distribute Travelタグをプロファイルに追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加したら、以下の構成を行います。

* **Distribute Travel ID：** Distribute Travelから提供される整数値（例：`123456`）

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをサイト上でいつ、どこに読み込むかを指定します。

推奨される読み込みルール：**すべてのページ**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Distribute Travelタグの宛先変数は、［データマッピング］タブに組み込まれています。利用可能なカテゴリーは次のとおりです。

### 標準

| **宛先名**           | **説明**                                  |
|:---------------------|:------------------------------------------|
| Distribute Travel ID | Distribute Travelから提供されたID         |