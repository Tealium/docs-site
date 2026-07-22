---
title: comScore Digital Analytixタグ構成ガイド
description: この記事では、comScore Digital Analytixタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/comscore-digital-analytix-tag/
---
## タグのヒント

* comScoreは現在、GDPRに準拠しています。訪問の同意を示すには、`cs_ucfr`パラメータを0（同意なし）または1（同意）に構成します。デフォルトでは`cs_ucfrパラメータ`は0に構成されています。このパラメータはマッピングを通じて構成できます。この機能を利用するためには、このタグのテンプレートを更新する必要があるかもしれません。
* 追加の`c-parameters`を追加するためにマッピングを使用します。
* 注文IDがE-Commerce拡張機能を介して構成されると、注文追跡が自動的にトリガーされます。
* 次のE-Commerce拡張機能の値をサポートしています：
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

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

以下の構成を行います：

* **クライアントID**：あなたのcomScoreクライアントID（c2）
* **Stream Senseビデオトラッキング**： 
* **フォーム識別子**：フォームの測定を有効にするためにフォームIDまたは名前を入力します。すべてのフォームを測定するには*を入力します。隠しフォームフィールドの測定にはマッピングを使用します。フォームトラッキングを無効にするには、このフィールドを空白にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `c1`  | <ul><li>C1</li><li>文字列</li></ul> |
| `c2`  | <ul><li>クライアントID</li><li>文字列</li></ul> |
| `ns_type` | <ul><li>NSタイプ</li><li>文字列</li></ul> |
| `form` | <ul><li>フォーム識別子</li></ul> |
| `form_normal`  | <ul><li>通常のフォームフィールド</li><li>配列</li></ul> |
| `form_hidden`  | <ul><li>隠しフォームフィールド</li><li> 配列</li></ul> |
| `form_submit`  | <ul><li>送信イベントを報告</li><li> ブール値</li></ul> |
| `form_abandon`  | <ul><li>放棄イベントを報告</li><li>ブール値</li></ul> |
| `form_failure`  | <ul><li>失敗イベントを報告</li><li>ブール値</li></ul> |
| `cs_ucfr`  | <ul><li>同意状態</li><li>[0/1]</li></ul> |

### E-Commerce

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


