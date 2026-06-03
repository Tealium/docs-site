---
title: AdRoll Smart Pixelタグ設定ガイド（廃止）
description: この記事では、Tealium iQタグ管理アカウントでAdRoll Smart Pixelタグを設定する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adroll-smart-pixel-tag/
---
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。現在のコネクタについては、[Adroll Pixelタグ設定ガイド]()をご覧ください。

## タグのヒント

* 初回のページロード後、`adroll_record_user`オブジェクトのマッピングからデータを取得した`adroll_record_user`関数によって、続けて呼び出しが行われます。
* `name=param`を追加するには、マッピングツールボックスを使用して`adroll_segments`に値をマップします。サンプル値は`checkout`または`orderconfirm`です。
* `_corder`を`adroll_custom_data.ORDER_ID`にマップするなど、マッピングを使用して`adroll_custom_data`の値を設定します。
* `adroll_conversion_value`はE-Commerce Extensionから`_csubtototal`に自動的にマップされます。
* `adroll_conversion_value`パラメータは、Order IDが設定されている場合にのみ設定されます。

## タグの設定

まず、Tealiumのタグマーケットプレイスに移動し、AdRoll Smart Pixelタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の設定を行います：

* **広告主ID**
  * 通常は22文字の英数字です。

* **ピクセルID**
  * 通常は22文字の英数字です。

## データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`adroll_custom_data.myvar`|  &lt;ul&gt;&lt;li&gt;カスタムデータ&lt;/li&gt;&lt;/ul&gt; |
|`adroll_record_user.myvar`|  &lt;ul&gt;&lt;li&gt;カスタムレコードユーザーデータ&lt;/li&gt;&lt;/ul&gt; |
|`adroll_conversion_value`|  &lt;ul&gt;&lt;li&gt;コンバージョン値&lt;/li&gt;&lt;/ul&gt; |
|`adroll_currency`|  &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;/ul&gt; |
|`adroll_segments`|  &lt;ul&gt;&lt;li&gt;セグメント&lt;/li&gt;&lt;/ul&gt; |
|`adroll_email`|  &lt;ul&gt;&lt;li&gt;メール&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_id`|  &lt;ul&gt;&lt;li&gt;製品ID&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_group`|  &lt;ul&gt;&lt;li&gt;製品グループ&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_action`|  &lt;ul&gt;&lt;li&gt;製品アクション&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_category_id`|  &lt;ul&gt;&lt;li&gt;製品カテゴリ&lt;/li&gt;&lt;/ul&gt; |
|`adroll_adv_id`|  &lt;ul&gt;&lt;li&gt;Adv Id&lt;/li&gt;&lt;/ul&gt; |
|`adroll_pix_id`|  &lt;ul&gt;&lt;li&gt;Pix Id&lt;/li&gt;&lt;/ul&gt; |
