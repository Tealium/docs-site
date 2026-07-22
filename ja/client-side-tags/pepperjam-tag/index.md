---
title: Pepperjamタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPepperjamタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pepperjam-tag/
---## タグのヒント

* 以下のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 小計
  * プロモーションコード
  * 商品IDのリスト
  * 価格のリスト
  * 数量のリスト
  * カテゴリのリスト
* "Standard Integration Type"の値は、タグの統合値が"Standard"の場合にのみ適用されます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Program ID**  
Pepperjamから提供されたID。
* **Integration**
* **Standard Integration Type**  
この選択は、このタグのStandard統合にのみ影響します。

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### Standard

|変数| 説明|
|---| ---|
|`base_url`|  <ul><li>ベースURL</li></ul> |
|`pid`|  <ul><li>プログラムID</li></ul> |
|`integration`|  <ul><li>統合</li><li>値は次の通りです：<ul><li>STANDARD</li><li>DYNAMIC</li><li>ITEMIZED</li></ul> </li></ul> |
|`type`|  <ul><li>Standard統合タイプ</li><li>値は**1**または**2**です。</li></ul> |
|`new_to_file`|  <ul><li>新規ファイル</li><li>値は**1**です。</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード</li><li>`_cpromo`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト</li><li>`_ccat`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |

