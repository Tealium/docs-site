---
title: Pixiboコンバージョンタグ構成ガイド
description: この記事では、タグ管理アカウントでpixibo.conversionタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pixibo-conversion-tag/
---## タグに関するヒント

* マッピングを使用して、次の操作を行います。
  * クライアントIDの標準構成値を動的に上書きする
  * 注文および商品の詳細の値を動的に上書きする
* サポートされているEコマース拡張パラメータ：
  * 注文ID（`_corder`）
  * 小計（`_csubtotal`）
  * 通貨（`_ccurrency`）
  * 顧客ID（`_ccusti`）
  * SKUのリスト（`_csku`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **クライアントID**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---| ---|
|`clientId`|  <ul><li>文字列</li><li>クライアントID</li></ul> |
|`size`|  <ul><li>配列</li><li>商品サイズのリスト</li></ul> |

### Eコマース

|変数|説明|
|---| ---|
|`order_id`|  <ul><li>（必須）注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_currency`|  <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_sku`|  <ul><li>配列</li><li>SKUのリスト</li><li>`_csku`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |