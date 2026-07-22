---
title: Pixibo FYFタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントで"Find your Fit" pixibo.fyfタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pixibo-fyf-tag/
---## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* タグを発火させるためには、マッピングのSKU IDが必要です。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **クライアント名**
* **クライアントID**
* **環境**
  * スクリプトの環境を指定するために使用します。
* **言語**
  * 任意
  * ウィジェットを読み込む言語。
  * デフォルト値は英語（`en`）です。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`clientName`|  <ul><li>クライアント名</li></ul> |
|`clientId`|  <ul><li>クライアントID</li></ul> |
|`environment`|  <ul><li>環境</li></ul> |
|`skuId`|  <ul><li>SKU ID</li></ul> |
|`lang`|  <ul><li>言語</li></ul> |

