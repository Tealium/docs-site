---
title: Lucky Orangeタグ構成ガイド
description: この記事では、タグ管理アカウントでLucky Orangeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/lucky-orange-tag/
---
## タグに関するヒント

* マッピングを使用して、タグ構成を上書きしたり動的に構成したりできます。
* カスタムイベントを使用して、必要なイベントの名前を入力します。
* カスタムパラメータは必要な数だけ使用できます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を行います。

* **サイトID**：（必須）クライアントのサイトを一意に識別するID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `site_id` | `String` | サイトID |
| `customer_id` | `String` | 顧客を識別するための訪問ID |
| `email` | `String` | 顧客のメールアドレス |
| `phone` | `String` | 顧客の電話番号 |
| `name` | `String` | 顧客名 |
| `identify.custom` | `String` | カスタム識別フィールド |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `site_id` | サイトID |
| `customer_id` | 顧客を識別するための訪問ID |
| `email` | 顧客のメールアドレス |
| `phone` | 顧客の電話番号 |
| `name` | 顧客名 |