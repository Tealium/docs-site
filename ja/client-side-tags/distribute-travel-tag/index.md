---
title: Distribute Travelタグ構成ガイドの配布
description: この記事では、Distribute Travelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/distribute-travel-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、Distribute Travelタグをプロフィールに追加します（[タグの追加]()を参照）。

タグを追加したら、以下の構成を行います：

* **Distribute Travel ID:** Distribute Travelから提供される整数値（例：`123456`）

## ロードルール

[ロードルール]()は、このタグをサイト上のどこといつロードするかを決定します。

推奨されるロードルール：**すべてのページ**

## データマッピング

マッピングは、[データレイヤー変数](/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Distribute Travelタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリーは以下の通りです：

### 標準

| **宛先名** | **説明**                          |
|:---------------------|:-----------------------------------------|
| Distribute Travel ID | Distribute Travelから提供されるID |
