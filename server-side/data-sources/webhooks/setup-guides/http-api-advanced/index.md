---
title: HTTP API - Advanced incoming webhook setup guide
description: This article describes how to use the HTTP API - Advanced data source.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/http-api-advanced/
---
## How it works

The HTTP API - Advanced data source is a generic data source that can conditionally parse incoming request bodies. This data source offers an HTTP endpoint that lets you collect real-time event data in a single HTTP call with support for complex objects flattening and batched events. The endpoint is flexible and can be implemented as a tracking pixel in a web page or as a JSON API in your custom application.

This data source is similar to the HTTP API data source, but with additional support for complex JSON objects and batching. 

Events sent using HTTP POST with a complex JSON object will be flattened as follows:

* Event attribute names are created by lower-casing and joining the object properties with an underscore ("\_"). For example:  
Source data: `"alpha" : { "beta" : true }`  
Flattened event attribute: `"alpha_beta" : true`
* Numbers, booleans, and strings inside of an array are preserved.
* Objects and arrays inside of an array are stringified.

Use this data source type when you need to send data in real-time and cannot modify the request to meet format requirements for the standard Tealium Collect endpoint.

### Requirements

* Tealium EventStream or Tealium AudienceStream

### Batched events

The HTTP API - Advanced data source HTTP endpoint supports multiple events in a single request. These events are called batched events. For batched events, you receive one response code based on the status of all records. If a single record/event fails, only that event fails and the rest is processed.

### Rate limits

The HTTP API - Advanced data source supports a maximum rate limit of 100 events/second. 

For example, if you send:

* 1 event per call, you can send 100 calls/second. 
* 10 events per call, you can send 10 calls/second.
* 100 events per call, you can send 1 call/second.

If you exceed the rate limit, Tealium will send an HTTP 429 response indicating too many requests.


<blockquote>
If your business needs require higher event limits, contact your Tealium account manager.
</blockquote>


## POST method

