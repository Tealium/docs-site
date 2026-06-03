---
title: データレイヤー
description: Adobe LaunchマーケットプレイスのCollectタグにおける組み込み（自動）データレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/adobe-launch/data-layer/
---
データレイヤーには、追跡されているページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、クッキー、ページの標準DOM変数、ロードされた構成に関するTealium固有の変数が含まれます。

[詳細を学ぶ]() データレイヤー変数の種類について。

## 標準ページデータ
以下の変数は、Webページで利用可能な標準JavaScriptプロパティから生成されます。

以下の例の値は、次のページURLに基づいています：

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| 変数| 説明| 例|
|:--------|:-----------|:--------|
| `dom.domain`| URLの完全なドメイン。出典: location.hostname| `www.example.com`|
| `dom.hash`| URLのハッシュフラグメント（#文字を除く）。出典: location.hash| `hash=fragment`|
| `dom.pathname`| クエリパラメータとドメインを除いたURLのパス。出典: location.pathname| `&#34;/path/file.html&#34;`|
| `dom.query_string`| URLの完全なクエリ文字列。出典: location.search| `param1=value1`|
| `dom.referrer`| 前のページのURL。出典: document.referrer||
| `dom.title`| &amp;lt;title&amp;gt;タグのテキスト。出典: document.title| `&#34;Page Title&#34; `|
| `dom.url`| ページの完全なURL。出典: document.URL| `http://www.example.com/ PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | ブラウザビューポートの高さ。出典: window.innerHeightまたはdocument.documentElement.clientHeight | `1320`|
| `dom.viewport_width`  | ブラウザビューポートの幅。出典: window.innerWidthまたはdocument.documentElement.clientWidth    | `1278`|

## クッキー

以下の変数は、`TEAL`という名前の単一のクッキーに保存および維持されます。それぞれが`TEAL`オブジェクトの変数です。

| 変数 | 説明 | 例 |
|:---------|:----------- |:------- |
| `tealium_session_event_number` | 現在のセッションのイベント数。 | `2` |
| `tealium_session_number`        | このユニーク訪問のセッション数。 | `1` |
| `tealium_session_id` | セッションのユニーク識別子。                             | `1628542077230` |
| `tealium_visitor_id` | 訪問のユニーク識別子。40文字以上の場合があります。 | `016297481...`  |

以下は、TEALクッキーのdocument.cookie形式の例であり、変数値が`$`文字で区切られて表示されます。

`TEAL=v:927b2ebc092a70110329356772472215264145f9fa1$t:1628543914615$s:1628542077230%3Bexp-sess$sn:1$en:3`

## Tealiumデータ

| 変数                | 名前                              | 例                  |
|:------------------------|:----------------------------------|:-------------------------|
| tealium_account         | アカウント名                      | sandbox                  |
| tealium_datasource      | データソースキー                   | abc123                   |
| tealium_environment     | 公開環境               | prod                     |
| tealium_event           | Tealiumイベント名                | my_event                 |
| tealium_library_name    | ライブラリ名                      | tealium.js               |
| tealium_library_version | ライブラリバージョン                   | 5.0.3                    |
| tealium_profile         | アカウントプロファイル                   | main                     |
| tealium_random          | ランダム数値                     | 7782219645308327         |
| tealium_timestamp_epoch | 現在のUnixタイムスタンプ（秒） | 1522956509               |
| tealium_timestamp_local | ローカルタイムスタンプ                   | 2018-04-05T12:28:29.019  |
| tealium_timestamp_utc   | UTCタイムスタンプ                     | 2018-04-05T19:28:29.019z |
| tealium_cookie_domain   | TEALクッキーが構成されているドメイン   | example.com              |
| tealium_domain          | ウェブサイトのドメイン                 | example.com              |

## 例示データ

以下は、自動的に利用可能な組み込みデータレイヤーの例です。

```json
{
        &#34;cp._ga&#34;: &#34;GA1.2.1370368844.1628542067&#34;,
        &#34;cp._gid&#34;: &#34;GA1.2.73283117.1628542067&#34;,
        &#34;tealium_session_number&#34;: 1,
        &#34;tealium_session_event_number&#34;: 3,
        &#34;tealium_session_id&#34;: &#34;1628542077230&#34;,
        &#34;tealium_visitor_id&#34;: &#34;927b2ebc092a70110329356772472215264145f9fa1&#34;,
        &#34;dom.referrer&#34;: &#34;&#34;,
        &#34;dom.title&#34;: &#34;Example dot com&#34;,
        &#34;dom.domain&#34;: &#34;example.com&#34;,
        &#34;dom.query_string&#34;: &#34;&#34;,
        &#34;dom.hash&#34;: &#34;&#34;,
        &#34;dom.url&#34;: &#34;https://example.com/&#34;,
        &#34;dom.pathname&#34;: &#34;/&#34;,
        &#34;dom.viewport_height&#34;: 936,
        &#34;dom.viewport_width&#34;: 1517,
        &#34;meta.description&#34;: &#34;View&#34;,
        &#34;meta.viewport&#34;: &#34;width=device-width, initial-scale=1&#34;,
        &#34;meta.theme-color&#34;: &#34;#13B0E9&#34;,
        &#34;tealium_cookie_domain&#34;: &#34;example.com&#34;,
        &#34;tealium_domain&#34;: &#34;example.com&#34;,
        &#34;tealium_event&#34;: &#34;test event&#34;,
        &#34;tealium_account&#34;: &#34;xxxxxxxxxxxx&#34;,
        &#34;tealium_profile&#34;: &#34;main&#34;,
        &#34;tealium_environment&#34;: &#34;prod&#34;,
        &#34;tealium_datasource&#34;: &#34;test1234&#34;,
        &#34;tealium_random&#34;: &#34;9870188345895229&#34;,
        &#34;tealium_library_name&#34;: &#34;tealium.js&#34;,
        &#34;tealium_library_version&#34;: &#34;5.0.3&#34;,
        &#34;tealium_timestamp_epoch&#34;: 1628542114,
        &#34;tealium_timestamp_utc&#34;: &#34;2021-08-09T20:48:34.616Z&#34;,
        &#34;tealium_timestamp_local&#34;: &#34;2021-08-09T13:48:34.616&#34;,
        &#34;timing.domain&#34;: &#34;example.com&#34;,
        &#34;timing.pathname&#34;: &#34;/&#34;,
        &#34;timing.query_string&#34;: &#34;&#34;,
        &#34;timing.timestamp&#34;: 1628542085435,
        &#34;timing.dns&#34;: 1,
        &#34;timing.connect&#34;: 99,
        &#34;timing.response&#34;: 0,
        &#34;timing.dom_loading_to_interactive&#34;: 7,
        &#34;timing.dom_interactive_to_complete&#34;: 129,
        &#34;timing.load&#34;: 0,
        &#34;timing.time_to_first_byte&#34;: 95,
        &#34;timing.front_end&#34;: 163,
        &#34;timing.fetch_to_response&#34;: 210,
        &#34;timing.fetch_to_complete&#34;: 373,
        &#34;timing.fetch_to_interactive&#34;: 244
}

