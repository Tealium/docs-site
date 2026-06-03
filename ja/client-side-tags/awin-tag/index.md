---
title: Awinタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAwinタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/awin-tag/
---
## タグのヒント

* タグとコネクターを使用したハイブリッド構成をお勧めします。この構成により、データの耐久性が最大化され、サーバーサイドのシグナルとのイベントマッチングが改善され、リアルタイムのクライアントサイドシグナルを保持しながらデータフローの連続性が維持されます。詳細については、[Awin Conversions Connector]()を参照してください。
* マッピングを使用して：
  * 標準の構成値を上書きします。
  * E-Commerce拡張の値を上書きします。
  * カスタムパラメータを渡します。
  * イベントトリガーを構成します。
* 次のE-Commerce拡張の値をサポートします：
  * 注文ID。
  * 注文合計。
  * 注文小計。
  * 注文送料。
  * 注文税金。
  * 注文通貨。
  * 製品IDのリスト。
  * カテゴリのリスト。
  * 数量のリスト。
  * 価格のリスト。
* 注文IDの値が構成されている場合、注文が記録されます。
* コミッショングループのデフォルト値は`DEFAULT`です。

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスして、Awinタグを追加します。詳細については、[タグの管理]()を参照してください。

タグを追加した後、次の構成を構成します：

* **広告主ID**：Awinから提供される広告主ID。
* **製品レベルデータを追加**：データペイロードに製品レベルのデータを追加します。
* **テストする**：このオプションを選択してタグをテストします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数 | タイプ | 説明 |
|:-------------|:---------|:---------|
| `advertiser_id`    | 文字列  | 広告主ID。          |
| `add_products`     | ブール値 | 製品レベルのデータを追加。 |
| `channel`          | 文字列  | チャネル。                |
| `commission_group` | 文字列  | コミッショングループ        |
| `is_test`          | ブール値 | テスト中。                |
| `custom`           | 配列   | カスタム値の配列。    |
| `custom.#`         | 文字列  | 最大255個のカスタムパラメータをマッピングできます。各パラメータは`custom.#`という命名規則に従います。ここで`#`は`11`から`255`の数字です。例：`custom.1`, `custom.2`など。       |

#### E-Commerce

| 変数 | タイプ | 説明 |
|:-------------|:---------|:---------|
| `order_id` (Overrides `_corder`)          | 文字列 | 注文ID。 |
| `order_subtotal` (Overrides `_csubtotal`) | 数値 | 小計/合計金額。 |
| `order_currency` (Overrides `_ccurrency`) | 文字列 | 通貨。 |
| `order_coupon_code` (Overrides `_cpromo`) | 文字列 | プロモコード。  |
| `product_id` (Overrides `_cprod`)         | 配列  | 製品IDのリスト。 |
| `product_name` (Overrides `_cprodname`)   | 配列  | 名称のリスト。    |
| `product_sku` (Overrides `_csku`)         | 配列  | SKUのリスト。 |
| `product_category` (Overrides `_ccat`)    | 配列  | カテゴリのリスト。 |
| `product_quantity` (Overrides `_cquan`)   | 配列  | 数量のリスト。 |
| `product_unit_price` (Overrides `_cprice`)| 配列  | 価格のリスト。  |
| `product_commission`                      | 配列  | コミッショングループのリスト。 |

#### イベントトリガー

| 変数   | タイプ | 説明  |
|:-----------|:-------------|:-------------|
| `conversion` | 文字列 | コンバージョン。 |

### ベンダー文書

* [Awin: なぜハイブリッドトラッキングがあなたのアフィリエイトプログラムに不可欠なのか](https://advertiser-success.awin.com/s/article/Why-hybrid-tracking-is-essential-for-your-affiliate-programme-here-s-what-you-need-to-know)
* [Awin: 広告主マスタータグ](https://developer.awin.com/docs/advertiser-mastertag)