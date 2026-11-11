---
title: Measure向けQuantcast Easy Tag構成ガイド
description: この記事では、タグ管理アカウントでMeasure向けQuantcast Easy Tagを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-easy-tag-for-measure/
---
## タグに関するヒント

* マッピングを使用して、アカウントの標準構成値を動的に上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **アカウントコード**
  * アカウントコード（Pコード）。
  * `p-`で始まる、大文字と小文字が区別される13文字の英数字コード。
  * ご不明な点がある場合は、Quantcastの担当者にお問い合わせください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`qacct`| <ul><li>アカウントコード（Pコード）。</li><li>`p-`で始まる、大文字と小文字が区別される13文字の英数字コード。</li></ul> |