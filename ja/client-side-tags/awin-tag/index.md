---
title: Awinタグ構成ガイド
description: この記事では、タグ管理アカウントでAwinタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/awin-tag/
---
## タグに関するヒント

* タグとコネクターの両方を使用するハイブリッド構成を推奨します。この構成により、データの耐障害性を最大限に高め、サーバー側のシグナルとのイベント照合を改善し、リアルタイムのクライアント側シグナルを維持しながらデータフローの継続性を確保できます。詳細については、[Awinコンバージョンコネクター](https://docs.tealium.com/awin-conversions-connector/)を参照してください。
* マッピングを使用すると、以下を実行できます。  
  * 標準構成値を上書きする。
  * Eコマース拡張機能の値を上書きする。
  * カスタムパラメータを渡す。
  * イベントトリガーを構成する。
* 以下のEコマース拡張機能の値をサポートしています。  
  * 注文ID。
  * 注文合計。
  * 注文小計。
  * 注文の送料。
  * 注文の税額。
  * 注文通貨。
  * 商品IDのリスト。
  * カテゴリーのリスト。
  * 数量のリスト。
  * 価格のリスト。
* 注文IDの値が構成されている場合、注文が記録されます。
* コミッショングループのデフォルト値は`DEFAULT`です。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を構成します。

* **広告主ID**：Awinから提供された広告主ID。
* **商品レベルデータを追加**：商品レベルのデータをデータペイロードに追加します。
* **テスト**：タグをテストするには、このオプションを選択します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:-------------|:---------|:---------|
| `advertiser_id`    | 文字列  | 広告主ID。          |
| `add_products`     | ブール値 | 商品レベルのデータを追加します。 |
| `channel`          | 文字列  | チャネル。                |
| `commission_group` | 文字列  | コミッショングループ。        |
| `is_test`          | ブール値 | テストかどうか。                |
| `custom`           | 配列   | カスタム値の配列。    |
| `custom.#`         | 文字列  | 最大255個のカスタムパラメータをマッピングできます。各パラメータは`custom.#`という命名規則に従います。ここで、`#`は`11`から`255`までの数値です。例：`custom.1`、`custom.2`など。       |

#### Eコマース

| 変数 | 型 | 説明 |
|:-------------|:---------|:---------|
| `order_id`（`_corder`を上書き）          | 文字列 | 注文ID。 |
| `order_subtotal`（`_csubtotal`を上書き） | 数値 | 小計／合計金額。 |
| `order_currency`（`_ccurrency`を上書き） | 文字列 | 通貨。 |
| `order_coupon_code`（`_cpromo`を上書き） | 文字列 | プロモーションコード。  |
| `product_id`（`_cprod`を上書き）         | 配列  | 商品IDのリスト。 |
| `product_name`（`_cprodname`を上書き）   | 配列  | 商品名のリスト。    |
| `product_sku`（`_csku`を上書き）         | 配列  | SKUのリスト。 |
| `product_category`（`_ccat`を上書き）    | 配列  | カテゴリーのリスト。 |
| `product_quantity`（`_cquan`を上書き）   | 配列  | 数量のリスト。 |
| `product_unit_price`（`_cprice`を上書き）| 配列  | 価格のリスト。  |
| `product_commission`                      | 配列  | コミッショングループのリスト。 |

#### イベントトリガー

| 変数   | 型 | 説明  |
|:-----------|:-------------|:-------------|
| `conversion` | 文字列 | コンバージョン。 |

### ベンダーのドキュメント

* [Awin：アフィリエイトプログラムにハイブリッドトラッキングが不可欠な理由](https://advertiser-success.awin.com/s/article/Why-hybrid-tracking-is-essential-for-your-affiliate-programme-here-s-what-you-need-to-know)
* [Awin：広告主向けMastertag](https://developer.awin.com/docs/advertiser-mastertag)