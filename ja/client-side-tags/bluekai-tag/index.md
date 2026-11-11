---
title: BlueKaiタグ構成ガイド
description: この記事では、タグ管理アカウントでBlueKaiタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bluekai-tag/
---
## タグに関するヒント

マッピングを使用すると、標準の構成値を上書きしたり、追加のパラメーターを渡したりできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **サイトID**：ピクセルが特定のDMPパートナーに属していることを識別する一意の番号。
* **上限**：BlueKaiによって配信されるメディアパートナーのセグメントピクセルの最大数。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

BlueKaiタグでは、次の変数を使用できます。

### 標準

|変数|説明|
|---|---|
|サイトID| (siteid)|
|上限| (limit)|
|複数回の呼び出しを許可（`allow_multiple_calls`）| [ブール値]|
|show| |
|tod| |
|lv| |
|ss| |
|top| |
|sub1| |
|sub2| |
|sub3| |
|ref| |
|srch| |