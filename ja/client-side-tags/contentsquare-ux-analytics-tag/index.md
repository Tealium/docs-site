---
title: Contentsquare UXアナリティクスタグ構成ガイド
description: この記事では、Contentsquare UXアナリティクスタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/contentsquare-ux-analytics-tag/
---
## タグのヒント
*   `ecommerce:addTransaction` イベントは、注文IDが構成されたときに追跡されます。
*   バッジをマッピングするときは、Contentsquareに表示される名前を入力してください。
*   **Send All Audiences** を `true` に構成すると、各オーディエンスを `_uxa.push([&#34;trackDynamicVariable&#34;, {key: &#34;CDP_TL_Audience ID : AUDIENCE_ID&#34;, value: &#34;AUDIENCE_NAME&#34;}]);` の形式でContentsquareに送信します。
*   サポートされているEコマース拡張パラメーター（\*トランザクションに必須）:
    *   注文ID (`_corder`) \*
    *   注文合計 (`_ctotal`) \*
    *   配送料 (`_cship`)
    *   税額 (`_ctax`)
    *   注文通貨 (`_ccurrency`)
    *   製品IDリスト (`_cprod`)
    *   名前リスト (`_cprodname`) \*
    *   SKUリスト (`_csku`) \*
    *   カテゴリリスト (`_ccat`)
    *   数量リスト (`_cquan`) \*
    *   価格リスト (`_cprice`) \*

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Main Tag ID**: あなたのウェブサイトに特有のメインタグID。
* **WebView Tag ID**: あなたのウェブサイトに特有のタグWebView ID。
* **Send All Audiences**: `True` を選択して、各オーディエンスを `_uxa.push([&#34;trackDynamicVariable&#34;, {key: &#34;Tealium Audience AUDIENCE ID&#34;, value: &#34;AUDIENCE NAME&#34;}]);` の形式でContentsquareに送信します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `id_project` | `String` | メインタグID |
| `webview_id_project` | `String` | WebViewタグID |
| `send_audiences` | `String` | すべてのオーディエンスを送信 |

### Eコマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文ID（`_corder`を上書き） |
| `order_total` | `Number`  | 注文合計（`_ctotal`を上書き） |
| `order_currency` | `String` | 通貨（`_ccurrency`を上書き） |
| `product_id` | `Array` | 製品IDリスト（`_cprod`を上書き） |
| `product_name` | `Array` | 名前リスト（`_cprodname`を上書き） |
| `product_sku` | `Array` | SKUリスト（`_csku`を上書き） |
| `product_category` | `Array` | カテゴリリスト（`_ccat`を上書き） |
| `product_quantity` | `Array` | 数量リスト（`_cquan`を上書き） |
| `product_unit_price` | `Array` | 価格リスト（`_cprice`を上書き） |

### バッジ

バッジをマッピングするには、Contentsquareに表示される名前を入力します。この名前は、`_uxa.push([&#34;trackDynamicVariable&#34;, { &#34;key&#34; : &#34;CDP_TL_Badge ID : BADGE_NAME&#34;, &#34;value&#34; : BADGE_VALUE`の`key`として使用されます。

### 動的変数

動的変数をマッピングするには、Contentsquareが期待する変数名を入力します。この変数名は、`_uxa.push([&#34;trackDynamicVariable&#34;, { &#34;key&#34;: &#34;my_key&#34;, &#34;value&#34;: my_value }]);`の`key`として使用されます。