---
title: Logicadタグ構成ガイド
description: この記事では、タグ管理アカウントでLogicadタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/logicad-tag/
---
Logicadでは、独自のアルゴリズムを使用してオーディエンスデータを高速かつ安定的に処理する大規模な配信ログおよびシステムインフラストラクチャにより、広告を効率的に配信できます。

## タグに関するヒント

* 動的クリエイティブリターゲティングタグタイプでは、商品グループIDと広告主商品IDのマッピングが必要です。
* 動的クリエイティブコンバージョンタグタイプでは、商品グループIDのマッピングが必要です。
* 次のEコマース拡張パラメータをサポートしています。
    * 注文ID（`_corder`）
    * 小計（`_csubtotal`）
    * 商品IDのリスト（`_cprod`）
    * 数量のリスト（`_cquan`）
    * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **広告主ID**：So-net Media Networkから提供された広告主ID。
* **タグタイプ**：ビジネスユースケースに適したタグのタイプを選択します。
* **フィールド区切り文字**：商品フィールド情報間の区切り文字。レコード区切り文字と同じ文字は使用できません。
* **レコード区切り文字**：商品レコード情報間の区切り文字。フィールド区切り文字と同じ文字は使用できません。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|---|---|
| `advertiser_id` | 広告主ID |
| `type` | タグタイプ |
| `field_delim` | 商品フィールドの区切り文字 |
| `record_delim` | 商品レコードの区切り文字 |
| `product_group_id` | 商品グループID |
| `advertiser_product_id` | 広告主商品ID |
| `retargeting_param` | リターゲティングパラメータ |
| `log_param1` | ログパラメータ1 |
| `log_param2` | ログパラメータ2 |
| `log_param3` | ログパラメータ3 |
| `log_param4` | ログパラメータ4 |
| `log_param5` | ログパラメータ5 |
| `log_param6` | ログパラメータ6 |
| `log_param7` | ログパラメータ7 |
| `log_param8` | ログパラメータ8 |
| `log_param9` | ログパラメータ9 |
| `log_param10` | ログパラメータ10 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文ID（`_corder`を上書き） |
| `order_subtotal` | 合計価格／小計（`_csubtotal`を上書き） |
| `order_quantity` | 合計数量（product_quantityの合計を上書き） |
|`product_id`  商品IDのリスト（`_cprod`を上書き）  | 
| `product_quantity` | 数量のリスト（`_cquan`を上書き） | 
| `product_unit_price` | 価格のリスト（`_cprice`を上書き） |