---
title: Top.Mail.ruタグ構成ガイド
description: この記事では、タグ管理アカウントでTop.Mail.ruタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/topmailru-tag/
---
## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **カウンターID**：（必須）Top.Mail.ruのカウンターID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `base_url` | 文字列 | ベースURL |
| `id` | 文字列 | カウンターID |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `productid` | 文字列 | 商品ID |
| `value` | 文字列 | 値 |
| `pagetype` | 文字列 | ページタイプ |
| `list` | 文字列 | リスト |
| `userid` | 文字列 | ユーザーID |
| `totalvalue` | 数値または文字列 | 合計値 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `pageView` | 文字列 | ページビュー |
| `viewProduct` | 文字列 | 商品の表示 |
| `addToCart` | 文字列 | カートに追加 |
| `purchase` | 文字列 | 購入 |
| `itemView` | 文字列 | アイテムの表示 |
| `custom` | 文字列 | カスタム |

### イベント固有のパラメーター

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `productid` | 文字列 | 商品ID |
| `value` | 文字列 | 値 |
| `pagetype` | 文字列 | ページタイプ |
| `list` | 文字列 | リスト |
| `userid` | 文字列 | ユーザーID |
| `totalvalue` | 数値または文字列 | 合計値 |
| `custom_parameter` | 文字列 | カスタムパラメーター |
| `pageView` | 文字列 | ページビュー |
| `viewProduct` | 文字列 | 商品の表示 |
| `addToCart` | 文字列 | カートに追加 |
| `purchase` | 文字列 | 購入 |
| `custom_event` | 文字列 | カスタムイベント |