---
title: Kenshoo Conversionタグ構成ガイド
description: この記事では、Tealium iQタグ管理（TiQ）アカウントでKenshoo Conversionタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kenshoo-conversion-tag/
---## タグのヒント

* E-commerce拡張機能を使用（`_corder`、`_csubtotal`、`_cpromo`、`_ccurrency`）
* 注文ID、金額、プロモーションコード、通貨は自動的に構成されます。これらの値はマッピングを作成することで上書きできます。
* &#39;type&#39;に値をマップすると、動的なConversion Typeを構成できます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Kenshoo ID**
  * URLのサブドメインを指します。
  * 次の例では値は00です：`//00.xg4ken.com/`
* **プロフィールトークン**
  * URLのcidクエリストリングパラメータに適用される長い英数字の値を指します。
* **Conversion Type**
  * この値はconversion typeの詳細を示し、デフォルトでは&#39;conv&#39;に構成されているべきです。
  * この値は、サイト内の他の関連するconversion typeに変更できます。
  * 例えば、登録を追跡したい場合は、それを&#39;reg&#39;に、リードを追跡したい場合は&#39;lead&#39;に変更します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|Conversion Type| (type)|
|Order Amount| (val)|
|Order ID| (orderId)|
|Order Promo Code| (promoCode)|
|Order Currency| (valueCurrency)|

### ベンダーのドキュメンテーション

* [Kenshooガイドシリーズ](http://www.kenshoo.com/guide-series/)
