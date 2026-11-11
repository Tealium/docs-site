---
title: Bidtellectコンバージョンタグ構成ガイド
description: この記事では、タグ管理アカウントでBidtellectコンバージョンタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bidtellect-conversion-tag/
---
## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Bidtellect Conversion ID**：ブランドを識別するためにBidtellectから提供される整数値。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|---------|------------|
| Bidtellect ID | `bidtellect_id` |