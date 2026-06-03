---
title: Connexityピクセル構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでConnexityピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/connexity-pixel/
---
Connexityは、パフォーマンスマーケティング技術会社であり、その主な目的はオンライン小売業者が新しい顧客を見つけ、ROAS目標を満たすコストで販売を促進することです。

## タグのヒント

* マッピングを使用して：
  * 構成データを動的に上書きする
  * E-Commerce拡張値を動的に上書きする
  * 追加のデータ値を送信する
  * イベント固有のパラメータを提供する
  * イベントトリガーを指定する
* 以下のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 注文の小計
  * 商品の数量
  * 通貨

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Merchant ID**: Connexityから提供されたMerchant ID

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`mid`|Merchant ID|
|`page_type`|ページタイプ| 

### E-Commerce

|変数| タイプ | 説明|
|---|---|---|
|`order_id` | String |注文ID (`_corder`を上書き)|
|`order_value` | String | 注文価格 (`csubtotal`を上書き) |
|`order_currency` | String | 通貨 (`_ccurrency`を上書き)|
|`category_name` | String | カテゴリ名 (`ccat`を上書き)|
|`product_sku` | Array |商品SKU (`csku`を上書き)|
|`product_quantity` | Array | 商品の数量 (`_cquan`を上書き)|
|`cust type` | String |カスタムタイプ|
|`category_id`| String |カテゴリID|



### イベントトリガー

|変数| 説明|
|---| ---|
| `pageview`|ページビュー|
|`conversion`|コンバージョン| 
| `addtocart`|カートに追加|
| `Custom Event`|カスタムイベント|

### イベント固有のパラメータ

|変数| 説明|
|---| ---|
|Page View| ページビュー|
|Add to Cart| カートに追加|
|Conversion| コンバージョン|
|Custom Event| カスタムイベント|

