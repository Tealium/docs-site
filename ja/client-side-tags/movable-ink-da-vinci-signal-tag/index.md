---
title: Movable Ink Da Vinci Signalタグ構成ガイド
description: この記事では、タグ管理アカウントでMovable Ink Da Vinci Signalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/movable-ink-da-vinci-signal-tag/
---
## タグに関するヒント

* マッピングを使用すると、以下のことができます。   
  * 構成データを動的に上書きする   
  * Eコマース拡張機能の値を動的に上書きする   
  * 追加のデータ値を送信する   
  * イベントをトリガーする
* 以下のEコマース拡張機能の値をサポートしています。   
  * 顧客ID   
  * 注文ID   
  * 注文小計   
  * 商品割引のリスト   
  * 商品IDのリスト   
  * 商品名のリスト   
  * 商品数量のリスト   
  * 商品価格のリスト

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **アクセストークン**：Da Vinci Signal APIのアクセストークン。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

イベントと想定されるイベントの詳細については、[Da Vinci JavaScript SDKドキュメント](https://help.coherentpath.com/guides/technical/javascript-sdk)を参照してください。このドキュメントにアクセスするには、Da Vinciヘルプセンターにログインする必要があります。アクセスに問題がある場合は、Da Vinciのアカウント担当チームにお問い合わせください。

利用可能なカテゴリーは以下のとおりです。

### タグの構成

|変数| 型 | 説明|
|---| ---|---|
| `config_access_token`| 文字列| アクセストークン。 | 
| `config_base_url` | 文字列 | ベースURL（デフォルト値は`https://track.coherentpath.com`です。） |
| `config_currency_code` | 文字列 | 通貨コード（デフォルト値は`USD`です。）|
| `config_debug` | ブール値 | デバッグフラグ（デフォルト値は`false`です。）|

### イベントパラメーター

|変数| 型 | 説明|
|---| ---| ---|
| `contact_id`| 文字列 | 連絡先ID。  |
| `customer_email`| 文字列| 顧客のメールアドレス。 |
| `order_discount`| 文字列| 注文の割引。 |
| `order_processed_at` | 文字列| 注文の処理日時。（デフォルト値は現在時刻です。） |
| `page_referrer` | 文字列| ページのリファラー。（デフォルト値は現在のページのリファラーです。）|
| `page_title` | 文字列| ページタイトル。（デフォルト値は現在のページタイトルです。） |
| `page_url` | 文字列| ページURL。（デフォルト値は現在のページURLです。） |
| `product_variant_id`| 配列| 商品バリエーションIDのリスト。 |
| `product_variant_name`| 配列| 商品バリエーション名のリスト。 |
| `product_variant_price`| 配列| 商品バリエーション価格のリスト。|
| `product_variant_product_id` | 配列| 商品バリエーションの商品IDのリスト。（商品バリエーションを商品に関連付けます。） |
| `search_term`| 文字列| 検索語句。|
| `source`| 文字列| ユーザーがページに到達した経路。 |
| `metadata_tags`| 配列| メタデータタグのリスト。 |
| `metadata_attributes`| オブジェクト| メタデータ属性。 |

### Eコマース

|変数| 型 | 説明|
|---| ---|---|
| `customer_id`（`_ccustid`を上書き）| 文字列| 顧客ID。 |
| `order_id`（`_corder`を上書き）| 文字列| 注文ID。 |
| `order_subtotal`（`_csubtotal`を上書き）| 文字列| 注文小計。 |
| `product_discount`（`_cpdisc`を上書き）| 配列| 商品割引のリスト。 |
| `product_id`（`_cprod`を上書き）| 配列| 商品IDのリスト。 |
| `product_name`（`_cprodname`を上書き）| 配列| 商品名のリスト。 |
| `product_quantity`（`_cquan`を上書き）| 配列| 商品数量のリスト。 | 
| `product_unit_price`（`_cprice`を上書き）| 配列| 商品価格のリスト。 |

### イベント

|変数| 説明|
|---| ---|
|`Forget`| 忘却|
|`Identity`| ID特定|
|`OrderCancelation`| 注文キャンセル|
|`OrderCompletion`| 注文完了|
|`OrderRefund`| 注文返金|
|`PageView`| ページ表示|
|`ProductPageView`| 商品ページ表示|
|`ProductSearch`| 商品検索|