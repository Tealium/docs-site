---
title: AdRoll Smart Pixelタグ設定ガイド（廃止）
description: この記事では、Tealium iQタグ管理アカウントでAdRoll Smart Pixelタグを設定する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adroll-smart-pixel-tag/
---

<blockquote>
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。現在のコネクタについては、[Adroll Pixelタグ設定ガイド](https://docs.tealium.com/adroll-pixel-tag/)をご覧ください。
</blockquote>


## タグのヒント

* 初回のページロード後、`adroll_record_user`オブジェクトのマッピングからデータを取得した`adroll_record_user`関数によって、続けて呼び出しが行われます。
* `name=param`を追加するには、マッピングツールボックスを使用して`adroll_segments`に値をマップします。サンプル値は`checkout`または`orderconfirm`です。
* `_corder`を`adroll_custom_data.ORDER_ID`にマップするなど、マッピングを使用して`adroll_custom_data`の値を設定します。
* `adroll_conversion_value`はE-Commerce Extensionから`_csubtototal`に自動的にマップされます。
* `adroll_conversion_value`パラメータは、Order IDが設定されている場合にのみ設定されます。

## タグの設定

まず、Tealiumのタグマーケットプレイスに移動し、AdRoll Smart Pixelタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の設定を行います：

* **広告主ID**
  * 通常は22文字の英数字です。

* **ピクセルID**
  * 通常は22文字の英数字です。

## データマッピング

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`adroll_custom_data.myvar`|  <ul><li>カスタムデータ</li></ul> |
|`adroll_record_user.myvar`|  <ul><li>カスタムレコードユーザーデータ</li></ul> |
|`adroll_conversion_value`|  <ul><li>コンバージョン値</li></ul> |
|`adroll_currency`|  <ul><li>通貨</li></ul> |
|`adroll_segments`|  <ul><li>セグメント</li></ul> |
|`adroll_email`|  <ul><li>メール</li></ul> |
|`adroll_custom_data.product_id`|  <ul><li>製品ID</li></ul> |
|`adroll_custom_data.product_group`|  <ul><li>製品グループ</li></ul> |
|`adroll_custom_data.product_action`|  <ul><li>製品アクション</li></ul> |
|`adroll_custom_data.product_category_id`|  <ul><li>製品カテゴリ</li></ul> |
|`adroll_adv_id`|  <ul><li>Adv Id</li></ul> |
|`adroll_pix_id`|  <ul><li>Pix Id</li></ul> |
