---
title: Salesforce Marketing Cloud（ExactTarget）タグ構成ガイド
description: この記事では、タグ管理アカウントで Salesforce Marketing Cloud（ExactTarget）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salesforce-marketing-cloud-exacttarget/
---
Salesforce Marketing Cloud（旧称 ExactTarget）は、企業と顧客をまったく新しい方法で結び付け、1 対 1 のカスタマージャーニーを実現するプラットフォームです。

## タグに関するヒント

* 次の E-Commerce 拡張パラメータをサポートします。
    * 注文 ID
    * 商品 ID のリスト
    * 価格のリスト
* このタグをランディングページとコンバージョンページに追加します。
* 訪問情報を Cookie に自動的に保存し、確認ページで送信します。
* マッピングを使用すると、標準構成値または E-Commerce 拡張機能の値を動的に上書きできます。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **アカウント**：ExactTarget のメンバー ID。ランディングページのクエリ文字列にある `mid = param` と一致する必要があります。
* **コンバージョンページ ID**：複数のコンバージョンページを区別するために使用する一意の番号です。
* **コンバージョンページのエイリアス**：このコンバージョンページについて ExactTarget に表示する名前です。
* **コンバージョンページの表示順序**：ExactTarget でコンバージョンページを表示する順序を表す番号です。
* **S4 を使用**：デフォルトは **いいえ** です。`click.exacttarget.com` の代わりにピクセルの送信先として `click.s4.exacttarget.com` を使用するには、**はい** に構成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `account` | アカウント ID |
| `convid` | コンバージョンリンク ID |
| `alias` | リンクのエイリアス |
| `displayorder` | 表示順序 |
| `s4` | S4 を使用 |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| `order_id`（`_corder` を上書き） | 注文 ID |
| `product_id`（`_cprod` を上書き） | 商品 ID のリスト |
| `product_unit_price`（`_cprice` を上書き） | 価格のリスト |