---
title: Catchpoint リアルユーザーモニタリング（RUM）タグ構成ガイド
description: この記事では、Catchpoint リアルユーザーモニタリングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/catchpoint-real-user-monitoring-rum-tag/
---
## タグのヒント

* ページグループ、バリエーション、インサイトインジケーター、トレースポイントを構成するためにマッピングを使用します。
* インサイトインジケーターとトレースポイントの値とトークンは、このデータをキャプチャするために変数が入力された状態でマッピングする必要があります。
* 注文IDが存在する場合、自動的にコンバージョンが発生します。
* 次のEコマース拡張パラメータをサポートします：
  * 注文ID（`_corder`）
  * 小計（`_csubtotal`）
  * 数量リスト（`_cquan`）

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスし、Catchpoint リアルユーザーモニタリング（RUM）タグを追加します（[タグの追加方法についてはこちら]()を参照）。

タグを追加した後、以下の構成を構成します：

* **REST URL**
  * タグスニペットで提供されるURL。
  * 例：`g.3gl.net/jp/xxx/v3/M`

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `pageGroup_token` |  &lt;ul&gt;&lt;li&gt;ページグループトークン。&lt;/li&gt;&lt;/ul&gt; |
| `variation_token` |  &lt;ul&gt;&lt;li&gt;バリエーションタグトークン。&lt;/li&gt;&lt;/ul&gt; |
| `indicator_token` |  &lt;ul&gt;&lt;li&gt;インジケータータグトークン。&lt;/li&gt;&lt;/ul&gt; |
| `indicator_value` |  &lt;ul&gt;&lt;li&gt;インジケーター値。&lt;/li&gt;&lt;/ul&gt; |
| `tracepoint_token` |  &lt;ul&gt;&lt;li&gt;トレースポイントトークン。&lt;/li&gt;&lt;/ul&gt; |
|`tracepoint_value`|  &lt;ul&gt;&lt;li&gt;トレースポイント値。&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

|変数| 説明|
|---| ---|
| `order_id` |  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計。&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;数量リスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書き。&lt;/li&gt;&lt;/ul&gt; |