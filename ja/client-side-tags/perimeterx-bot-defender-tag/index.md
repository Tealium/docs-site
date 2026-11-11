---
title: PerimeterX Bot Defenderタグ構成ガイド
description: この記事では、タグ管理アカウントでPerimeterX Bot Defenderタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/perimeterx-bot-defender-tag/
---
## タグ構成のヒント

* マッピングを使用すると、標準構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **AppID**：一意のアプリケーション識別子

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`appId`|<ul><li>AppID</li></ul>|
|`_pxParam1`|<ul><li>カスタムパラメーター1</li></ul>|
|`_pxParam2`|<ul><li>カスタムパラメーター2</li></ul>|
|`_pxParam3`|<ul><li>カスタムパラメーター3</li></ul>|
|`_pxParam4`|<ul><li>カスタムパラメーター4</li></ul>|