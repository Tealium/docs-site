---
title: Movable Ink Da Vinci Signalタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMovable Ink Da Vinci Signalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/movable-ink-da-vinci-signal-tag/
---
## タグのヒント

* マッピングを使用して:   
  * 構成データを動的に上書き   
  * E-Commerce拡張の値を動的に上書き   
  * 追加のデータ値を送信   
  * イベントトリガー
* 以下のE-Commerce拡張値をサポート:   
  * 顧客ID   
  * 注文ID   
  * 注文の小計   
  * 商品割引のリスト   
  * 商品IDのリスト   
  * 商品名のリスト   
  * 商品数量のリスト   
  * 商品価格のリスト

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います:

* **アクセストークン**: Da Vinci Signal APIのアクセストークン。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

イベントと予想されるイベント詳細についての詳細は、[Da Vinci Javascript SDKドキュメンテーション](https://help.coherentpath.com/guides/technical/javascript-sdk)を参照してください。ドキュメンテーションにアクセスするにはDa Vinciヘルプセンターにログインする必要があります。アクセスに問題がある場合は、Da Vinciアカウントチームに連絡してください。

利用可能なカテゴリは以下の通りです:

### タグ構成

|変数| タイプ | 説明|
|---| ---|---|
| `config_access_token`| 文字列| アクセストークン。 | 
| `config_base_url` | 文字列 | ベースURL (デフォルト値は `https://track.coherentpath.com`。) |
| `config_currency_code` | 文字列 | 通貨コード (デフォルト値は `USD`。)|
| `config_debug` | ブール値 | デバッグフラグ (デフォルト値は `false`。)|

### イベントパラメータ

|変数| タイプ | 説明|
|---| ---| ---|
| `contact_id`| 文字列 | コンタクトID。  |
| `customer_email`| 文字列| 顧客のメール。 |
| `order_discount`| 文字列| 注文割引。 |
| `order_processed_at` | 文字列| 注文処理日。 (デフォルト値は現在の時間。) |
| `page_referrer` | 文字列| ページリファラー。 (デフォルト値は現在のページリファラー。)|
| `page_title` | 文字列| ページタイトル。 (デフォルト値は現在のページタイトル。) |
| `page_url` | 文字列| ページURL。 (デフォルト値は現在のページURL。) |
| `product_variant_id`| 配列| 商品バリアントIDのリスト。 |
| `product_variant_name`| 配列| 商品バリアント名のリスト。 |
| `product_variant_price`| 配列| 商品バリアント価格のリスト。|
| `product_variant_product_id` | 配列| 商品バリアントの商品IDのリスト。 (商品バリアントと商品をリンク。) |
| `search_term`| 文字列| 検索語。|
| `source`| 文字列| ユーザーがページに到達した方法。 |
| `metadata_tags`| 配列| メタデータタグのリスト。 |
| `metadata_attributes`| オブジェクト| メタデータ属性。 |

### E-Commerce

|変数| タイプ | 説明|
|---| ---|---|
| `customer_id` ( `_ccustid`を上書き)| 文字列| 顧客ID。 |
| `order_id` ( `_corder`を上書き)| 文字列| 注文ID。 |
| `order_subtotal` ( `_csubtotal`を上書き)| 文字列| 注文の小計。 |
| `product_discount` ( `_cpdisc`を上書き)| 配列| 商品割引のリスト。 |
| `product_id` ( `_cprod`を上書き)| 配列| 商品IDのリスト。 |
| `product_name` ( `_cprodname`を上書き)| 配列| 商品名のリスト。 |
| `product_quantity` ( `_cquan`を上書き)| 配列| 商品数量のリスト。 | 
| `product_unit_price` ( `_cprice`を上書き)| 配列| 商品価格のリスト。 |

### イベント

|変数| 説明|
|---| ---|
|`Forget`| 忘れる|
|`Identity`| 身元|
|`OrderCancelation`| 注文キャンセル|
|`OrderCompletion`| 注文完了|
|`OrderRefund`| 注文返金|
|`PageView`| ページビュー|
|`ProductPageView`| 商品ページビュー|
|`ProductSearch`| 商品検索|

