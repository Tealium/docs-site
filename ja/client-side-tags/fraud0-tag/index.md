---
title: Fraud0タグ構成ガイド
description: この記事では、タグ管理アカウントでFraud0タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fraud0-tag/
---
## タグ構成のヒント

* 必要に応じて、データマッピングを使用して標準のタグ構成構成を上書きします。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **タグID**：Fraud0タグID（`cid`）。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `cid` | 文字列 | タグID。 |
| `customer_id` | 文字列 | 顧客ID。 |
| `conversion_id` | 文字列 | コンバージョンID。 |