---
title: Neustar PageAdvisor タグ構成ガイド
description: この記事では、Neustar PageAdvisor タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/neustar-pageadvisor-tag/
---
## タグに関するヒント

* マッピングを使用して、標準構成値を動的に上書きします。
* カスタム変数を使用して、動的な値を割り当てます。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **サービスID（sid）**：Neustarがクライアントを識別するための10桁の数値（例：`9876543210`）。
* **ページ参照（page）**：ユーザーがどのページを閲覧しているかをクライアントが示すために使用する参照（例：`http://www.neustar.biz`）。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
|   `service_id` | サービスID |
|   `page_ref` | ページ参照 |
|   `cv1` | カスタム変数 |