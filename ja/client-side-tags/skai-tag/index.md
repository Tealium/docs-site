---
title: Skai（旧 Kenshoo）タグ
description: この記事では、Skai（旧 Kenshoo）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/skai-tag/
---
## タグに関するヒント

* マッピングを使用して、タグの構成を動的に上書きまたは構成できます。
* コンバージョントラッキングを実行するには、`cid`、`conversion_code`、`conversionType` を構成する必要があります。`conversionType` パラメータは、構成されていない場合はデフォルトで「conv」になります。
* カスタムパラメータをトラッキングするには、カスタムの送信先にマッピングする必要があります。
* 以下の E コマース拡張パラメータをサポートしています。
    * 注文 ID（`_corder`）
    * 注文小計（`_csubtotal`）
    * 注文通貨（`_ccurrency`）
    * 注文クーポンコード（`_cpromo`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **顧客 ID**：Skai の顧客 ID。
* **コンバージョンコード**：Skai から提供されたコンバージョンコード。
* **コンバージョンタイプ**：コンバージョンのタイプ。構成されていない場合は、デフォルトで「conv」になります。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `cid` | 顧客 ID |
| `conversion_code` | コンバージョンコード |
| `conversionType` | コンバージョンタイプ |

### E コマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文 ID（`_corder` を上書き） |
| `order_subtotal` | 小計（`_csubtotal` を上書き） |
| `order_currency` | 通貨（`_ccurrency` を上書き） |
| `order_coupon_code` | プロモーションコード（`_cpromo` を上書き） |