---
title: アンプリチュードタグの構成（廃止）
description: この記事では、Tealium iQタグ管理（TiQ）アカウントでアンプリチュードタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-tag/
---
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。現在のコネクタについては、[Amplitude Browser SDKタグ構成ガイド]()を参照してください。

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

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **APIキー**  
Amplitudeから提供されるAPIまたはプロジェクトキー。

## データマッピング

マッピングは、[データレイヤー変数]()からのデータをベンダータグの対応する宛先変数に送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;Amplitudeから提供されるAPIまたはプロジェクトキー。&lt;/li&gt;&lt;/ul&gt; |
|`batchEvents`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`cookieExpiration`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |
|`cookieName`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`deviceId`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`deviceIdFromUrlParam`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`domain`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
| `eventUploadPeriodMillis` |  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |
|`eventUploadThreshold`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |
|`forceHttps`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`includeGclid`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`includeReferrer`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
| `includeUtm` |  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`optOut`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`platform`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`saveEvents`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`savedMaxCount`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |
|`saveParamsReferrerOncePerSession`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;/ul&gt; |
|`sessionTimeout`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |
|`uploadBatchSize`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;/ul&gt; |

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
| `order_id` |  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_type`|  &lt;ul&gt;&lt;li&gt;カートまたは注文タイプ&lt;/li&gt;&lt;li&gt;`_ctype`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt; &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;/ul&gt; &lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
