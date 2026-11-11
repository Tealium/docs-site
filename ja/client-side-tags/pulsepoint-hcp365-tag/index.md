---
title: PulsePoint HCP365 Pixelタグ構成ガイド
description: この記事では、PulsePoint HCP365 Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pulsepoint-hcp365-tag/
---
Signalプラットフォーム初のセルフサービス製品であるHCP365を使用すると、HCPオーディエンスがブランドのデジタルタッチポイントに自然に関与しているユーザー、方法、タイミングをNPIレベルで把握できます。HCP365 Pixelは、ページレベルの情報をPulsePointシステムに送信します。

## タグに関するヒント

* 標準パラメータを上書きするには、マッピングを使用します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **PulsePoint Container Pixel**：クライアントごとに固有のPulsePointコンテナピクセル
* **Token**：ブランドのPulsePoint内部識別子（たとえば、Merck広告主が複数のブランドを所有している場合は、複数のトークンを使用します）

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
| --- | --- |
| PulsePointコンテナピクセル（`p`） | `String` |
| トークン（`token`） | `String` |
| ベースURL（`base_url`） | `String` |
| CCPAオプトアウト（`us_privacy`）（必須） | `String` |
| タグが発火したページのURL（`url`）（必須） | `String` |
| ページのリファラー（`rr`）（必須） | `String` |
| ピクセルに追加情報を渡すための追加パラメータ（`param1`） | `String` |
| ピクセルに追加情報を渡すための追加パラメータ（`param2`） | `String` |
| ピクセルに追加情報を渡すための追加パラメータ（`param3`） | `String` |
| ピクセルに追加情報を渡すための追加パラメータ（`param4`） | `String` |
| ピクセルに追加情報を渡すための追加パラメータ（`param5`） | `String` |
| フォーム送信時にタグが発火した場合のフォーム詳細（`frmtext`） | `String` |
| クリックされたリンクのリンクテキスト、またはダウンロードされたドキュメントのドキュメント名（`clktext`） | `String` |