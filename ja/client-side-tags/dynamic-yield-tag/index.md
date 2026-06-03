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

まず、Tealiumのタグマーケットプレイスに移動し、ダイナミックイールドタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Site ID**: ダイナミックイールドから提供されたSite IDまたはscsec

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数             | 説明                                                |
|:-----------------|:----------------------------------------------------|
| `SiteID`         | &lt;ul&gt;&lt;li&gt;(`scsec`)&lt;/li&gt;&lt;/ul&gt;                         |
| `evt_list`       | &lt;ul&gt;&lt;li&gt;CSV/Array&lt;/li&gt;&lt;li&gt;発火するイベントのリスト&lt;/li&gt;&lt;/ul&gt; |
| `context.type`   | &lt;ul&gt;&lt;li&gt;コンテキストタイプ&lt;/li&gt;&lt;/ul&gt;                 |
| `context.data`   | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;/ul&gt;    |

### E-Commerce

| 変数                 | 説明                                                                      |
|:---------------------|:---------------------------------------------------------------------------------|
| `order_id`           | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                          |
| `order_total`        | &lt;ul&gt;&lt;li&gt;注文合計&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                       |
| `order_subtotal`     | &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                       |
| `order_currency`     | &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                       |
| `product_id`         | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_name`       | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt;   |
| `product_quantity`   | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt;  |
| `product_unit_price` | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt;     |

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

