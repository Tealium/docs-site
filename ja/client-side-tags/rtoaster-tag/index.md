---
title: RToasterタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでRToasterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rtoaster-tag/
---
## タグのヒント

* カンマで区切ったリストとしてIDを入力することで、複数の要素IDを構成できます。
* マッピングを使用して、標準の構成値を上書きします。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Rtoasterタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **アカウントID**
  * あなたのRtoasterアカウントID。

* **推奨要素ID**
  * Rtoasterの推奨対象となる要素のID。
  * カンマで区切ったリストとして複数のIDを入力できます。

* **ポップアップ要素ID**
  * Rtoasterのポップアップ推奨対象となる要素のID。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`account_id`|  <ul><li>文字列</li><li>アカウントID</li></ul> |
|`element_id`|  <ul><li>文字列、配列</li><li>要素ID</li></ul> |
|`popup_element_id`|  <ul><li>文字列</li><li>ポップアップ要素ID</li></ul> |
|`category`|  <ul><li>文字列、配列</li><li>カテゴリ</li></ul> |
|`price_min`|  <ul><li>文字列、数値</li><li>最低価格</li></ul> |
|`price_max`|  <ul><li>文字列、数値</li><li>最高価格</li></ul> |

### E-コマース

|変数| 説明|
|---| ---|
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_shipping`|  <ul><li>送料。</li><li>`_cship`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |
