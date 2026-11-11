---
title: Teadsタグ構成ガイド
description: この記事では、Teadsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/teads-tag/
---
## タグに関するヒント

* マッピングを使用すると、標準の構成値を上書きしたり、追加のオプションを構成したりできます。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **pid**
  * Teadsから提供されたPID

* **lang**
  * 言語。
  * デフォルト値は英語（ `en`）です。

* **Slot**
  * 広告を配置するためのセレクター。
  * 例：`.article .article_body &gt; p`

* **Format**
* **minSlot**
* **Mobile**
* **css**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数       | 説明                      |
|:-----------|:--------------------------|
| Pid        |                           |
| Lang       |                           |
| Slot       |                           |
| Format     |                           |
| minSlot    |                           |
| mobile     | <ul><li>ブール値</li></ul> |
| Skip delay |                           |
| Mute delay |                           |
| CSS        |                           |
| BTF        | <ul><li>ブール値</li></ul> |
| Mutable    | <ul><li>ブール値</li></ul> |
| AdBreaks   |                           |
| avoidSlot  |                           |