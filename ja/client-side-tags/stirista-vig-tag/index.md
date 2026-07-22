---
title: Stirista VIGタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでStirista VIGタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/stirista-vig-tag/
---
## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Stirista VIGタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **フィールドi**
  * 生成されたコードスニペットに見つかる英数字の値。
  * 例：`i=000a000b123c`

* **フィールドs**
  * 生成されたコードスニペットに見つかる英数字の値。
  * 例：`s=000a000b123c`

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`i`| マッピングが必要です。|
|`t`| マッピングが必要です。|
|`p`| マッピングが必要です。|
|`s`| マッピングが必要です。|
|`r`| マッピングが必要です。|
|`u`| マッピングが必要です。|
