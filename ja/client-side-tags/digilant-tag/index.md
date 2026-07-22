---
title: Digilantタグ構成ガイド
description: この記事では、Digilantタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/digilant-tag/
---
## タグのヒント

* 標準構成でPixel IDを指定します。
* マッピングを通じて標準構成のPixel IDを上書きします。
* ライブラリを同期的にロードする必要がある場合は、**Advanced Settings**で**Synchronous Load Type**を構成します。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Digilantタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **タグバージョン**
* **Pixel ID**：

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`id`| Pixel ID|

