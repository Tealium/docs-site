---
title: Salsifyタグ構成ガイド
description: この記事では、タグ管理アカウントでSalsifyタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salsify-tag/
---
Salsify Enhanced Contentは、ブランドがコンバージョン率を向上させる、信頼性の高い魅力的なファーストビュー以降のブランド体験を構築し、公開するための統合ソリューションです。Enhanced Contentを使用すると、Enhanced Contentサービスを利用しているSalsifyのサプライヤーやブランドから、画像、動画、比較表、インタラクティブな製品ツアーを受け取ることができます。

Enhanced Contentは、Salsifyが提供するJavaScriptタグまたはNPM連携を通じて配信できます。

## タグに関するヒント

* 次のEコマース拡張機能の値をサポートしています。
  * 製品ID
  * 製品カテゴリ
  * 製品数量
  * 製品ブランド
  * 製品価格

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **クライアントID**：Salsify Experiences SDKのクライアントID。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能な送信先カテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|クライアントID| (`clientId`)|
|IDタイプ| (`idType`)|
|Enhanced Contentコンテナ| (`enhancedContentContainer`)|

### Eコマース

|変数| 説明|
|---| ---|
|製品ID（`productId`）（`_cprod`をオーバーライド）| [配列]|
|製品カテゴリ（`category`）（`_ccat`をオーバーライド）| [配列]|
|製品数量（`quantity`）（`_cquan`をオーバーライド）| [配列]|
|製品ブランド（`brand`）（`_cbrand`をオーバーライド）| [配列]|
|製品価格（`price`）（_cprice`をオーバーライド）| [配列]|

### イベント

|変数| 説明|
|---| ---|
|カートに追加| `addToCart`|
|ページナビゲーション| `navigation`|

### イベント固有のパラメータ

|変数| 説明|
|---| ---|
|カートに追加| `addToCart`|
|ページナビゲーション| `navigation`|