---
title: Data layer
description: Learn about the built-in (automatic) data layer variables for the Collect tag in the Adobe Launch marketplace.
url: https://docs.tealium.com/platforms/adobe-launch/data-layer/
---
The data layer contains built-in variables that collect basic information about the page being tracked. These variables include cookies, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more](https://docs.tealium.com/data-layer-variables/) about the types of data layer variables available.


## Standard page data
The following variables are generated from the standard JavaScript properties available for the web page.

The example values shown are based on the following page URL:

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| Variable| Description| Example|
|:--------|:-----------|:--------|
| `dom.domain`| The full domain of the URL. Source: location.hostname| `www.example.com`|
| `dom.hash`| The hash fragment of the URL (excluding the # character). Source: location.hash| `hash=fragment`|
| `dom.pathname`| The path of the URL, excluding the query parameters and domain. Source: location.pathname| `"/path/file.html"`|
| `dom.query_string`| The full query string of the URL. Source: location.search| `param1=value1`|
| `dom.referrer`| URL of previous page. Source: document.referrer||
| `dom.title`| Text in the &lt;title&gt; tag. Source: document.title| `"Page Title" `|
| `dom.url`| The full URL of the page. Source: document.URL| `http://www.example.com/ PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | The height of the browser view port. Source: window.innerHeight or document.documentElement.clientHeight | `1320`|
| `dom.viewport_width`  | The width of the browser view port. Source: window.innerWidth or document.documentElement.clientWidth    | `1278`|

## Cookies

The following variables are stored and maintained in a single cookie named `TEAL`. Each is a variable in the `TEAL` object.

| Variable | Description | Example |
|:---------|:----------- |:------- |
| `tealium_session_event_number` | The number of events in the current session. | `2` |
| `tealium_session_number`        | The number of sessions for this unique visitor. | `1` |
| `tealium_session_id` | The unique identifier for the session.                             | `1628542077230` |
| `tealium_visitor_id` | A unique identifier for the visitor. May be 40 characters or more. | `016297481...`  |

The following is an example of the document.cookie format of the TEAL cookie, which shows the variable values separated by `$` characters.

`TEAL=v:927b2ebc092a70110329356772472215264145f9fa1$t:1628543914615$s:1628542077230%3Bexp-sess$sn:1$en:3`

## Tealium data

| Variable                | Name                              | Example                  |
|:------------------------|:----------------------------------|:-------------------------|
| tealium_account         | Account Name                      | sandbox                  |
| tealium_datasource      | Data Source Key                   | abc123                   |
| tealium_environment     | Publish Environment               | prod                     |
| tealium_event           | Tealium Event Name                | my_event                 |
| tealium_library_name    | Library Name                      | tealium.js               |
| tealium_library_version | Library Version                   | 5.0.3                    |
| tealium_profile         | Account Profile                   | main                     |
| tealium_random          | Random Number                     | 7782219645308327         |
| tealium_timestamp_epoch | Current Unix timestamp in seconds | 1522956509               |
| tealium_timestamp_local | Local Timestamp                   | 2018-04-05T12:28:29.019  |
| tealium_timestamp_utc   | UTC Timestamp                     | 2018-04-05T19:28:29.019z |
| tealium_cookie_domain   | Domain where TEAL cookie is set   | example.com              |
| tealium_domain          | Domain of website                 | example.com              |

## Example data

The following is an example of the built-in data layer that is automatically available.

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
## How data layer variables are flattened

Adobe Experience Platform Launch events are converted into flattened attribute names to meet the Tealium Customer Data Hub specifications.

Here is an example of an Adobe Experience Platform Launch event prior to being flattened:

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

The flattened event sent by Tealium Collect:

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
