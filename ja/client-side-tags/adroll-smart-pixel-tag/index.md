---
title: AdRoll Smart Pixelタグ構成ガイド（非推奨）
description: この記事では、タグ管理アカウントでAdRoll Smart Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adroll-smart-pixel-tag/
---

<blockquote>
このコネクタは現在非推奨となっており、タグマーケットプレイスでは利用できません。現在のコネクタについては、[Adroll Pixelタグ構成ガイド](https://docs.tealium.com/adroll-pixel-tag/)を参照してください。
</blockquote>


## タグに関するヒント

* 最初のページ読み込み後、以降の呼び出しは、マッピング内の`adroll_record_user`オブジェクトのデータを使用して`adroll_record_user`関数によって行われます。
* `name=param`を追加するには、マッピングツールボックスを使用して値を`adroll_segments`にマッピングします。値の例には`checkout`や`orderconfirm`があります。
* マッピングを使用して`adroll_custom_data`の値を構成します。たとえば、`_corder`を`adroll_custom_data.ORDER_ID`にマッピングします。
* `adroll_conversion_value`は、E-Commerce Extensionの`_csubtototal`に自動的にマッピングされます。
* `adroll_conversion_value`パラメータは、注文IDが構成されている場合にのみ構成されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **広告主ID**
  * 通常は22文字の英数字です。

* **ピクセルID**
  * 通常は22文字の英数字です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`adroll_custom_data.myvar`|  <ul><li>カスタムデータ</li></ul> |
|`adroll_record_user.myvar`|  <ul><li>カスタムユーザーレコードデータ</li></ul> |
|`adroll_conversion_value`|  <ul><li>コンバージョン値</li></ul> |
|`adroll_currency`|  <ul><li>通貨</li></ul> |
|`adroll_segments`|  <ul><li>セグメント</li></ul> |
|`adroll_email`|  <ul><li>メールアドレス</li></ul> |
|`adroll_custom_data.product_id`|  <ul><li>商品ID</li></ul> |
|`adroll_custom_data.product_group`|  <ul><li>商品グループ</li></ul> |
|`adroll_custom_data.product_action`|  <ul><li>商品アクション</li></ul> |
|`adroll_custom_data.product_category_id`|  <ul><li>商品カテゴリ</li></ul> |
|`adroll_adv_id`|  <ul><li>広告主ID</li></ul> |
|`adroll_pix_id`|  <ul><li>ピクセルID</li></ul> |