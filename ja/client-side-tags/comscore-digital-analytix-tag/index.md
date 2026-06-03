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

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

以下の構成を行います：

* **クライアントID**：あなたのcomScoreクライアントID（c2）
* **Stream Senseビデオトラッキング**： 
* **フォーム識別子**：フォームの測定を有効にするためにフォームIDまたは名前を入力します。すべてのフォームを測定するには*を入力します。隠しフォームフィールドの測定にはマッピングを使用します。フォームトラッキングを無効にするには、このフィールドを空白にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `c1`  | &lt;ul&gt;&lt;li&gt;C1&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
| `c2`  | &lt;ul&gt;&lt;li&gt;クライアントID&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
| `ns_type` | &lt;ul&gt;&lt;li&gt;NSタイプ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
| `form` | &lt;ul&gt;&lt;li&gt;フォーム識別子&lt;/li&gt;&lt;/ul&gt; |
| `form_normal`  | &lt;ul&gt;&lt;li&gt;通常のフォームフィールド&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;/ul&gt; |
| `form_hidden`  | &lt;ul&gt;&lt;li&gt;隠しフォームフィールド&lt;/li&gt;&lt;li&gt; 配列&lt;/li&gt;&lt;/ul&gt; |
| `form_submit`  | &lt;ul&gt;&lt;li&gt;送信イベントを報告&lt;/li&gt;&lt;li&gt; ブール値&lt;/li&gt;&lt;/ul&gt; |
| `form_abandon`  | &lt;ul&gt;&lt;li&gt;放棄イベントを報告&lt;/li&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
| `form_failure`  | &lt;ul&gt;&lt;li&gt;失敗イベントを報告&lt;/li&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
| `cs_ucfr`  | &lt;ul&gt;&lt;li&gt;同意状態&lt;/li&gt;&lt;li&gt;[0/1]&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `order_shipping` | &lt;ul&gt;&lt;li&gt;送料&lt;/li&gt;&lt;li&gt;`_cship`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `customer_id` | &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_id` | &lt;ul&gt;&lt;li&gt;製品IDのリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cprod`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_brand` | &lt;ul&gt;&lt;li&gt;ブランドのリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cbrand`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_category` | &lt;ul&gt;&lt;li&gt;カテゴリのリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_ccat`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_subcategory` | &lt;ul&gt;&lt;li&gt;サブカテゴリのリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_ccat`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity` | &lt;ul&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cquan`を上書き&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` | &lt;ul&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cprice`を上書き&lt;/li&gt;&lt;/ul&gt; |   


