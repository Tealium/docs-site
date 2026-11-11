---
title: Pepperjamタグ構成ガイド
description: この記事では、タグ管理アカウントでPepperjamタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pepperjam-tag/
---## タグに関するヒント

* 次のEコマース拡張機能の値をサポートしています。
  * 注文ID
  * 小計
  * プロモーションコード
  * 商品IDのリスト
  * 価格のリスト
  * 数量のリスト
  * カテゴリーのリスト
* 「標準統合タイプ」の値は、タグの統合値が「標準」の場合にのみ適用されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **プログラムID**  
Pepperjamから提供されたID。
* **統合**
* **標準統合タイプ**  
この選択は、このタグの標準統合にのみ影響します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`base_url`|  <ul><li>ベースURL</li></ul> |
|`pid`|  <ul><li>プログラムID</li></ul> |
|`integration`|  <ul><li>統合</li><li>値は次のとおりです。<ul><li>STANDARD</li><li>DYNAMIC</li><li>ITEMIZED</li></ul> </li></ul> |
|`type`|  <ul><li>標準統合タイプ</li><li>値は**1**または**2**です。</li></ul> |
|`new_to_file`|  <ul><li>新規顧客</li><li>値は、または**1**です。</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード</li><li>`_cpromo`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリーのリスト</li><li>`_ccat`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |