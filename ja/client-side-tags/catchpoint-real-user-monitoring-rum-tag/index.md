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

まず、Tealiumのタグマーケットプレイスにアクセスし、Catchpoint リアルユーザーモニタリング（RUM）タグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照）。

タグを追加した後、以下の構成を構成します：

* **REST URL**
  * タグスニペットで提供されるURL。
  * 例：`g.3gl.net/jp/xxx/v3/M`

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `pageGroup_token` |  <ul><li>ページグループトークン。</li></ul> |
| `variation_token` |  <ul><li>バリエーションタグトークン。</li></ul> |
| `indicator_token` |  <ul><li>インジケータータグトークン。</li></ul> |
| `indicator_value` |  <ul><li>インジケーター値。</li></ul> |
| `tracepoint_token` |  <ul><li>トレースポイントトークン。</li></ul> |
|`tracepoint_value`|  <ul><li>トレースポイント値。</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
| `order_id` |  <ul><li>注文ID。</li><li>`_corder`を上書き。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>`_csubtotal`を上書き。</li></ul> |
|`product_quantity`|  <ul><li>配列。</li><li>数量リスト。</li><li>`_cquan`を上書き。</li></ul> |