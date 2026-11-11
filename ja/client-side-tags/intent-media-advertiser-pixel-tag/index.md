---
title: Intent Media Advertiser Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでIntent Media Advertiser Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intent-media-advertiser-pixel-tag/
---## タグに関するヒント

* 次のEコマース変数を使用します
  * `_corder`
  * `_csubtotal`/`_ctotal`
  * `_ccurrency`
  * `_ccustid`
* ページビュータイプ／ページカテゴリーは、マッピングを使用して上書きできます

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **エンティティID**
  * Intent Media Advertiser Pixelによって構成されます。
* **ページビュータイプ**
  * 'HOME'、'LIST'、'DETAILS'、'CART'、'EMAIL'、'EMAIL_CONFIRMATION'、'CONVERSION'、'UNKNOWN'のいずれかである必要があります。
* **商品カテゴリー**
  * 'HOME'、'FLIGHTS'、'CARS'、'HOTELS'、'PACKAGE'、'EMAIL'、'UNKNOWN'のいずれかである必要があります。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`Entity` ID| <ul><li>エンティティID。</li><li>Intent Media Advertiser Pixelによって構成されます。</li></ul> |
|`page_view_type`| <ul><li>ページビュータイプ。</li><li>次のいずれかである必要があります。<ul><li>HOME</li><li>LIST</li><li>DETAILS</li><li>CART</li><li>EMAIL</li><li>EMAIL\_CONFIRMATION</li><li>CONVERSION</li><li>UNKNOWN</li></ul></li></ul> |
|`product_category`| <ul><li>商品カテゴリー。</li><li>次のいずれかである必要があります。<ul><li>HOME</li><li>FLIGHTS</li><li>CARS</li><li>HOTELS</li><li>PACKAGE</li><li>EMAIL</li><li>UNKNOWN</li></ul></li></ul> |
|`page_id`| <ul><li>ページID</li></ul> |

### Eコマース

|変数|説明|
|---|---|
|`order_id`| <ul><li>注文ID。</li><li>デフォルトの`_corder`を上書きします。</li></ul> |
|`order_subtotal`| <ul><li>注文の小計。</li><li>（デフォルトの`_csubtotal`を上書きします。</li></ul> |
|`currency`| <ul><li>通貨。</li><li>デフォルトの`_ccurrency`を上書きします。</li></ul> |
|`custid`| <ul><li>顧客ID。</li><li>デフォルトの`_ccustid`（`user_member_id`）を上書きします。</li></ul> |