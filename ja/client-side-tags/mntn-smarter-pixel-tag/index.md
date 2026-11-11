---
title: MNTN Smarter Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでMNTN（旧Steelhouse）Smarter Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mntn-smarter-pixel-tag/
---

## タグに関するヒント

* マッピングを使用すると、アカウントIDを動的に上書きしたり、`additional`パラメータにデータを渡したりできます。
* 注文IDが構成されると、コンバージョンタグが発火します。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 小計（`_csubtotal`）
  * 商品IDのリスト（`_cprod`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **アカウントID**
  * 例：`12345`

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`acct`| アカウントID|

### 追加変数

|変数| 説明|
|---| ---|
|`adv.track.myvar`| 追加のトラッキング変数 |
|`adv.conv.myvar`| アカウントコンバージョン変数 |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`| <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`| <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`product_id`| <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_quantity`| <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`| <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |