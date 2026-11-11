---
title: Bidtellect Universal Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでBidtellect Universal Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bidtellect-universal-pixel-tag/
---
## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **顧客ブランドID**：ブランドを識別するためにBidtellectから提供される整数値です。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| 顧客ブランドID | Bidtellectから提供されるブランドIDです。 |
| URL | 指定した場合、ページURLを上書きします。 |