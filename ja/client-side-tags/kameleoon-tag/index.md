---
title: Kameleoonタグ構成ガイド
description: この記事では、Kameleoonタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kameleoon-tag/
---
## タグ構成のヒント

* 商品表示のトラッキングやカート追加のトラッキングなど、単一商品の情報を使用するイベントでは、マッピングが構成されていない場合、Eコマース配列内で最初に使用可能なデータポイントが取得されます。
* マッピングは次の目的で使用します。
  * 標準の構成値を上書きし、パラメータを構成する。
  * イベントをトリガーする。
  * イベント固有のパラメータを構成する。
* 次のEコマース拡張機能の値をサポートしています。
  * 注文合計
  * SKUのリスト
  * 商品IDのリスト
  * 商品名のリスト
  * ブランドのリスト
  * カテゴリーのリスト
  * 数量のリスト
  * 価格のリスト

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **サイトコード**：Kameleoonから提供される一意のサイトコード。
* **Iframe URL**：セルフホストしているIframeのURL。
* **クロスドメイントラッキングIframeを使用**：クロスドメイントラッキングIframeを使用します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数                    | 説明                                       |
|:------------------------|:-------------------------------------------|
| `site_code`             | サイトコード。                             |
| `use_iframe`            | クロスドメイントラッキングIframeを使用。   |
| `iframe_url`            | Iframe URL。                               |
| `eventName`             | カスタムイベント名。                       |
| `redirectionURL`        | リダイレクトURL。                          |
| `goalNameOrID`          | ゴール名またはID。                         |
| `revenue`               | ゴール収益。                               |
| `name`                  | 名前。                                     |
| `value`                 | カスタムデータ値。                         |
| `overwriteIfCollection` | コレクションの場合にカスタムデータを上書き。 |
| `experimentID`          | 実験ID。                                   |
| `variationID`           | バリエーションID。                         |
| `override`              | 割り当てられたバリエーションを上書き。     |
| `productId`             | 商品ID。                                   |
| `productName`           | 商品名。                                   |
| `categoryId`            | 商品カテゴリーID。                         |
| `category`              | 商品カテゴリー名。                         |
| `mainImageURL`          | 商品のメイン画像URL。                      |
| `unitPrice`             | 商品の単価。                               |
| `quantity`              | 商品の数量。                               |
| `available`             | 商品の在庫状況。                           |
| `brand`                 | 商品のブランド。                           |
| `child`                 | 子供向け商品。                             |
| `gender`                | 商品の対象性別。                           |
| `type`                  | 商品タイプ。                               |
| `feature`               | 商品の特徴。                               |
| `sku`                   | 商品SKU。                                  |

### Eコマース

| 変数                 | 型     | 説明                                           |
|:---------------------|:-------|:-----------------------------------------------|
| `order_total`        | 数値   | 注文合計（`_ctotal`を上書き）。                |
| `product_id`         | 配列   | 商品IDのリスト（`_cprod`を上書き）。           |
| `product_name`       | 配列   | 商品名のリスト（`_cprodname`を上書き）。       |
| `product_sku`        | 配列   | SKUのリスト（`_csku`を上書き）。               |
| `product_brand`      | 配列   | ブランドのリスト（`_cbrand`を上書き）。        |
| `product_category`   | 配列   | カテゴリーのリスト（`_ccat`を上書き）。        |
| `product_quantity`   | 配列   | 数量のリスト（`_cquan`を上書き）。             |
| `product_unit_price` | 配列   | 価格のリスト（`_cprice`を上書き）。            |

### イベントパラメータ

| 変数                          | 説明                             |
|:------------------------------|:---------------------------------|
| `enable_legal_consent`        | 法的同意を有効化。               |
| `disable_legal_consent`       | 法的同意を無効化。               |
| `enable_single_page_support`  | シングルページサポートを有効化。 |
| `load`                        | 読み込み。                       |
| `process_redirect`            | リダイレクトを処理。             |
| `cancel_conversion`           | コンバージョンをキャンセル。     |
| `process_conversion`          | コンバージョンを処理。           |
| `reset_custom_data`           | カスタムデータをリセット。       |
| `set_custom_data`             | カスタムデータを構成。           |
| `trigger`                     | トリガー。                       |
| `track_add_to_cart`           | カートへの追加をトラッキング。   |
| `track_category_view`         | カテゴリー表示をトラッキング。   |
| `track_product_view`          | 商品表示をトラッキング。         |
| `track_transaction`           | トランザクションをトラッキング。 |
| `assign_variation`            | バリエーションを割り当て。       |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント                     | 説明                                         |
|:-----------------------------|:---------------------------------------------|
| `eventName`                  | カスタムイベント名。                         |
| `redirectionURL`             | リダイレクトURL。                            |
| `goalNameOrID`               | ゴール名またはID。                           |
| `revenue`                    | ゴール収益。                                 |
| `value`                      | カスタムデータ値。                           |
| `overwriteIfCollection`      | コレクションの場合にカスタムデータを上書き。 |
| `experimentID`               | 実験ID。                                     |
| `variationID`                | バリエーションID。                           |
| `override`                   | 割り当てられたバリエーションを上書き。       |
| `productId`                  | 商品ID。                                     |
| `productName`                | 商品名。                                     |
| `categoryId`                 | 商品カテゴリーID。                           |
| `category`                   | 商品カテゴリー名。                           |
| `mainImageURL`               | 商品のメイン画像URL。                        |
| `unitPrice`                  | 商品の単価。                                 |
| `quantity`                   | 商品の数量。                                 |
| `available`                  | 商品の在庫状況。                             |
| `brand`                      | 商品のブランド。                             |
| `child`                      | 子供向け商品。                               |
| `gender`                     | 商品の対象性別。                             |
| `type`                       | 商品タイプ。                                 |
| `feature`                    | 商品の特徴。                                 |
| `sku`                        | 商品SKU。                                    |