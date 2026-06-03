---
title: Exactagタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでExactagタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/exactag-tag/
---
## タグのヒント

* E-Commerce拡張に対応しています:
  * 注文ID
  * 注文小計
  * 注文合計
  * 注文クーポンコード
  * 顧客ID
  * 商品ID
  * 商品名
  * 商品カテゴリ
  * 商品数量
  * 商品単価

* 注文IDが存在する場合、自動的にコンバージョンデータが追加されます。コンバージョンデータは、**Is Conversion Flag**を`true`に構成することで手動でトリガーできます
* **UI Add Custom Destination**オプションを通じて追加のデータポイントを追加できます

### タグ構成

まず、タグマーケットプレイスに移動し、Exactagタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います:

* **キャンペーンコード**  
ブランド固有のキャンペーンコード

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです:

### スタンダード

| 変数               | 説明             |
|:-------------------|:------------------|
| キャンペーンコード | (`campaign`)      |
| リファラーURL      | (`referrer`)      |
| ホストドメイン     | (`host`)          |
| サイトパス         | (`site`)          |
| 検索パラメータ     | (`search`)        |
| サイトグループ     | (`sitegroup`)     |
| クロスデバイスID   | (`crossid`)       |
| Subid              | (`subid`)         |
| コンバージョンフラグ | (`is_conversion`) |

### E-Commerce

| 変数                                                       | 説明                                      |
|:-----------------------------------------------------------|:-------------------------------------------|
| レベル値                                                   | (`level`)                                  |
| 顧客性別                                                   | (`customer_gender`)                         |
| 顧客タイプ                                                 | (`customer_type`)                           |
| 注文ID                                                     | (`order_id`) (Overrides `_corder`)           |
| 収益/注文合計                                              | (`order_total`) (Overrides `_ctotal`)        |
| 合計価格/小計                                              | (`order_subtotal`) (Overrides `_csubtotal`)  |
| プロモーションコード                                       | (`order_coupon_code`) (Overrides `_cpromo`) |
| カートまたは注文タイプ                                     | (`order_type`) (Overrides `_ctype`)          |
| 顧客ID                                                     | (`customer_id`) (Overrides `_ccustid`)       |
| 商品IDのリスト (`product_id`) (Overrides `_cprod`)           | [配列]                                      |
| 名前のリスト (`product_name`) (Overrides `_cprodname`)       | [配列]                                      |
| カテゴリのリスト (`product_category`) (Overrides `_ccat`)     | [配列]                                      |
| 数量のリスト (`product_quantity`) (Overrides `_cquan`)       | [配列]                                      |
| 価格のリスト (`product_unit_price`) (Overrides `_cprice`)   | [配列]                                      |
