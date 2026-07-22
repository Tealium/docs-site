---
title: アンプリチュードタグの構成（廃止）
description: この記事では、Tealium iQタグ管理（TiQ）アカウントでアンプリチュードタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-tag/
---

<blockquote>
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。現在のコネクタについては、[Amplitude Browser SDKタグ構成ガイド](https://docs.tealium.com/amplitude-browser-sdk-tag/)を参照してください。
</blockquote>


## タグのヒント

* 注文IDが構成されるとコンバージョンが発生します。
* 次のE-Commerce拡張パラメータをサポートしています：
  * 注文ID (`_corder`)
  * カートまたは注文タイプ (`_ctype`)
  * 顧客ID (`_ccustid`)
  * 商品IDのリスト ( `_cprod`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **APIキー**  
Amplitudeから提供されるAPIまたはプロジェクトキー。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からのデータをベンダータグの対応する宛先変数に送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`api_key`|  <ul><li>Amplitudeから提供されるAPIまたはプロジェクトキー。</li></ul> |
|`batchEvents`|  <ul><li>ブール値</li></ul> |
|`cookieExpiration`|  <ul><li>数値</li></ul> |
|`cookieName`|  <ul><li>文字列</li></ul> |
|`deviceId`|  <ul><li>文字列</li></ul> |
|`deviceIdFromUrlParam`|  <ul><li>ブール値</li></ul> |
|`domain`|  <ul><li>文字列</li></ul> |
| `eventUploadPeriodMillis` |  <ul><li>数値</li></ul> |
|`eventUploadThreshold`|  <ul><li>数値</li></ul> |
|`forceHttps`|  <ul><li>ブール値</li></ul> |
|`includeGclid`|  <ul><li>ブール値</li></ul> |
|`includeReferrer`|  <ul><li>ブール値</li></ul> |
| `includeUtm` |  <ul><li>ブール値</li></ul> |
|`language`|  <ul><li>文字列</li></ul> |
|`optOut`|  <ul><li>ブール値</li></ul> |
|`platform`|  <ul><li>文字列</li></ul> |
|`saveEvents`|  <ul><li>ブール値</li></ul> |
|`savedMaxCount`|  <ul><li>数値</li></ul> |
|`saveParamsReferrerOncePerSession`|  <ul><li>ブール値</li></ul> |
|`sessionTimeout`|  <ul><li>数値</li></ul> |
|`uploadBatchSize`|  <ul><li>数値</li></ul> |

### ユーザープロパティ

これらのマッピングを使用して、ユーザープロパティの操作を制御し、位置、言語、アカウントタイプ、プレイヤータイプなどのユーザープロパティ値を構成および更新します。

`custom`をユーザープロパティの名前に変更します。例えば、ユーザーの言語をマッピングするには、`set.language`のマッピングを作成します。

[Amplitude User Properties](http://Set%20the value, and once set these values cannot be overwritten)について詳しく学びましょう。

|変数| 説明|
|---| ---|
|add.custom| 指定した数値で数値を増加させる|
|append.custom| プロパティ配列に値を追加する|
|prepend.custom| プロパティ配列の先頭に値を追加する|
|set.custom| プロパティ値を構成または上書きする|
|setOnce.custom| 値を構成し、一度構成するとこれらの値は上書きできない|
|unset.custom| 値をnullに構成する|

### イベント

|変数| 説明|
|---| ---|
|イベント名|
|eventProperties.custom|

### E-Commerce

|変数| 説明|
|---| ---|
| `order_id` |  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_type`|  <ul><li>カートまたは注文タイプ</li><li>`_ctype`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul> <ul><li>配列</li><li>価格のリスト</li></ul> </ul> <ul><li>`_cprice`を上書きします。</li></ul> |
