---
title: Data layer
description: Learn about the built-in (automatic) data layer variables for the Collect tag in the Adobe Launch marketplace.
url: https://docs.tealium.com/platforms/adobe-launch/data-layer/
---
The data layer contains built-in variables that collect basic information about the page being tracked. These variables include cookies, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more]() about the types of data layer variables available.


## Standard page data
The following variables are generated from the standard JavaScript properties available for the web page.

The example values shown are based on the following page URL:

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| Variable| Description| Example|
|:--------|:-----------|:--------|
| `dom.domain`| The full domain of the URL. Source: location.hostname| `www.example.com`|
| `dom.hash`| The hash fragment of the URL (excluding the # character). Source: location.hash| `hash=fragment`|
| `dom.pathname`| The path of the URL, excluding the query parameters and domain. Source: location.pathname| `&#34;/path/file.html&#34;`|
| `dom.query_string`| The full query string of the URL. Source: location.search| `param1=value1`|
| `dom.referrer`| URL of previous page. Source: document.referrer||
| `dom.title`| Text in the &amp;lt;title&amp;gt; tag. Source: document.title| `&#34;Page Title&#34; `|
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
## How data layer variables are flattened

Adobe Experience Platform Launch events are converted into flattened attribute names to meet the Tealium Customer Data Hub specifications.

Here is an example of an Adobe Experience Platform Launch event prior to being flattened:

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

The flattened event sent by Tealium Collect:

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
