---
title: Amplitudeタグの構成（非推奨）
description: この記事では、タグ管理アカウントでAmplitudeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-tag/
---

<blockquote>
このコネクタは現在非推奨となっており、タグマーケットプレイスでは利用できません。現在のコネクタについては、[Amplitude Browser SDKタグ構成ガイド](https://docs.tealium.com/amplitude-browser-sdk-tag/)を参照してください。
</blockquote>


## タグに関するヒント

* 注文IDが構成されると、コンバージョンが発生します。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * カートまたは注文タイプ（`_ctype`）
  * 顧客ID（`_ccustid`）
  * 商品IDのリスト（`_cprod`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **APIキー**  
Amplitudeから提供されたAPIキーまたはプロジェクトキー。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`api_key`|  <ul><li>Amplitudeから提供されたAPIキーまたはプロジェクトキー。</li></ul> |
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

これらのマッピングを使用して、所在地、言語、アカウントタイプ、プレイヤータイプなどのユーザープロパティ値を構成および更新するユーザープロパティ操作を制御します。

`custom`をユーザープロパティの名前に変更します。たとえば、ユーザーの言語をマッピングするには、`set.language`のマッピングを作成します。

[Amplitudeのユーザープロパティ](http://Set%20the value, and once set these values cannot be overwritten)の詳細をご覧ください。

|変数| 説明|
|---| ---|
|add.custom| 数値を指定した数だけ増加させる|
|append.custom| プロパティ配列の末尾に値を追加する|
|prepend.custom| プロパティ配列の先頭に値を追加する|
|set.custom| プロパティ値を構成または上書きする|
|setOnce.custom| 値を構成する。一度構成すると、これらの値は上書きできない|
|unset.custom| 値をnullに構成解除する|

### イベント

|変数| 説明|
|---| ---|
|イベント名|
|eventProperties.custom|

### Eコマース

|変数| 説明|
|---| ---|
| `order_id` |  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_type`|  <ul><li>カートまたは注文タイプ</li><li>`_ctype`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul> <ul><li>配列</li><li>価格のリスト</li></ul> </ul> <ul><li>`_cprice`を上書きします。</li></ul> |