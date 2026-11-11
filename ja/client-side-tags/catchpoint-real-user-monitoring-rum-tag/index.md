---
title: Catchpoint リアルユーザーモニタリング（RUM）タグ構成ガイド
description: この記事では、Catchpoint リアルユーザーモニタリングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/catchpoint-real-user-monitoring-rum-tag/
---
## タグに関するヒント

* マッピングを使用して、ページグループ、バリエーション、インサイトインジケーター、およびトレースポイントを構成します。
* インサイトインジケーターとトレースポイントのデータを取得するには、値とトークンの両方を、値が構成された変数にマッピングする必要があります。
* 注文 ID が存在する場合、コンバージョンが自動的に発生します。
* 次の E コマース拡張パラメータをサポートしています。
  * 注文 ID（`_corder`）
  * 小計（`_csubtotal`）
  * 数量のリスト（`_cquan`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **REST URL**
  * タグスニペットで提供される URL。
  * 例：`g.3gl.net/jp/xxx/v3/M`

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
| `pageGroup_token` | <ul><li>ページグループトークン。</li></ul> |
| `variation_token` | <ul><li>バリエーションタグトークン。</li></ul> |
| `indicator_token` | <ul><li>インジケータータグトークン。</li></ul> |
| `indicator_value` | <ul><li>インジケーター値。</li></ul> |
| `tracepoint_token` | <ul><li>トレースポイントトークン。</li></ul> |
|`tracepoint_value`| <ul><li>トレースポイント値。</li></ul> |

### E コマース

|変数|説明|
|---|---|
| `order_id` | <ul><li>注文 ID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`| <ul><li>小計。</li><li>`_csubtotal`を上書きします。</li></ul> |
|`product_quantity`| <ul><li>配列。</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |