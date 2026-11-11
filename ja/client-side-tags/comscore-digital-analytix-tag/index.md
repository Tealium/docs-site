---
title: comScore Digital Analytixタグ構成ガイド
description: この記事では、comScore Digital Analytixタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/comscore-digital-analytix-tag/
---
## タグに関するヒント

* comScoreは現在、GDPRに準拠しています。`cs_ucfr`パラメータを0（同意なし）または1（同意あり）に構成することで、訪問の同意を示すことができます。デフォルトでは、`cs_ucfr parameter`は0に構成されています。このパラメータはマッピングを使用して構成できます。この機能を利用するには、このタグのテンプレートを更新する必要がある場合があります。
* マッピングを使用して、追加の`c-parameters`を指定します。
* Eコマース拡張機能によって注文IDが構成されると、注文トラッキングが自動的にトリガーされます。
* 以下のEコマース拡張機能の値をサポートしています。
    * 注文ID
    * 送料
    * 顧客ID
    * 製品IDのリスト
    * ブランドのリスト
    * カテゴリのリスト
    * カテゴリ2のリスト
    * 数量のリスト
    * 価格のリスト

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

以下の構成を行います。

* **クライアントID**：comScoreのクライアントID（c2）
* **Stream Sense動画トラッキング**：
* **フォーム識別子**：フォーム測定を有効にするには、フォームIDまたは名前を入力します。すべてのフォームを測定するには、*を入力します。非表示のフォームフィールドを測定するには、マッピングを使用します。フォームトラッキングを無効にするには、このフィールドを空白のままにします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `c1`  | <ul><li>C1</li><li>文字列</li></ul> |
| `c2`  | <ul><li>クライアントID</li><li>文字列</li></ul> |
| `ns_type` | <ul><li>NSタイプ</li><li>文字列</li></ul> |
| `form` | <ul><li>フォーム識別子</li></ul> |
| `form_normal`  | <ul><li>通常のフォームフィールド</li><li>配列</li></ul> |
| `form_hidden`  | <ul><li>非表示のフォームフィールド</li><li>配列</li></ul> |
| `form_submit`  | <ul><li>送信イベントをレポート</li><li>ブール値</li></ul> |
| `form_abandon`  | <ul><li>離脱イベントをレポート</li><li>ブール値</li></ul> |
| `form_failure`  | <ul><li>失敗イベントをレポート</li><li>ブール値</li></ul> |
| `cs_ucfr`  | <ul><li>同意状態</li><li>[0/1]</li></ul> |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | <ul><li>注文ID</li><li>`_corder`を上書き</li></ul> |
| `order_shipping` | <ul><li>送料</li><li>`_cship`を上書き</li></ul> |
| `customer_id` | <ul><li>顧客ID</li><li>`_ccustid`を上書き</li></ul> |
| `product_id` | <ul><li>製品IDのリスト</li><li>配列</li><li>`_cprod`を上書き</li></ul> |
| `product_brand` | <ul><li>ブランドのリスト</li><li>配列</li><li>`_cbrand`を上書き</li></ul> |
| `product_category` | <ul><li>カテゴリのリスト</li><li>配列</li><li>`_ccat`を上書き</li></ul> |
| `product_subcategory` | <ul><li>サブカテゴリのリスト</li><li>配列</li><li>`_ccat`を上書き</li></ul> |
| `product_quantity` | <ul><li>数量のリスト</li><li>配列</li><li>`_cquan`を上書き</li></ul> |
| `product_unit_price` | <ul><li>価格のリスト</li><li>配列</li><li>`_cprice`を上書き</li></ul> |