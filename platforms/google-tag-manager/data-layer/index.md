---
title: Data Layer
description: Learn about the built-in (automatic) data layer variables for the Collect tag in the Google Tag Manager marketplace.
url: https://docs.tealium.com/platforms/google-tag-manager/data-layer/
---
The data layer contains built-in variables that collect basic information about the page being tracked. These variables include cookies, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more](https://docs.tealium.com/data-layer-variables/) about the types of data layer variables available.


## Standard Page Data
The following variables are generated from the standard JavaScript properties available for the web page.

The example values shown are based on the following page URL:

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| Variable              | Description                                                                                              | Example                                                             |
|:----------------------|:---------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------|
| `dom.domain`          | The full domain of the URL. Source: location.hostname                                                    | `www.example.com`                                                   |
| `dom.hash`            | The hash fragment of the URL (excluding the # character). Source: location.hash                          | `hash=fragment`                                                     |
| `dom.pathname`        | The path of the URL, excluding the query parameters and domain. Source: location.pathname                | `"/path/file.html"`                                                 |
| `dom.query_string`    | The full query string of the URL. Source: location.search                                                | `param1=value1`                                                     |
| `dom.referrer`        | URL of previous page. Source: document.referrer                                                          |                                                                     |
| `dom.title`           | Text in the &lt;title&gt; tag. Source: document.title                                                    | `"Page Title" `                                                     |
| `dom.url`             | The full URL of the page. Source: document.URL                                                           | `http://www.example.com/ PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | The height of the browser view port. Source: window.innerHeight or document.documentElement.clientHeight | `1320`                                                              |
| `dom.viewport_width`  | The width of the browser view port. Source: window.innerWidth or document.documentElement.clientWidth    | `1278`                                                              |

## Cookies

The following variables are stored and maintained in a single cookie named `TEAL`. Each is a variable in the `TEAL` object.

| Variable                        | Description                                                        | Example         |
|:--------------------------------|:-------------------------------------------------------------------|:----------------|
| `tealium)_session_event_number` | The number of events in the current session.                       | `2`             |
| `tealium_session_number`        | The number of sessions for this unique visitor.                    | `1`             |
| `tealium_session_id`            | The unique identifier for the session.                             | `1628542077230` |
| `tealium_visitor_id`            | A unique identifier for the visitor. May be 40 characters or more. | `016297481...`  |

The following is an example of the document.cookie format of the TEAL cookie, which shows the variable values separated by `$` characters.

`TEAL=v:927b2ebc092a70110329356772472215264145f9fa1$t:1628543914615$s:1628542077230%3Bexp-sess$sn:1$en:3`

## Tealium Data

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

## Example Data

The following is an example of the built-in data layer that is automatically available.

```
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
## How Data Layer Variables are Flattened

Google Tag Manager events are flattened to Tealium attribute names to meet the Tealium Customer Data Hub specifications. The event data is received by Tealium EventStream.

The value of `tealium_event` is the value of the `event` in the `dataLayer.push` call. Google Tag Manager sets the default page view value to `gtm.js` as the name of the event.  To override the default, set the Tealium Event config setting to a variable that contains the event name.


<blockquote>
Attributes are not automatically added. You must add these attributes in Tealium EventStream.
</blockquote>


## E-Commerce

The following purchase event example shows how the client-side e-commerce events get flattened.

```js
dataLayer.push({
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': 'T12345',    // Transaction ID. Required for purchases and refunds.
        'affiliation': 'Online Store',
        'revenue': '35.43',
        'tax':'4.90',
        'shipping': '5.99',
        'coupon': 'SUMMER_SALE'
      },
      'products': [{
        'name': 'Triblend Android T-Shirt',     // Name or ID is required.
        'id': '12345',
        'price': '15.25',
        'brand': 'Google',
        'category': 'Apparel',
        'variant': 'Gray',
        'quantity': 1,
        'coupon': ''
       },
       {
        'name': 'Donut Friday Scented T-Shirt',
        'id': '67890',
        'price': '33.75',
        'brand': 'Google',
        'category': 'Apparel',
        'variant': 'Black',
        'quantity': 1
       }]
    }
  }
});
```
After flattening, the purchase event becomes:

```js
"ecommerce.purchase.actionField.affiliation": "Online Store"
"ecommerce.purchase.actionField.coupon": "SUMMER_SALE"
"ecommerce.purchase.actionField.id": "T12345"
"ecommerce.purchase.actionField.revenue": "35.43"
"ecommerce.purchase.actionField.shipping": "5.99"
"ecommerce.purchase.actionField.tax": "4.90"
"ecommerce.purchase.products.brand": [ "Google", "Google" ]
"ecommerce.purchase.products.category": [ "Apparel", "Apparel" ]
"ecommerce.purchase.products.coupon": [ "", "" ]
"ecommerce.purchase.products.id": [ "12345", "67890" ]
"ecommerce.purchase.products.name": [ "Triblend Android T-Shirt", "Donut Friday Scented T-Shirt" ]
"ecommerce.purchase.products.price": [ "15.25", "33.75" ]
"ecommerce.purchase.products.variant": [ "Gray", "Black" ]
"ecommerce.purchase.products.quantity": [ "1", "1" ]
```

The flattener uses dot notation to create the key, and the value is set to an array of all values from the purchase event.

## Events

The following `dataLayer.push` command fires when "event" is included in the data layer:

```js
window.dataLayer.push({
  event: "test_number",
  type_number: 5,
  type_string: 'hello',
  type_object: { someKey: 'someValue' },
  type_array: [1,2,3,4],
  type_function: function() { return 'hello'; },
  type_boolean: true
});
```

The data layer that arrives in Tealium EventStream looks as follows.  Only the `type_object` is flattened and the function is removed.

```
{
    "event": "test_number",
    "type_number": 5,
    "type_string": "hello",
    "type_object.someKey": "someValue",
    "type_array": [1, 2, 3, 4],
    "type_boolean": true
}
```
