---
title: ラッキーオレンジタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでラッキーオレンジタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/lucky-orange-tag/
---
## タグのヒント

*   マッピングを使用してタグ構成を上書きし、動的に構成します。
*   カスタムイベントを使用して必要なイベントの名前を入力します。
*   必要なだけカスタムパラメータを使用できます。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **サイトID**：必須。クライアントのサイトの一意の識別子。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `site_id` | `String` | サイトID |
| `customer_id` | `String` | 顧客を識別するための訪問ID |
| `email` | `String` | 顧客のメールアドレス |
| `phone` | `String` | 顧客の電話番号 |
| `name` | `String` | 顧客の名前 |
| `identify.custom` | `String` | カスタム識別フィールド |

### イベント固有のパラメータ

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `site_id` | サイトID |
| `customer_id` | 顧客を識別するための訪問ID |
| `email` | 顧客のメールアドレス |
| `phone` | 顧客の電話番号 |
| `name` | 顧客の名前 |