```
## データレイヤー変数のフラット化について

Adobe Experience Platform Launchのイベントは、Tealium Customer Data Hubの仕様に合わせて属性名がフラット化されます。

こちらは、フラット化される前のAdobe Experience Platform Launchイベントの例です：

```js
digitalData = {
    product: [{
        productInfo: {
            productID: &#34;4859&#34;,
            productName: &#34;Example product&#34;,
            description: &#34;Example description&#34;,
            productURL: &#34;https://example.com/product.html&#34;,
            productImage: &#34;https://example.com/product_image.png&#34;,
            productThumbnail: &#34;https://example.com/product_thumbnail.png&#34;,
            manufacturer: &#34;Example manufacturer&#34;,
            quantity: 1,
            size: &#34;Product size&#34;
        }
    }],
    cart: {
        cartID: &#34;934856&#34;,
        price: {
            basePrice: 200.00,
            voucherCode: &#34;EXAMPLEVOUCHER1&#34;,
            voucherDiscount: 0.50,
            currency: &#34;USD&#34;,
            taxRate: 0.20,
            shipping: 5.00,
            shippingMethod: &#34;UPS&#34;,
            priceWithTax: 120,
            cartTotal: 125
        }
    }
}
```

Tealium Collectによって送信されるフラット化されたイベント：

```json
{
    &#34;product.productInfo.productID&#34;: [&#34;4859&#34;],
    &#34;product.productInfo.productName&#34;: [&#34;Example product&#34;],
    &#34;product.productInfo.description&#34;: [&#34;Example description&#34;],
    &#34;product.productInfo.productURL&#34;: [&#34;https://example.com/product.html&#34;],
    &#34;product.productInfo.productImage&#34;: [&#34;https://example.com/product_image.png&#34;],
    &#34;product.productInfo.productThumbnail&#34;: [&#34;https://example.com/product_thumbnail.png&#34;],
    &#34;product.productInfo.manufacturer&#34;: [&#34;Example manufacturer&#34;],
    &#34;product.productInfo.quantity&#34;: [&#34;1&#34;],
    &#34;product.productInfo.size&#34;: [&#34;Product size&#34;],
    &#34;cart.cartID&#34;: &#34;934856&#34;,
    &#34;cart.price.basePrice&#34;: &#34;200.00&#34;,
    &#34;cart.price.voucherCode&#34;: &#34;EXAMPLEVOUCHER1&#34;,
    &#34;cart.price.voucherDiscount&#34;: &#34;0.50&#34;,
    &#34;cart.price.currency&#34;: &#34;USD&#34;,
    &#34;cart.price.taxRate&#34;: &#34;0.20&#34;,
    &#34;cart.price.shipping&#34;: &#34;5.00&#34;,
    &#34;cart.price.shippingMethod&#34;: &#34;UPS&#34;,
    &#34;cart.price.priceWithTax&#34;: &#34;120&#34;,
    &#34;cart.price.cartTotal&#34;: &#34;125&#34;
}
```