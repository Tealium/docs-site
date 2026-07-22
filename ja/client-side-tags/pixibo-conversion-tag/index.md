---
title: Pixiboコンバージョンタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでpixibo.conversionタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pixibo-conversion-tag/
---## タグのヒント

* マッピングを使用して：
  * クライアントIDの標準構成値を動的に上書きします
  * 注文と製品詳細の値を動的に上書きします
* サポートされているE-Commerce拡張パラメータ：
  * 注文ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 通貨 (`_ccurrency`)
  * 顧客ID (`_ccusti` )
  * SKUのリスト (`_csku`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアントID**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`clientId`|  <ul><li>文字列</li><li>クライアントID</li></ul> |
|`size`|  <ul><li>配列</li><li>製品サイズのリスト</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>必須</li><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_currency`|  <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_sku`|  <ul><li>配列</li><li>SKUのリスト</li><li>`_csku`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |


