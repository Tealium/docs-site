---
title: HTTP API - Advanced incoming webhook setup guide
description: This article describes how to use the HTTP API - Advanced data source.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/http-api-advanced/
---
## How it works

The HTTP API - Advanced data source is a generic data source that can conditionally parse incoming request bodies. This data source offers an HTTP endpoint that lets you collect real-time event data in a single HTTP call with support for complex objects flattening and batched events. The endpoint is flexible and can be implemented as a tracking pixel in a web page or as a JSON API in your custom application.

This data source is similar to the HTTP API data source, but with additional support for complex JSON objects and batching. 

Events sent using HTTP POST with a complex JSON object will be flattened as follows:

* Event attribute names are created by lower-casing and joining the object properties with an underscore (&#34;\_&#34;). For example:  
Source data: `&#34;alpha&#34; : { &#34;beta&#34; : true }`  
Flattened event attribute: `&#34;alpha_beta&#34; : true`
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

If your business needs require higher event limits, contact your Tealium account manager.

## POST method

The HTTP API - Advanced data source supports the POST method. For GET method requests, use the [HTTP API]().

Use the following endpoint to access the HTTP API - Advanced data source:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Use the optional `tealium_trace_id` query parameter (`tealium_trace_id=TRACEID`) to support debugging with the Trace tool. For more information about using a trace, see [About Trace]().

To find your data source key, navigate to the **Data Sources** dashboard, click the data source you want to use, and copy the key from the **Data Source Key** field.

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

If you are using Tealium iQ Tag Management and sending API calls server-to-server to enrich anonymous visitor profiles, then the value of the `tealium_visitor_id` must match the value in the `utag_main_v_id` cookie. For more information about the built-in variables from utag.js, see [JavaScript (Web) &gt; Data Layer]().

If you are using Adobe Launch or Google Tag Manager, then the value needs to match the `v` part of the **TEAL** cookie.

#### Known-visitors server-to-server

|AudienceStream| EventStream|
|---| ---|
| Required | Recommended |

When sending data for known visitors (when a value exists for a visitor ID attribute such as `email_address`), include a concatenation of the following:

* Account
* Profile  
Including the profile name ensures the `tealium_visitor_id` is unique to each server-side profile, which is essential when the same visitor profile is sent to multiple server-side profiles within a region.
* Visitor ID attribute ID and value You can find the visitor ID attribute ID next to the attribute name in the attribute list or within the expanded details. For more information, see [About Attributes]().
* Value in the `tealium_visitor_id` parameter

For example, for the following values:

* Account name: `my-account`
* Profile: `main`
* Visitor ID attribute ID: `7688`
* Customer number value you want to pass: `45653454`

you would concatenate these values in the following way:

```
tealium_visitor_id&#34;:&#34;__my-account_main__7688_45653454__&#34;
```

 Ensure that your `tealium_visitor_id` is formatted correctly before proceeding. Incorrectly formatted parameters will cause errors in AudienceStream and may not track properly.

Example JSON:

```json
{
    &#34;tealium_account&#34;    : &#34;my-account&#34;,
    &#34;tealium_profile&#34;    : &#34;main&#34;,
    &#34;tealium_event&#34;      : &#34;user_login&#34;,
    &#34;email_address&#34;      : &#34;user@example.com&#34;,
    &#34;customer_number&#34;    : &#34;45653454&#34;, 
    &#34;tealium_visitor_id&#34; : &#34;__my-account_main__7688_45653454__&#34;
}
```

 Whether you use anonymous visitors or known visitors, if your API calls do not contain a consistent `tealium_visitor_id`, each event will generate a new visit and visitor stitching will not be possible.

### User Identifiers

When using AudienceStream, you can pass a known user identifier with a tracking call. For example, `email_address` or `login_id`.

A user identifier is also needed if you are using EventStream and need to provide an ID to a vendor connector.

In AudienceStream, these user identifiers are used to enrich [visitor ID attributes]().

## Adding the data source

This section provides guidance on how to add the HTTP API - Advanced data source and create a webhook.

Add the HTTP API - Advanced data source before proceeding, then copy the generated endpoint for use in an external system.

The HTTP API - Advanced endpoint is not active until you add the data source and publish the profile. 

Related: [How to Add a Data Source]()

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
    &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
    &#34;my_string&#34;: &#34;12345a&#34;,
    &#34;Detail&#34;: {
      &#34;Name&#34;: &#34;Event A&#34;
    }
  },
  {
    &#34;tealium_visitor_id&#34;: &#34;e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629&#34;,
    &#34;my_string&#34;: &#34;12345b&#34;,
    &#34;Detail&#34;: {
      &#34;Name&#34;: &#34;Event B&#34;
    }
  }
]
```

This payload will be transformed into several events:

```json
// First Event
  {
    &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
    &#34;my_string&#34;: &#34;12345a&#34;,
    &#34;detail_name&#34;:  &#34;Event A&#34;
  }

  // Second Event
  {
    &#34;tealium_visitor_id&#34;: &#34;e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629&#34;,
    &#34;my_string&#34;: &#34;12345b&#34;,
    &#34;detail_name&#34;:  &#34;Event B&#34;
  }
```

### JSON array as key-value in a payload

If you pass an array as the value of a key in the payload, the array will be flattened into an array of strings.

For example, the following array:

```json
{
   &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
   &#34;my_string&#34;: &#34;12345a&#34;,
   &#34;detail_name&#34;: &#34;Event A&#34;,
   &#34;events&#34;: [
       {
           &#34;id&#34;: &#34;1&#34;,
           &#34;name&#34;: &#34;Event A&#34;
       },
       {
           &#34;id&#34;: &#34;2&#34;,
           &#34;name&#34;: &#34;Event B&#34;
       },
       {
           &#34;id&#34;: &#34;3&#34;,
           &#34;name&#34;: &#34;Event C&#34;
       }
   ]
}

```

will be flattened into the following array of strings:

```json
{
   &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
   &#34;my_string&#34;: &#34;12345a&#34;,
   &#34;detail_name&#34;: &#34;Event A&#34;,
       &#34;events&#34;: [
        &#34;{\&#34;id\&#34;:\&#34;1\&#34;,\&#34;name\&#34;:\&#34;Event A\&#34;}&#34;,
        &#34;{\&#34;id\&#34;:\&#34;2\&#34;,\&#34;name\&#34;:\&#34;Event B\&#34;}&#34;,
        &#34;{\&#34;id\&#34;:\&#34;3\&#34;,\&#34;name\&#34;:\&#34;Event C\&#34;}&#34;
    ]
}

```

For complex business cases or requirements, consider using the [Tealium Event Transformation functions]() in addition to, or instead of, the HTTP API - Advanced endpoint.

## Complex object

This section provides examples of input code and the resulting (flattened) output for complex objects.

### Before flattening

The following purchase event example shows how client-side e-commerce events with complex objects get flattened.

```json
{
   &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
   &#34;my_string&#34;: &#34;12345a&#34;,
   &#34;detail_name&#34;: &#34;Event A&#34;,
  &#34;ecommerce&#34;: {
    &#34;event&#34;: &#34;purchase&#34;,
    &#34;purchase&#34;: {
      &#34;customer&#34;: {
        &#34;id&#34;: &#34;8237572&#34;,
        &#34;email&#34;: &#34;john.smith@example.com&#34;,
        &#34;city&#34;: &#34;San Diego&#34;,
        &#34;state&#34;: &#34;CA&#34;,
        &#34;country&#34;: &#34;United States&#34;
      },
      &#34;order&#34;: {
        &#34;id&#34;: &#34;ORD123456&#34;,
        &#34;store&#34;: &#34;mobile web&#34;,
        &#34;subtotal&#34;: &#34;2524.00&#34;,
        &#34;total&#34;: &#34;2549.00&#34;
      },
      &#34;product&#34;: {
          &#34;name&#34;: [&#34;Product One&#34;, &#34;Product Two&#34;],
          &#34;id&#34;: [&#34;PROD123&#34;,&#34;PROD456&#34;],
          &#34;price&#34;: [&#34;12.00&#34;,&#34;1250.00&#34;],
          &#34;brand&#34;: [&#34;Ralph Lauren&#34;,&#34;Lucky&#34;],
          &#34;category&#34;: [&#34;Apparel&#34;,&#34;Apparel&#34;],
          &#34;quantity&#34;: [1,1]
        }
    }
  }
}

```

### After flattening

After flattening, the purchase event becomes:

```json
{
   &#34;tealium_visitor_id&#34;: &#34;503126878d17fcd6bde7df320ff6eb7c278a1c42f&#34;,
   &#34;my_string&#34;: &#34;12345a&#34;,
   &#34;detail_name&#34;: &#34;Event A&#34;,
    &#34;ecommerce_event&#34;: &#34;purchase&#34;,
    &#34;ecommerce_purchase_customer_id&#34;: &#34;8237572&#34;,
    &#34;ecommerce_purchase_customer_email&#34;: &#34;john.smith@example.com&#34;,
    &#34;ecommerce_purchase_customer_city&#34;: &#34;San Diego&#34;,
    &#34;ecommerce_purchase_customer_state&#34;: &#34;CA&#34;,
    &#34;ecommerce_purchase_customer_country&#34;: &#34;United States&#34;,
    &#34;ecommerce_purchase_order_id&#34;: &#34;ORD123456&#34;,
    &#34;ecommerce_purchase_order_store&#34;: &#34;mobile web&#34;,
    &#34;ecommerce_purchase_order_subtotal&#34;: &#34;2524.00&#34;,
    &#34;ecommerce_purchase_order_total&#34;: &#34;2549.00&#34;,
    &#34;ecommerce_purchase_product_name&#34;: [&#34;Product One&#34;, &#34;Product Two&#34;],
    &#34;ecommerce_purchase_product_id&#34;: [&#34;PROD123&#34;,&#34;PROD456&#34;],
    &#34;ecommerce_purchase_product_price&#34;: [&#34;12.00&#34;,&#34;1250.00&#34;],
    &#34;ecommerce_purchase_product_brand&#34;: [&#34;Ralph Lauren&#34;,&#34;Lucky&#34;],
    &#34;ecommerce_purchase_product_category&#34;: [&#34;Apparel&#34;,&#34;Apparel&#34;],
    &#34;ecommerce_purchase_product_quantity&#34;: [1,1]
}

```

## Limitations

* The maximum payload size is 3.5 MB.
* The number of records that can be processed per request is limited by the payload size.
