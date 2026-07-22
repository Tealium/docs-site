---
title: データレイヤー
description: Adobe LaunchマーケットプレイスのCollectタグにおける組み込み（自動）データレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/adobe-launch/data-layer/
---
データレイヤーには、追跡されているページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、クッキー、ページの標準DOM変数、ロードされた構成に関するTealium固有の変数が含まれます。

[詳細を学ぶ](https://docs.tealium.com/data-layer-variables/) データレイヤー変数の種類について。

## 標準ページデータ
以下の変数は、Webページで利用可能な標準JavaScriptプロパティから生成されます。

以下の例の値は、次のページURLに基づいています：

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| 変数| 説明| 例|
|:--------|:-----------|:--------|
| `dom.domain`| URLの完全なドメイン。出典: location.hostname| `www.example.com`|
| `dom.hash`| URLのハッシュフラグメント（#文字を除く）。出典: location.hash| `hash=fragment`|
| `dom.pathname`| クエリパラメータとドメインを除いたURLのパス。出典: location.pathname| `"/path/file.html"`|
| `dom.query_string`| URLの完全なクエリ文字列。出典: location.search| `param1=value1`|
| `dom.referrer`| 前のページのURL。出典: document.referrer||
| `dom.title`| &lt;title&gt;タグのテキスト。出典: document.title| `"Page Title" `|
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
        "cp._ga": "GA1.2.1370368844.1628542067",
        "cp._gid": "GA1.2.73283117.1628542067",
        "tealium_session_number": 1,
        "tealium_session_event_number": 3,
        "tealium_session_id": "1628542077230",
        "tealium_visitor_id": "927b2ebc092a70110329356772472215264145f9fa1",
        "dom.referrer": "",
        "dom.title": "Example dot com",
        "dom.domain": "example.com",
        "dom.query_string": "",
        "dom.hash": "",
        "dom.url": "https://example.com/",
        "dom.pathname": "/",
        "dom.viewport_height": 936,
        "dom.viewport_width": 1517,
        "meta.description": "View",
        "meta.viewport": "width=device-width, initial-scale=1",
        "meta.theme-color": "#13B0E9",
        "tealium_cookie_domain": "example.com",
        "tealium_domain": "example.com",
        "tealium_event": "test event",
        "tealium_account": "xxxxxxxxxxxx",
        "tealium_profile": "main",
        "tealium_environment": "prod",
        "tealium_datasource": "test1234",
        "tealium_random": "9870188345895229",
        "tealium_library_name": "tealium.js",
        "tealium_library_version": "5.0.3",
        "tealium_timestamp_epoch": 1628542114,
        "tealium_timestamp_utc": "2021-08-09T20:48:34.616Z",
        "tealium_timestamp_local": "2021-08-09T13:48:34.616",
        "timing.domain": "example.com",
        "timing.pathname": "/",
        "timing.query_string": "",
        "timing.timestamp": 1628542085435,
        "timing.dns": 1,
        "timing.connect": 99,
        "timing.response": 0,
        "timing.dom_loading_to_interactive": 7,
        "timing.dom_interactive_to_complete": 129,
        "timing.load": 0,
        "timing.time_to_first_byte": 95,
        "timing.front_end": 163,
        "timing.fetch_to_response": 210,
        "timing.fetch_to_complete": 373,
        "timing.fetch_to_interactive": 244
}

```
## データレイヤー変数のフラット化について

Adobe Experience Platform Launchのイベントは、Tealium Customer Data Hubの仕様に合わせて属性名がフラット化されます。

こちらは、フラット化される前のAdobe Experience Platform Launchイベントの例です：

```js
digitalData = {
    product: [{
        productInfo: {
            productID: "4859",
            productName: "Example product",
            description: "Example description",
            productURL: "https://example.com/product.html",
            productImage: "https://example.com/product_image.png",
            productThumbnail: "https://example.com/product_thumbnail.png",
            manufacturer: "Example manufacturer",
            quantity: 1,
            size: "Product size"
        }
    }],
    cart: {
        cartID: "934856",
        price: {
            basePrice: 200.00,
            voucherCode: "EXAMPLEVOUCHER1",
            voucherDiscount: 0.50,
            currency: "USD",
            taxRate: 0.20,
            shipping: 5.00,
            shippingMethod: "UPS",
            priceWithTax: 120,
            cartTotal: 125
        }
    }
}
```

Tealium Collectによって送信されるフラット化されたイベント：

```json
{
    "product.productInfo.productID": ["4859"],
    "product.productInfo.productName": ["Example product"],
    "product.productInfo.description": ["Example description"],
    "product.productInfo.productURL": ["https://example.com/product.html"],
    "product.productInfo.productImage": ["https://example.com/product_image.png"],
    "product.productInfo.productThumbnail": ["https://example.com/product_thumbnail.png"],
    "product.productInfo.manufacturer": ["Example manufacturer"],
    "product.productInfo.quantity": ["1"],
    "product.productInfo.size": ["Product size"],
    "cart.cartID": "934856",
    "cart.price.basePrice": "200.00",
    "cart.price.voucherCode": "EXAMPLEVOUCHER1",
    "cart.price.voucherDiscount": "0.50",
    "cart.price.currency": "USD",
    "cart.price.taxRate": "0.20",
    "cart.price.shipping": "5.00",
    "cart.price.shippingMethod": "UPS",
    "cart.price.priceWithTax": "120",
    "cart.price.cartTotal": "125"
}
```