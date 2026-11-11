---
title: Lyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでLyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/lytics-tag/
---

## タグに関するヒント

* マッピングを使用して、標準構成値を上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **コレクションID**：Lyticsから提供されたコレクションID（`cid`/`account id`）

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`cid`|コレクションID|