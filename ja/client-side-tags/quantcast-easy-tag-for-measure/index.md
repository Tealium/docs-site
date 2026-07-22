---
title: Quantcast Easy Tag for Measure構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuantcast Easy Tag for Measureを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-easy-tag-for-measure/
---
## タグのヒント

* マッピングを使用して、アカウントの標準構成値を動的に上書きします。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Quantcast Easy Tag for Measureタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **アカウントコード**
  * アカウントコード（P-code）。
  * `p-`で始まる13文字の大文字小文字を区別する英数字のコード。
  * 質問がある場合は、Quantcastの担当者にお問い合わせください。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`qacct`|  <ul><li>アカウントコード（P-code）。</li><li>`p-`で始まる13文字の大文字小文字を区別する英数字のコード。</li></ul> |
