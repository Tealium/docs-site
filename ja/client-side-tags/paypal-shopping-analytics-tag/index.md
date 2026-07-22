---
title: PayPalショッピングアナリティクスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPayPalショッピングアナリティクスタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/paypal-shopping-analytics-tag/
---
SDKは、ウェブサイトの訪問から分析データを収集します。このデータはPayPalによって、離脱する訪問を再ターゲティングするオプションを提供するために使用されます。

## タグのヒント

* マッピングを使用して：   
- 構成データを動的に上書きする   
- E-Commerce拡張値を動的に上書きする   
- イベントトリガー

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **クライアントID**：マーチャントの場合、これは本番クライアントIDです。パートナーの場合、これはパートナークライアントIDです。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。変数をタグの宛先にマップする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 構成

|変数| 説明|
|---| ---|
|スクリーン名 (client\_id) (必須)| 文字列|
|ユーザーID (user\_id)| 文字列|
|初回訪問 (first\_time\_visit)| [ブーリアン]|

### ページビュー

|変数| 説明|
|---| ---|
|ページタイプ (page\_type) (必須)| 文字列|
|ページ名 (page\_name)| 文字列|
|ページパス (page\_path)| 文字列|
|ページカテゴリ名 (page\_category\_name)| 文字列|
|ページカテゴリID (page\_category\_id)| 文字列|
|ディールID (deal\_id)| 文字列|
|ディール名 (deal\_name)| 文字列|
|ディール値 (deal\_value)| 文字列|
|検索結果数 (search\_results\_count)| 文字列|

### 商品ビュー

|変数| 説明|
|---| ---|
|商品ID (product\_id) (必須)| 文字列 (\_cprodを上書き)|
|商品名 (product\_name) | 文字列 (\_cprodnameを上書き)|
|商品URL (product\_url)| 文字列|
|商品価格 (product\_price) | 文字列 (\_cpriceを上書き)|
|商品ブランド (product\_brand) | 文字列 (\_cbrandを上書き)|
|商品カテゴリ名 (product\_category\_name)| 文字列 (\_ccatを上書き)|
|商品カテゴリID (product\_category\_id)| 文字列 |
|商品割引 (product\_discount) | 文字列 (\_cpdiscを上書き)|

### イベント

|変数| 説明|
|---| ---|
|ページビュー (page\_view)| page\_view|
|商品ビュー (product\_view)| product\_view|


