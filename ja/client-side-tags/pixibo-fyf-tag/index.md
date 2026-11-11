---
title: Pixibo FYFタグ構成ガイド
description: この記事では、タグ管理アカウントで「Find your Fit」pixibo.fyfタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pixibo-fyf-tag/
---## タグに関するヒント

* マッピングを使用すると、標準構成値を動的に上書きできます。
* タグを発火させるには、マッピング内のSKU IDが必須です。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **クライアント名**
* **クライアントID**
* **環境**
  * スクリプトの環境を指定するために使用します。
* **言語**
  * 任意
  * ウィジェットを読み込む際の言語です。
  * デフォルト値は英語（`en`）です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`clientName`| <ul><li>クライアント名</li></ul> |
|`clientId`| <ul><li>クライアントID</li></ul> |
|`environment`| <ul><li>環境</li></ul> |
|`skuId`| <ul><li>SKU ID</li></ul> |
|`lang`| <ul><li>言語</li></ul> |