The HTTP API - Advanced data source supports the POST method. For GET method requests, use the [HTTP API](https://docs.tealium.com/platforms/http-api/endpoint-spec/).

Use the following endpoint to access the HTTP API - Advanced data source:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Use the optional `tealium_trace_id` query parameter (`tealium_trace_id=TRACEID`) to support debugging with the Trace tool. For more information about using a trace, see [About Trace](https://docs.tealium.com/about-trace/).


<blockquote>
To find your data source key, navigate to the **Data Sources** dashboard, click the data source you want to use, and copy the key from the **Data Source Key** field.
</blockquote>


## Visitor identifiers

AudienceStream tracks visitors using a combination of:

* **Anonymous ID**: An ID usually used to track the visitor anonymously (for example, from a device or browser). In the case of a [known visitor](#known-visitors-server-to-server), you can use a value based on a user identifier.
* **User Identifier**: Sent after the visitor is known. Based on a value that identifies the user instead of a particular device.

### Anonymous ID

The Anonymous ID is an anonymous identifier used by AudienceStream to associate a visitor between events and visits. Ensure this value is a GUID and consistent for the visitor. This value must also be unique to each server-side profile.

The key name of the anonymous ID is `tealium_visitor_id`.

Depending on your business case, you can use anonymous values or values based on known user identifiers.

#### Anonymous values

|AudienceStream| EventStream|
|---| ---|
| Required | N/A |

If you are using Tealium iQ Tag Management and sending API calls server-to-server to enrich anonymous visitor profiles, then the value of the `tealium_visitor_id` must match the value in the `utag_main_v_id` cookie. For more information about the built-in variables from utag.js, see [JavaScript (Web) > Data Layer](https://docs.tealium.com/platforms/javascript/data-layer/).


<blockquote>
If you are using Adobe Launch or Google Tag Manager, then the value needs to match the `v` part of the **TEAL** cookie.
</blockquote>


#### Known-visitors server-to-server

|AudienceStream| EventStream|
|---| ---|
| Required | Recommended |

When sending data for known visitors (when a value exists for a visitor ID attribute such as `email_address`), include a concatenation of the following:

* Account
* Profile  
Including the profile name ensures the `tealium_visitor_id` is unique to each server-side profile, which is essential when the same visitor profile is sent to multiple server-side profiles within a region.
* Visitor ID attribute ID and value 
<blockquote>
You can find the visitor ID attribute ID next to the attribute name in the attribute list or within the expanded details. For more information, see [About Attributes](https://docs.tealium.com/about-attributes/#attribute-ids).
</blockquote>

* Value in the `tealium_visitor_id` parameter

For example, for the following values:

* Account name: `my-account`
* Profile: `main`
* Visitor ID attribute ID: `7688`
* Customer number value you want to pass: `45653454`

you would concatenate these values in the following way:

```
tealium_visitor_id":"__my-account_main__7688_45653454__"
```


<blockquote>
Ensure that your `tealium_visitor_id` is formatted correctly before proceeding. Incorrectly formatted parameters will cause errors in AudienceStream and may not track properly.
</blockquote>


Example JSON:

```json
{
    "tealium_account"    : "my-account",
    "tealium_profile"    : "main",
    "tealium_event"      : "user_login",
    "email_address"      : "user@example.com",
    "customer_number"    : "45653454", 
    "tealium_visitor_id" : "__my-account_main__7688_45653454__"
}
```


<blockquote>
Whether you use anonymous visitors or known visitors, if your API calls do not contain a consistent `tealium_visitor_id`, each event will generate a new visit and visitor stitching will not be possible.
</blockquote>


### User Identifiers

When using AudienceStream, you can pass a known user identifier with a tracking call. For example, `email_address` or `login_id`.

A user identifier is also needed if you are using EventStream and need to provide an ID to a vendor connector.

In AudienceStream, these user identifiers are used to enrich [visitor ID attributes](https://docs.tealium.com/visitor-id-attribute/).

## Adding the data source

This section provides guidance on how to add the HTTP API - Advanced data source and create a webhook.

Add the HTTP API - Advanced data source before proceeding, then copy the generated endpoint for use in an external system.


<blockquote>
The HTTP API - Advanced endpoint is not active until you add the data source and publish the profile.
</blockquote>


Related: [How to Add a Data Source](https://docs.tealium.com/about-data-sources/)

## Response codes

|Response Code| DESCRIPTION|
|---| ---|
| HTTP 204 | Request Successful|
| HTTP 400 | Malformed JSON request|
| HTTP 404 |

## Examples

The HTTP API - Advanced Incoming Webhook is useful when you want to send an HTTP API Advanced call using JavaScript, bash scripting or curl.

### JSON array as payload

If you pass a JSON array as the entire payload, it will be treated as several events (batching).

```json
[
  {
    "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
    "my_string": "12345a",
    "Detail": {
      "Name": "Event A"
    }
  },
  {
    "tealium_visitor_id": "e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629",
    "my_string": "12345b",
    "Detail": {
      "Name": "Event B"
    }
  }
]
```

This payload will be transformed into several events:

```json
// First Event
  {
    "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
    "my_string": "12345a",
    "detail_name":  "Event A"
  }

  // Second Event
  {
    "tealium_visitor_id": "e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629",
    "my_string": "12345b",
    "detail_name":  "Event B"
  }
```

### JSON array as key-value in a payload

If you pass an array as the value of a key in the payload, the array will be flattened into an array of strings.

For example, the following array:

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
   "events": [
       {
           "id": "1",
           "name": "Event A"
       },
       {
           "id": "2",
           "name": "Event B"
       },
       {
           "id": "3",
           "name": "Event C"
       }
   ]
}

```

will be flattened into the following array of strings:

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
       "events": [
        "{\"id\":\"1\",\"name\":\"Event A\"}",
        "{\"id\":\"2\",\"name\":\"Event B\"}",
        "{\"id\":\"3\",\"name\":\"Event C\"}"
    ]
}

```

For complex business cases or requirements, consider using the [Tealium Event Transformation functions](https://docs.tealium.com/about-data-transformation-functions/) in addition to, or instead of, the HTTP API - Advanced endpoint.

## Complex object

This section provides examples of input code and the resulting (flattened) output for complex objects.

### Before flattening

The following purchase event example shows how client-side e-commerce events with complex objects get flattened.

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
  "ecommerce": {
    "event": "purchase",
    "purchase": {
      "customer": {
        "id": "8237572",
        "email": "john.smith@example.com",
        "city": "San Diego",
        "state": "CA",
        "country": "United States"
      },
      "order": {
        "id": "ORD123456",
        "store": "mobile web",
        "subtotal": "2524.00",
        "total": "2549.00"
      },
      "product": {
          "name": ["Product One", "Product Two"],
          "id": ["PROD123","PROD456"],
          "price": ["12.00","1250.00"],
          "brand": ["Ralph Lauren","Lucky"],
          "category": ["Apparel","Apparel"],
          "quantity": [1,1]
        }
    }
  }
}

```

### After flattening

After flattening, the purchase event becomes:

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
    "ecommerce_event": "purchase",
    "ecommerce_purchase_customer_id": "8237572",
    "ecommerce_purchase_customer_email": "john.smith@example.com",
    "ecommerce_purchase_customer_city": "San Diego",
    "ecommerce_purchase_customer_state": "CA",
    "ecommerce_purchase_customer_country": "United States",
    "ecommerce_purchase_order_id": "ORD123456",
    "ecommerce_purchase_order_store": "mobile web",
    "ecommerce_purchase_order_subtotal": "2524.00",
    "ecommerce_purchase_order_total": "2549.00",
    "ecommerce_purchase_product_name": ["Product One", "Product Two"],
    "ecommerce_purchase_product_id": ["PROD123","PROD456"],
    "ecommerce_purchase_product_price": ["12.00","1250.00"],
    "ecommerce_purchase_product_brand": ["Ralph Lauren","Lucky"],
    "ecommerce_purchase_product_category": ["Apparel","Apparel"],
    "ecommerce_purchase_product_quantity": [1,1]
}

```

## Limitations

* The maximum payload size is 3.5 MB.
* The number of records that can be processed per request is limited by the payload size.
