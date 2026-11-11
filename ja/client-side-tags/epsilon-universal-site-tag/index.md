---
title: Epsilon Siteタグ構成ガイド
description: この記事では、タグ管理アカウントでEpsilon Siteタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/epsilon-universal-site-tag/
---
## タグ構成

タグマーケットプレイスに移動し、Epsilon Siteタグを追加します。タグの追加の詳細については、[manage-tags](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **ドメインとタグパス**：タグ内で使用するドメイン。Epsilonから提供されたタグ構成ドキュメントを参照してください。
* **リバースプロキシのディレクトリパス**：リバースプロキシを使用している場合は、そのパス（例：`/tag_path`、またはリバースプロキシのルートとして構成したカスタムパス）を入力します。
* **会社ID**：会社ID `dtm_cid`。
* **セカンダリ会社ID**：`dtm_cmagic`。
* **フォームID**：`dtm_fid`。
* **統合タイプ**：使用可能な構成は`Default`または`Limited`です。限定的な統合は、Epsilonから指定された場合にのみ使用してください。
* **SPAサポート**：有効にすると、すべてのリクエストに`dtm_clear_tag=all`クエリ文字列パラメーターが含まれます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成

|変数| 型 | 説明|
|---| ---|---|
| `tag_domain`| 文字列| ドメイン。|
| `tag_path`| 文字列| リバースプロキシのディレクトリパス。|
| `dtm_cid`| 文字列| 会社ID。|
| `dtm_cmagic`| 文字列| セカンダリ会社ID。|
| `dtm_fid`| 文字列| フォームID。|
| `integration_type`| 真偽値| 統合タイプ。|
| `spa_support`| 真偽値| SPAサポート。|

### 標準

|変数| 型 | 説明|
|---| ---|---|
| `dtm_promo_id`| 文字列| プロモーションID。|
|`dtmc_tcf_string`| 文字列| GDPR同意文字列。|
|`dtm_email_hash`| 文字列| メールアドレスのハッシュ。|
| `dtm_user_id`| 文字列| ユーザーID。|
| `custom.myvar`| 文字列| カスタム。|
| `dtm_cookie_id` | 文字列 | Cookie IDをクエリパラメーターとして送信します。|

### ページ訪問

|変数| 型 | 説明|
|---| ---|---|
| `dtmc_department`| 文字列| 部門。|
| `dtmc_category`| 文字列| カテゴリー。|
| `dtmc_sub_category`| 文字列| サブカテゴリー。|
| `dtmc_product_id`| 文字列| 製品ID。|
| `dtmc_brand`| 文字列| メーカーのブランド。|
| `dtmc_upc`| 文字列| メーカーのUPC。|
| `dtmc_mpn`| 文字列| メーカーのモデル部品番号。|

### コンバージョン

|変数| 型 | 説明|
|---| ---|---|
| `dtmc_conv_type`| 文字列| コンバージョンタイプ。|
| `dtmc_conv_store_location`| 文字列| 店舗所在地。|
| `dtmc_transaction_id`（`_corder`を上書き| 文字列| 注文ID。|
| `dtm_conv_val`（`_csubtotal`を上書き| 文字列| 注文小計。|
| `dtm_conv_curr`（`_ccurrency`を上書き| 文字列| 注文通貨。|
| `product_id`（`_cprod`を上書き| 配列| 製品ID。|
| `product_quantity`（`_cquan`を上書き| 配列| 製品数量。|
| `product_unit_price`（`_cprice`を上書き| 配列| 製品価格。|
| `product_discount`（`_cpdisc`を上書き| 配列| 製品の割引額。|
|`dtm_items.myvar`| 配列| カスタムアイテム属性。|