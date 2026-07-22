---
title: AppsFlyerスマートバナーSDKタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAppsFlyerスマートバナーSDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appsflyer-smart-banner-sdk-tag/
---

People-Based AttributionのWeb-S2S APIは、Web SDKの範囲外でウェブサイト上で発生するイベントをマーケターが報告できるように補完します。

## タグのヒント

* AppsFlyer Web SDKまたはAppsFlyer Smart Banner SDKのどちらか一方を使用します。
* Web Dev Keyを取得するには、AppsFlyerで「My Apps」タブに移動し、「View brand bundles」をクリックします。
* バナーキーを取得するには、AppsFlyerで「Engagement & Deep Linking > Smart Banners」に移動します。
* マッピングを使用して：
  * E-Commerce拡張値を動的に上書きします
  * イベントトリガーを構成します
* 次のE-Commerce拡張値をサポートしています：
  * 注文小計（\_csubtotal）
  * 注文通貨（\_ccurrency）

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[Tag Overview](https://docs.tealium.com/about-tags/)記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Web Dev Key**
* **Your Banner Key**

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### タグ構成

|変数| 説明|
|---| ---|
|Web Dev Key (web\_dev\_key)| [文字列]|
|Your Banner Key (your\_banner\_key)| [文字列]|

### E-Commerce

|変数| 説明|
|---| ---|
|Sub Total (order\_subtotal) (Overrides \_csubtotal)| [文字列]|
|Currency (order\_currency) (Overrides \_ccurrency)| [文字列]|

### イベント

|変数| 説明|
|---| ---|
|Search| search|
|AddToCart| addToCart|
|RemoveFromCart| removeFromCart|
|Purchase| purchase|
|Download| download|
|Signup| signup|
|Subscriptions| subscriptions|
|Custom| Custom|

### イベント固有のパラメータ

|変数| 説明|
|---| ---|
|Search| search|
|AddToCart| addToCart|
|RemoveFromCart| removeFromCart|
|Purchase| purchase|
|Download| download|
|Signup| signup|
|Subscriptions| subscriptions|
|Custom Event| Custom\_Event|

