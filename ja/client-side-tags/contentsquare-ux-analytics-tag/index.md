---
title: Contentsquare UX Analyticsタグ構成ガイド
description: この記事では、Contentsquare UX Analyticsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/contentsquare-ux-analytics-tag/
---
## タグに関するヒント
*   注文IDが構成されると、`ecommerce:addTransaction`イベントがトラッキングされます。
*   バッジをマッピングする場合は、Contentsquareに表示する名前を入力します。
*   各オーディエンスを`_uxa.push(["trackDynamicVariable", {key: "CDP_TL_Audience ID : AUDIENCE_ID", value: "AUDIENCE_NAME"}]);`の形式でContentsquareに送信するには、**Send All Audiences**を`true`に構成します。
*   サポートされているEコマース拡張機能のパラメータ（\*はトランザクションに必須）：
    *   注文ID（`_corder`）\*
    *   注文合計（`_ctotal`）\*
    *   配送料（`_cship`）
    *   税額（`_ctax`）
    *   注文通貨（`_ccurrency`）
    *   製品IDのリスト（`_cprod`）
    *   名前のリスト（`_cprodname`）\*
    *   SKUのリスト（`_csku`）\*
    *   カテゴリのリスト（`_ccat`）
    *   数量のリスト（`_cquan`）\*
    *   価格のリスト（`_cprice`）\*

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の項目を構成します。

* **Main Tag ID**：Webサイト固有のメインタグID。
* **WebView Tag ID**：Webサイト固有のタグWebView ID。
* **Send All Audiences**：各オーディエンスを`_uxa.push(["trackDynamicVariable", {key: "Tealium Audience AUDIENCE ID", value: "AUDIENCE NAME"}]);`の形式でContentsquareに送信するには、`True`を選択します。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングにより、データレイヤー変数の値がベンダータグ内の対応する変数に送信されます。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `id_project` | `String` | メインタグID |
| `webview_id_project` | `String` | WebViewタグID |
| `send_audiences` | `String` | すべてのオーディエンスを送信 |

### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文ID（`_corder`を上書き） |
| `order_total` | `Number`  | 注文合計（`_ctotal`を上書き） |
| `order_currency` | `String` | 通貨（`_ccurrency`を上書き） |
| `product_id` | `Array` | 製品IDのリスト（`_cprod`を上書き） |
| `product_name` | `Array` | 名前のリスト（`_cprodname`を上書き） |
| `product_sku` | `Array` | SKUのリスト（`_csku`を上書き） |
| `product_category` | `Array` | カテゴリのリスト（`_ccat`を上書き） |
| `product_quantity` | `Array` | 数量のリスト（`_cquan`を上書き） |
| `product_unit_price` | `Array` | 価格のリスト（`_cprice`を上書き） |

### バッジ

バッジをマッピングするには、Contentsquareに表示する名前を入力します。この名前は、`_uxa.push(["trackDynamicVariable", { "key" : "CDP_TL_Badge ID : BADGE_NAME", "value" : BADGE_VALUE`を呼び出す際に`key`で使用されます。

### 動的変数

動的変数をマッピングするには、Contentsquareで想定されている変数名を入力します。この変数名は、`_uxa.push(["trackDynamicVariable", { "key": "my_key", "value": my_value }]);`を呼び出す際に`key`として使用されます。