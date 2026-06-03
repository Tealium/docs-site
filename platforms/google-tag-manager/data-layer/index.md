---
title: Data Layer
description: Learn about the built-in (automatic) data layer variables for the Collect tag in the Google Tag Manager marketplace.
url: https://docs.tealium.com/platforms/google-tag-manager/data-layer/
---
The data layer contains built-in variables that collect basic information about the page being tracked. These variables include cookies, standard DOM variables from the page, and Tealium-specific variables about the loaded configuration.

[Learn more]() about the types of data layer variables available.


## Standard Page Data
The following variables are generated from the standard JavaScript properties available for the web page.

The example values shown are based on the following page URL:

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| Variable              | Description                                                                                              | Example                                                             |
|:----------------------|:---------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------|
| `dom.domain`          | The full domain of the URL. Source: location.hostname                                                    | `www.example.com`                                                   |
| `dom.hash`            | The hash fragment of the URL (excluding the # character). Source: location.hash                          | `hash=fragment`                                                     |
| `dom.pathname`        | The path of the URL, excluding the query parameters and domain. Source: location.pathname                | `&#34;/path/file.html&#34;`                                                 |
| `dom.query_string`    | The full query string of the URL. Source: location.search                                                | `param1=value1`                                                     |
| `dom.referrer`        | URL of previous page. Source: document.referrer                                                          |                                                                     |
| `dom.title`           | Text in the &amp;lt;title&amp;gt; tag. Source: document.title                                                    | `&#34;Page Title&#34; `                                                     |
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
## How Data Layer Variables are Flattened

Google Tag Manager events are flattened to Tealium attribute names to meet the Tealium Customer Data Hub specifications. The event data is received by Tealium EventStream.

The value of `tealium_event` is the value of the `event` in the `dataLayer.push` call. Google Tag Manager sets the default page view value to `gtm.js` as the name of the event.  To override the default, set the Tealium Event config setting to a variable that contains the event name.

Attributes are not automatically added. You must add these attributes in Tealium EventStream.

## E-Commerce

The following purchase event example shows how the client-side e-commerce events get flattened.

```js
dataLayer.push({
  &#39;ecommerce&#39;: {
    &#39;purchase&#39;: {
      &#39;actionField&#39;: {
        &#39;id&#39;: &#39;T12345&#39;,    // Transaction ID. Required for purchases and refunds.
        &#39;affiliation&#39;: &#39;Online Store&#39;,
        &#39;revenue&#39;: &#39;35.43&#39;,
        &#39;tax&#39;:&#39;4.90&#39;,
        &#39;shipping&#39;: &#39;5.99&#39;,
        &#39;coupon&#39;: &#39;SUMMER_SALE&#39;
      },
      &#39;products&#39;: [{
        &#39;name&#39;: &#39;Triblend Android T-Shirt&#39;,     // Name or ID is required.
        &#39;id&#39;: &#39;12345&#39;,
        &#39;price&#39;: &#39;15.25&#39;,
        &#39;brand&#39;: &#39;Google&#39;,
        &#39;category&#39;: &#39;Apparel&#39;,
        &#39;variant&#39;: &#39;Gray&#39;,
        &#39;quantity&#39;: 1,
        &#39;coupon&#39;: &#39;&#39;
       },
       {
        &#39;name&#39;: &#39;Donut Friday Scented T-Shirt&#39;,
        &#39;id&#39;: &#39;67890&#39;,
        &#39;price&#39;: &#39;33.75&#39;,
        &#39;brand&#39;: &#39;Google&#39;,
        &#39;category&#39;: &#39;Apparel&#39;,
        &#39;variant&#39;: &#39;Black&#39;,
        &#39;quantity&#39;: 1
       }]
    }
  }
});
```
After flattening, the purchase event becomes:

```js
&#34;ecommerce.purchase.actionField.affiliation&#34;: &#34;Online Store&#34;
&#34;ecommerce.purchase.actionField.coupon&#34;: &#34;SUMMER_SALE&#34;
&#34;ecommerce.purchase.actionField.id&#34;: &#34;T12345&#34;
&#34;ecommerce.purchase.actionField.revenue&#34;: &#34;35.43&#34;
&#34;ecommerce.purchase.actionField.shipping&#34;: &#34;5.99&#34;
&#34;ecommerce.purchase.actionField.tax&#34;: &#34;4.90&#34;
&#34;ecommerce.purchase.products.brand&#34;: [ &#34;Google&#34;, &#34;Google&#34; ]
&#34;ecommerce.purchase.products.category&#34;: [ &#34;Apparel&#34;, &#34;Apparel&#34; ]
&#34;ecommerce.purchase.products.coupon&#34;: [ &#34;&#34;, &#34;&#34; ]
&#34;ecommerce.purchase.products.id&#34;: [ &#34;12345&#34;, &#34;67890&#34; ]
&#34;ecommerce.purchase.products.name&#34;: [ &#34;Triblend Android T-Shirt&#34;, &#34;Donut Friday Scented T-Shirt&#34; ]
&#34;ecommerce.purchase.products.price&#34;: [ &#34;15.25&#34;, &#34;33.75&#34; ]
&#34;ecommerce.purchase.products.variant&#34;: [ &#34;Gray&#34;, &#34;Black&#34; ]
&#34;ecommerce.purchase.products.quantity&#34;: [ &#34;1&#34;, &#34;1&#34; ]
```

The flattener uses dot notation to create the key, and the value is set to an array of all values from the purchase event.

## Events

The following `dataLayer.push` command fires when &#34;event&#34; is included in the data layer:

```js
window.dataLayer.push({
  event: &#34;test_number&#34;,
  type_number: 5,
  type_string: &#39;hello&#39;,
  type_object: { someKey: &#39;someValue&#39; },
  type_array: [1,2,3,4],
  type_function: function() { return &#39;hello&#39;; },
  type_boolean: true
});
```

The data layer that arrives in Tealium EventStream looks as follows.  Only the `type_object` is flattened and the function is removed.

```
{
    &#34;event&#34;: &#34;test_number&#34;,
    &#34;type_number&#34;: 5,
    &#34;type_string&#34;: &#34;hello&#34;,
    &#34;type_object.someKey&#34;: &#34;someValue&#34;,
    &#34;type_array&#34;: [1, 2, 3, 4],
    &#34;type_boolean&#34;: true
}
```
