---
title: AcuityAds Universal Pixel セットアップガイド
description: この記事では、タグ管理アカウントで AcuityAds Universal Pixel タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/acuityads-universal-pixel-tag/
---
Acuity タグを使用すると、メディア購入プロセスに伴うリスク、不確実性、無駄を体系的かつ数学的に排除し、広告費を常に賢く効果的に使用できるようにするとともに、その効果を実証することもできます。

## タグに関するヒント

* マッピングを使用して、Pixel Key または E-commerce 変数の値を上書きし、**ページグループ番号**を構成します。

* 次の E-Commerce 拡張パラメータをサポートしています。
  * 注文 ID（`_corder`）
  * 注文合計（`_ctotal`）、商品 ID（`_cprod`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Pixel Key**：ピクセル固有のキー値。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| Pixel Key `pixel_key` | 文字列 |
| ページグループ番号 `page_group_number` | 数値 |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| 注文 ID | `order_id`（`_corder`を上書き）数値 |
| 注文合計／カート収益 | `order_total`（`_ctotal`を上書き）数値 |
| 商品 ID のリスト `product_id`（`_cprod`を上書き） | 配列 |