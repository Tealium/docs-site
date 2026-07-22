---
title: Dynamic Yield タグ構成ガイド
description: この記事では、ダイナミックイールドタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dynamic-yield-tag/
---
## タグのヒント

* 名前とプロパティを構成できます。
* マッピングツールボックス内のカスタムイベントデータタブで、カスタムイベントのタイプパラメータをマッピングできます。
* Order IDが構成されるとコンバージョンが発生します。
* 以下のE-Commerce拡張パラメータをサポートしています：
  * Order ID (`_corder`)
  * Order Total (`_ctotal`)
  * Sub Total (`_csubtotal`)
  * Currency (`_ccurrency`)
  * List of Product IDs (`_cprod`)
  * List of Names `_cprodname`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、ダイナミックイールドタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Site ID**: ダイナミックイールドから提供されたSite IDまたはscsec

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数             | 説明                                                |
|:-----------------|:----------------------------------------------------|
| `SiteID`         | <ul><li>(`scsec`)</li></ul>                         |
| `evt_list`       | <ul><li>CSV/Array</li><li>発火するイベントのリスト</li></ul> |
| `context.type`   | <ul><li>コンテキストタイプ</li></ul>                 |
| `context.data`   | <ul><li>配列</li><li>コンテキストデータ</li></ul>    |

### E-Commerce

| 変数                 | 説明                                                                      |
|:---------------------|:---------------------------------------------------------------------------------|
| `order_id`           | <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul>                          |
| `order_total`        | <ul><li>注文合計</li><li>`_ctotal`を上書きします。</li></ul>                       |
| `order_subtotal`     | <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul>                       |
| `order_currency`     | <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul>                       |
| `product_id`         | <ul><li>配列</li><li>製品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
| `product_name`       | <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li></ul>   |
| `product_quantity`   | <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul>  |
| `product_unit_price` | <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul>     |

### イベント

| 変数               | 説明          |
|:-------------------|:--------------|
| `AddToCart`        | カートに追加  |
| `RemoveFromCart`   | カートから削除 |
| `Search`           | 検索          |
| `EmailSignup`      | メール登録    |
| `VideoWatch`       | ビデオ視聴    |
| `Custom`           | カスタム      |

### パラメータ

| 変数                         | 説明                  |
|:-----------------------------|:----------------------|
| サイズ (`size`)              | `properties.size`     |
| 検索キーワード (`keywords`)  | `properties.keywords` |
| ハッシュ化されたメール (`hashedEmail`) | `properties.hashedEmail` |
| カスタム                     | カスタム              |

### ビデオパラメータ

| 変数                                       | 説明                  |
|:-------------------------------------------|:----------------------|
| アイテムID                                 | `properties.itemId`   |
| カテゴリ (`categories`)                    | `properties.categories` |
| 自動再生 (`autoplay`) [`true`/`false`]     | `properties.autoplay` |
| 進行状況 (`progress`)                      | `properties.progress` |
| 進行状況のパーセンテージ (`progressPercent`) | `properties.progressPercent` |
| カスタム                                   | カスタム              |

