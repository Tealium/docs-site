---
title: Kameleoonタグ構成ガイド
description: この記事では、Kameleoonタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kameleoon-tag/
---
## タグのヒント

* 「商品表示を追跡」や「カートに追加を追跡」など、単一の商品情報を使用するイベントは、マッピングが存在しない場合、eコマース配列で最初に利用可能なデータポイントを引き出します。
* マッピングを使用して以下を行います：
  * 標準の構成値を上書きし、パラメータを構成します。
  * イベントをトリガーします。
  * イベント固有のパラメータを構成します。
* 次のEコマース拡張値をサポートします：
  * 注文合計
  * SKUリスト
  * 製品IDリスト
  * 名前リスト
  * ブランドリスト
  * カテゴリリスト
  * 数量リスト
  * 価格リスト

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際、以下の構成を行います：

* **サイトコード**：Kameleoonから提供されるユニークなサイトコード。
* **Iframe URL**：自己ホスト型IframeのURL。
* **クロスドメイントラッキングIframeを使用**：クロスドメイントラッキングIframeを使用します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数                        | 説明                                   |
|:----------------------------|:--------------------------------------|
| `site_code`                 | サイトコード。                         |
| `use_iframe`                | クロスドメイントラッキングIframeを使用。 |
| `iframe_url`                | Iframe URL。                          |
| `eventName`                 | カスタムイベント名。                   |
| `redirectionURL`            | リダイレクションURL。                 |
| `goalNameOrID`              | 目標名またはID。                       |
| `revenue`                   | 目標収益。                             |
| `name`                      | 名前。                                 |
| `value`                     | カスタムデータ値。                     |
| `overwriteIfCollection`     | コレクションの場合、カスタムデータを上書き。 |
| `experimentID`              | 実験ID。                               |
| `variationID`               | 変異ID。                               |
| `override`                  | 割り当てられた変異を上書き。           |
| `productId`                 | 製品ID。                               |
| `productName`               | 製品名。                               |
| `categoryId`                | 製品カテゴリID。                       |
| `category`                  | 製品カテゴリ名。                       |
| `mainImageURL`              | 製品のメイン画像URL。                  |
| `unitPrice`                 | 製品の単価。                           |
| `quantity`                  | 製品の数量。                           |
| `available`                 | 製品の利用可能性。                     |
| `brand`                     | 製品ブランド。                         |
| `child`                     | 子供用製品。                           |
| `gender`                    | 製品の性別。                           |
| `type`                      | 製品タイプ。                           |
| `feature`                   | 製品特徴。                             |
| `sku`                       | 製品SKU。                              |

### Eコマース

| 変数                        | タイプ   | 説明                                             |
|:----------------------------|:---------|:------------------------------------------------|
| `order_total`               | 数値     | 注文合計（`_ctotal`を上書き）。                  |
| `product_id`                | 配列     | 製品IDリスト（`_cprod`を上書き）。               |
| `product_name`              | 配列     | 製品名リスト（`_cprodname`を上書き）。           |
| `product_sku`               | 配列     | SKUリスト（`_csku`を上書き）。                   |
| `product_brand`             | 配列     | ブランドリスト（`_cbrand`を上書き）。             |
| `product_category`          | 配列     | カテゴリリスト（`_ccat`を上書き）。               |
| `product_quantity`          | 配列     | 数量リスト（`_cquan`を上書き）。                  |
| `product_unit_price`        | 配列     | 価格リスト（`_cprice`を上書き）。                 |

### イベントパラメータ

| 変数                            | 説明                       |
|:--------------------------------|:--------------------------|
| `enable_legal_consent`          | 法的同意を有効にする。     |
| `disable_legal_consent`         | 法的同意を無効にする。     |
| `enable_single_page_support`    | シングルページサポートを有効にする。 |
| `load`                          | ロード。                   |
| `process_redirect`              | リダイレクトを処理する。   |
| `cancel_conversion`             | コンバージョンをキャンセルする。 |
| `process_conversion`            | コンバージョンを処理する。 |
| `reset_custom_data`             | カスタムデータをリセットする。 |
| `set_custom_data`               | カスタムデータを構成する。 |
| `trigger`                       | トリガー。                 |
| `track_add_to_cart`             | カートに追加を追跡する。   |
| `track_category_view`           | カテゴリ表示を追跡する。   |
| `track_product_view`            | 商品表示を追跡する。       |
| `track_transaction`             | トランザクションを追跡する。 |
| `assign_variation`              | 変異を割り当てる。         |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント                        | 説明                                   |
|:--------------------------------|:--------------------------------------|
| `eventName`                     | カスタムイベント名。                   |
| `redirectionURL`                | リダイレクションURL。                 |
| `goalNameOrID`                  | 目標名またはID。                       |
| `revenue`                       | 目標収益。                             |
| `value`                         | カスタムデータ値。                     |
| `overwriteIfCollection`         | コレクションの場合、カスタムデータを上書き。 |
| `experimentID`                  | 実験ID。                               |
| `variationID`                   | 変異ID。                               |
| `override`                      | 割り当てられた変異を上書き。           |
| `productId`                     | 製品ID。                               |
| `productName`                   | 製品名。                               |
| `categoryId`                    | 製品カテゴリID。                       |
| `category`                      | 製品カテゴリ名。                       |
| `mainImageURL`                  | 製品のメイン画像URL。                  |
| `unitPrice`                     | 製品の単価。                           |
| `quantity`                      | 製品の数量。                           |
| `available`                     | 製品の利用可能性。                     |
| `brand`                         | 製品ブランド。                         |
| `child`                         | 子供用製品。                           |
| `gender`                        | 製品の性別。                           |
| `type`                          | 製品タイプ。                           |
| `feature`                       | 製品特徴。                             |
| `sku`                           | 製品SKU。                              |
