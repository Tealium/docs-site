---
title: Salsifyタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSalsifyタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salsify-tag/
---
Salsify Enhanced Contentは、ブランドが統一されたソリューションを構築し、説得力のある下部のブランド体験を公開し、コンバージョン率を向上させるためのものです。Enhanced Contentを使用すると、Salsifyのサプライヤーやブランドから画像、ビデオ、比較チャート、インタラクティブな製品ツアーを受け取ることができます。

Enhanced Contentは、Salsifyが提供するJavaScriptタグまたはNPM統合を通じて提供することができます。

## タグのヒント

* 以下のE-Commerce拡張値をサポートしています：
  * 商品ID
  * 商品カテゴリ
  * 商品の数量
  * 商品ブランド
  * 商品価格

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[Tag Overview]()の記事を参照してください。

タグを追加した後、以下の構成を行います：

* **クライアントID**：あなたのSalsify Experiences SDKクライアントID。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能な宛先カテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|クライアントID| (`clientId`)|
|IDタイプ| (`idType`)|
|Enhanced Content Container| (`enhancedContentContainer`)|

### E-Commerce

|変数| 説明|
|---| ---|
|商品ID (`productId`) (`_cprod`を上書き)| [配列]|
|商品カテゴリ (`category`) (`_ccat`を上書き)| [配列]|
|商品の数量 (`quantity`) (`_cquan`を上書き)| [配列]|
|商品ブランド (`brand`) (`_cbrand`を上書き)| [配列]|
|商品価格 (`price`) (`_cprice`を上書き)| [配列]|

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

