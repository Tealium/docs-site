---
title: Neustar IDMP Site Activityタグ構成ガイド
description: この記事では、Neustar Identity Management Platform（IDMP）Site Activityタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/neustar-idmp-site-activity-tag/
---
Neustar IDMP Site Activityタグを使用すると、コンバージョンイベントなど、Webサイト上でのユーザー行動を追跡できます。

## タグに関するヒント

* タグ構成で**ピクセルタイプ**を選択し、適切なスクリプトタイプを読み込みます。
* マッピングを使用して、タグ構成を上書きし、動的に構成します。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **NeustarタグID**：Neustar IDMPタグの数値。
* **ピクセルタイプ**：画像またはiframeのどちらのタグタイプを生成するかを選択します。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `pixelId`  | 文字列 | ピクセルID |
|  `pixelType`  | 文字列 | ピクセルタイプ |

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `che`  | 文字列 | キャッシュバスター |
|  `rev`  | 数値 | 収益 |
|  `cur`  | 文字列 | 通貨コード |
|  `qty`  | 数値 | 注文数 |
|  `type`  | 文字列 | タイプ |
|  `ord`  | 文字列 | 注文ID |
|  `uid`  | 文字列 | サードパーティユーザーID |
|  `dedup`  | 文字列 | 重複排除ID |
|  `ip`  | 文字列 | IPアドレス |