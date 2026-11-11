---
title: RToasterタグ構成ガイド
description: この記事では、タグ管理アカウントでRToasterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rtoaster-tag/
---
## タグ構成のヒント

* 複数の要素IDを構成するには、IDをカンマ区切りのリストとして入力します。
* マッピングを使用して、標準の構成値を上書きします。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **アカウントID**
  * RtoasterのアカウントID。

* **レコメンド要素ID**
  * Rtoasterレコメンドの対象となる要素のID。
  * 複数のIDをカンマ区切りのリストで入力できます。

* **ポップアップ要素ID**
  * Rtoasterポップアップレコメンドの対象となる要素のID。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`account_id`| <ul><li>文字列</li><li>アカウントID</li></ul> |
|`element_id`| <ul><li>文字列、配列</li><li>要素ID</li></ul> |
|`popup_element_id`| <ul><li>文字列</li><li>ポップアップ要素ID</li></ul> |
|`category`| <ul><li>文字列、配列</li><li>カテゴリー</li></ul> |
|`price_min`| <ul><li>文字列、数値</li><li>最低価格</li></ul> |
|`price_max`| <ul><li>文字列、数値</li><li>最高価格</li></ul> |

### Eコマース

|変数|説明|
|---|---|
|`order_subtotal`| <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_shipping`| <ul><li>送料。</li><li>`_cship`を上書きします。</li></ul> |
|`customer_id`| <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`| <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_quantity`| <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`| <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |