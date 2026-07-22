---
title: エプシロンサイトタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでエプシロンサイトタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/epsilon-universal-site-tag/
---
## タグ構成

タグマーケットプレイスに移動し、エプシロンサイトタグを追加します。タグの追加についての詳細は、[manage-tags](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加した後、以下の構成を行います：

* **ドメインとタグパス**：タグ内で使用されるドメイン。エプシロンから提供されたタグ付けドキュメントを参照してください。
* **リバースプロキシディレクトリパス**：リバースプロキシを使用している場合は、そのパスを入力します（例：`/tag_path`、またはリバースプロキシのルートとして構成したカスタムパス）。
* **会社ID**：会社ID `dtm_cid`。
* **セカンダリ会社ID**：`dtm_cmagic`。
* **フォームID**：`dtm_fid`。
* **統合タイプ**：利用可能な構成は`Default`または`Limited`です。Limited統合はエプシロンに指定された場合のみ使用すべきです。
* **SPAサポート**：有効にすると、`dtm_clear_tag=all`クエリストリングパラメータがすべてのリクエストに含まれます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

|変数| タイプ | 説明|
|---| ---|---|
| `tag_domain`| String| ドメイン。|
| `tag_path`| String| リバースプロキシディレクトリパス。|
| `dtm_cid`| String| 会社ID。|
| `dtm_cmagic`| String| セカンダリ会社ID。|
| `dtm_fid`| String| フォームID。|
| `integration_type`| Boolean| 統合タイプ。|
| `spa_support`| Boolean| SPAサポート。|

### スタンダード

|変数| タイプ | 説明|
|---| ---|---|
| `dtm_promo_id`| String| プロモID。|
|`dtmc_tcf_string`| String| GDPR同意文字列。|
|`dtm_email_hash`| String| メールハッシュ。|
| `dtm_user_id`| String| ユーザーID。|
| `custom.myvar`| String| カスタム。|
| `dtm_cookie_id` | String | Cookie IDをクエリパラメータとして送信します。 |

### ページ訪問

|変数| タイプ | 説明|
|---| ---|---|
| `dtmc_department`| String| 部門。|
| `dtmc_category`| String| カテゴリ。|
| `dtmc_sub_category`| String| サブカテゴリ。|
| `dtmc_product_id`| String| 製品ID。|
| `dtmc_brand`| String| メーカーブランド。|
| `dtmc_upc`| String| メーカーUPC。|
| `dtmc_mpn`| String| メーカーモデル部品番号。|

### コンバージョン

|変数| タイプ | 説明|
|---| ---|---|
| `dtmc_conv_type`| String| コンバージョンタイプ。|
| `dtmc_conv_store_location`| String| 店舗の場所。|
| `dtmc_transaction_id` (Overrides `_corder`| String| 注文ID。|
| `dtm_conv_val` (Overrides `_csubtotal`| String| 注文小計。|
| `dtm_conv_curr` (Overrides `_ccurrency`| String|  注文通貨。|
| `product_id` (Overrides `_cprod`| Array| 製品ID。|
| `product_quantity` (Overrides `_cquan`| Array| 製品数量。|
| `product_unit_price` (Overrides `_cprice`| Array| 製品価格。|
| `product_discount` (Overrides `_cpdisc`| Array| 製品割引額。|
|`dtm_items.myvar`| Array| カスタムアイテム属性。|