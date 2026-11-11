---
title: The Trade Deskリアルタイムコンバージョンイベントタグ構成ガイド
description: この記事では、タグ管理アカウントでThe Trade Deskリアルタイムコンバージョンイベントタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/the-trade-desk-real-time-conversion-events-tag/
---
## タグに関するヒント

* 注文IDが入力されると、購入トラッキングが自動的に行われます。
* イベントトラッキングIDフィールドには、イベントトラッキングIDをカンマ区切りのリストとして入力できます。
* マッピングを使用すると、次のことができます。
    * タグ構成を動的に指定する
    * Eコマース拡張機能の値を上書きする
* 次のEコマース拡張機能パラメータをサポートしています。
    * 注文ID
    * 小計
    * 通貨
    * 商品IDのリスト
    * 商品カテゴリーのリスト
    * 商品価格のリスト
    * 商品数量のリスト
    * 商品名のリスト

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **マーチャントID**：マーチャントIDは、オンボーディングプロセス中にThe Trade Deskから提供されます。
* **イベントトラッキングID**：プラットフォームUIで構成されたイベントトラッキングタグID（またはカンマ区切りのIDリスト）（`pixel_id`）。詳しくは、[The Trade Desk：リアルタイムコンバージョンイベント](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)を参照してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグ内の対応する変数に値を送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `pixel_id` | 文字列 | イベントトラッキングID。 |
| `merchant_id` | 文字列 | マーチャントID。 |

### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | 文字列 | 注文ID（`_corder`を上書き）。 |
| `value` | 文字列 | 小計（`_csubtotal`を上書き）。 |
| `currency` | 文字列 | 通貨（`_ccurrency`を上書き）。 |
| `items.cat` | 配列 | 商品カテゴリーのリスト（`_ccat`を上書き）。 |
| `items.item_code` | 配列 | 商品IDのリスト（`_cprod`を上書き）。 |
| `items.name` | 配列 | 商品名のリスト（`_cprodname`を上書き）。 |
| `items.qty` | 配列 | 商品数量のリスト（`_cquan`を上書き）。 |
| `items.price` | 配列 | 商品価格のリスト（`_cprice`を上書き）。 |

### ユーザーデータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `country` | 文字列 | 国。 |
| `region` | 文字列 | 地域。 |
| `metro` | 文字列 | 大都市圏。 |
| `city` | 文字列 | 市区町村。 |
| `zip` | 文字列 | 郵便番号。 |

### イベント

イベントのマッピング方法について詳しくは、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `addtocart` | カートに追加。 |
| `purchase` | 購入。 |
| `viewitem` | 商品を表示。 |
| `searchitem` | 商品を検索。 |
| `searchcategory` | カテゴリーを検索。 |
| `login` | ログイン。 |
| `messagebusiness` | ビジネスにメッセージを送信。 |
| `direction` | 道順。 |
| `startcheckout` | チェックアウトを開始。 |
| `viewcart` | カートを表示。 |
| `sitevisit` | サイト訪問。 |
| `wishlistitem` | ウィッシュリストの商品。 |

### イベント固有のパラメータ

イベントのマッピング方法について詳しくは、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `pixel_id` | イベントトラッキングID。 |
| `merchant_id` | マーチャントID。 |
| `order_id` | 注文ID。 |
| `value` | 小計。 |
| `currency` | 通貨。 |
| `items.item_code` | 商品IDのリスト。 |
| `items.name` | 商品名のリスト。 |
| `items.qty` | 商品数量のリスト。 |
| `items.price` | 商品価格のリスト。 |
| `country` | 国。 |
| `region` | 地域。 |
| `metro` | 大都市圏。 |
| `city` | 市区町村。 |
| `zip` | 郵便番号。 |
| `td1` | カスタムパラメータtd1。 |
| `td2` | カスタムパラメータtd2。 |
| `td3` | カスタムパラメータtd3。 |
| `td4` | カスタムパラメータtd4。 |
| `td5` | カスタムパラメータtd5。 |
| `td6` | カスタムパラメータtd6。 |
| `td7` | カスタムパラメータtd7。 |
| `td8` | カスタムパラメータtd8。 |
| `td9` | カスタムパラメータtd9。 |
| `td10` | カスタムパラメータtd10。 |
| `addtocart` | カートに追加。 |
| `purchase` | 購入。 |
| `viewitem` | 商品を表示。 |
| `searchitem` | 商品を検索。 |
| `searchcategory` | カテゴリーを検索。 |
| `login` | ログイン。 |
| `messagebusiness` | ビジネスにメッセージを送信。 |
| `direction` | 道順。 |
| `startcheckout` | チェックアウトを開始。 |
| `viewcart` | カートを表示。 |
| `sitevisit` | サイト訪問。 |
| `wishlistitem` | ウィッシュリストの商品。 |

### カスタムパラメータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `td1` | 文字列 | カスタムパラメータtd1。 |
| `td2` | 文字列 | カスタムパラメータtd2。 |
| `td3` | 文字列 | カスタムパラメータtd3。 |
| `td4` | 文字列 | カスタムパラメータtd4。 |
| `td5` | 文字列 | カスタムパラメータtd5。 |
| `td6` | 文字列 | カスタムパラメータtd6。 |
| `td7` | 文字列 | カスタムパラメータtd7。 |
| `td8` | 文字列 | カスタムパラメータtd8。 |
| `td9` | 文字列 | カスタムパラメータtd9。 |
| `td10` | 文字列 | カスタムパラメータtd10。 |