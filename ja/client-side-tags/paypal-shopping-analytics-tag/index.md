---
title: PayPal Shopping Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでPayPal Shopping Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/paypal-shopping-analytics-tag/
---
SDKは、Webサイトの訪問から分析データを収集します。PayPalはこのデータを使用して、途中で離脱した訪問をリターゲティングするためのオプションを提供します。

## タグに関するヒント

* マッピングは、以下の目的で使用します。   
- 構成データを動的に上書きする   
- Eコマース拡張機能の値を動的に上書きする   
- イベントをトリガーする

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **クライアントID**：マーチャントの場合は、本番環境のクライアントIDです。パートナーの場合は、パートナーのクライアントIDです。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 構成

|変数|説明|
|---|---|
|画面名 (client\_id)（必須）|文字列|
|ユーザーID (user\_id)|文字列|
|初回訪問 (first\_time\_visit)|[ブール値]|

### ページビュー

|変数|説明|
|---|---|
|ページタイプ (page\_type)（必須）|文字列|
|ページ名 (page\_name)|文字列|
|ページパス (page\_path)|文字列|
|ページカテゴリー名 (page\_category\_name)|文字列|
|ページカテゴリーID (page\_category\_id)|文字列|
|ディールID (deal\_id)|文字列|
|ディール名 (deal\_name)|文字列|
|ディール値 (deal\_value)|文字列|
|検索結果数 (search\_results\_count)|文字列|

### 商品ビュー

|変数|説明|
|---|---|
|商品ID (product\_id) |（必須）文字列（\_cprodを上書き）|
|商品名 (product\_name) |文字列（\_cprodnameを上書き）|
|商品URL (product\_url)|文字列|
|商品価格 (product\_price) |文字列（\_cpriceを上書き）|
|商品ブランド (product\_brand) |文字列（\_cbrandを上書き）|
|商品カテゴリー名 (product\_category\_name)|文字列（\_ccatを上書き）|
|商品カテゴリーID (product\_category\_id)|文字列|
|商品割引 (product\_discount) |文字列（\_cpdiscを上書き）|

### イベント

|変数|説明|
|---|---|
|ページビュー (page\_view)|page\_view|
|商品ビュー (product\_view)|product\_view|