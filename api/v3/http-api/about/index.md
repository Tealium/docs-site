---
title: About the Tealium Collect HTTP API
description: Use the HTTP API to send events from any application that can send HTTP requests.
url: https://docs.tealium.com/api/v3/http-api/about/
---
## How it works

The Tealium Collect HTTP API is an authenticated endpoint that supports GET and POST methods for data collection. For the unauthenticated endpoint, see [HTTP API v1](/platforms/http-api/).

```
https://collect.tealiumiq.com/v3/collect/event
```

Sessions are determined based on the [Visit scope]() attribute property.

### Regional and global endpoints

The HTTP API is a cross-regional endpoint that recognizes the region of the account and profile that receives data.

HTTP API supports the following two hosts:

* `collect.tealiumiq.com`  
Sends events to the nearest server (one with the lowest latency).
* `collect-&lt;region&gt;.tealiumiq.com`  
Sends events to the server in the region of the profile.

For authenticated endpoints, the global endpoints are internally mapped to `collect.tealiumiq.com` and regional endpoints are mapped to `collect-&lt;region&gt;.tealiumiq.com`.

### Rate limits

The HTTP API supports a maximum rate limit of 100 events/second. 

For example, if you send:

* 1 event per call, you can send 100 calls/second. 
* 10 events per call, you can send 10 calls/second.

If you exceed the rate limit, Tealium returns an HTTP 429 response to indicate that you have sent too many requests.

If you need higher event limits, contact your Tealium account manager.

## Endpoints

The following endpoints are offered for various data collection purposes:

### Events

A RESTful endpoint that supports GET and POST requests for standard data collection.

| Type | Endpoint |
|----- | -------- | 
| Authenticated global endpoint |  `/v3/collect/event` |
| Authenticated regional endpoint | `/v3/collect/regional/event` |

### Bulk events

A RESTful endpoint that supports POST requests for multiple events (up to 10) in a single request.

| Type | Endpoint |
|----- | -------- | 
| Authenticated bulk global endpoint | `/v3/collect/bulk-event` |
| Authenticated bulk regional endpoint | `/v3/collect/regional/bulk-event` |


### Integrations

A RESTful endpoint used by [incoming webhooks](/server-side/data-sources/webhooks/).

| Type | Endpoint |
|----- | -------- | 
| Authenticated global endpoint |  `/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceID}` |
| Authenticated regional endpoint | `/v3/collect/regional/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceID}` |

## Visitor identifiers

Identify visitors using a combination of:

* **Anonymous ID**: An ID used to track the visitor anonymously (for example, from a device or browser). In the case of a [known visitor](#known-visitors-server-to-server), use a value based on a user identifier.
* **User Identifier**: Sent after the visitor is known. Based on a value that identifies the user instead of a particular device.

### Anonymous ID

The anonymous ID is an anonymous identifier used by Tealium to associate a visitor between events and visits. Ensure this value is a GUID and consistent for the visitor.

The key name of the anonymous ID is `tealium_visitor_id`.

Depending on your business case, use anonymous values or values based on known user identifiers.

#### Anonymous values

|AudienceStream| EventStream|
|---| ---|
| Required | N/A |

If you are using Tealium iQ Tag Management and sending API calls server-to-server to enrich anonymous visitor profiles, then the value of the `tealium_visitor_id` must match the value in the `utag_main_v_id` cookie. For more information about the built-in variables from `utag.js`, see [JavaScript (Web) &gt; Data Layer]().

If you are using Adobe Launch or Google Tag Manager, then the value needs to match the `v` part of the **TEAL** cookie.

#### Known-visitors server-to-server

|AudienceStream| EventStream|
|---| ---|
| Required | Recommended |

When sending data for known visitors (when a value exists for a visitor ID attribute such as `email_address`), concatenate the following values in the format `__ACCOUNT_PROFILE__ATTRIBUTE-ID_ATTRIBUTE-VALUE__`:

* Account
* Profile
* Visitor ID attribute ID and value You can find the visitor ID attribute ID next to the attribute name in the attribute list or within the expanded details. For more information, see [About Attributes]().

For example, if you have the following values:

* Account name: `my-account`
* Profile: `main`
* Visitor ID attribute ID: `7688`
* Visitor ID attribute value: `45653454`

The concatenated value is:

```
&#34;tealium_visitor_id&#34;:&#34;__my-account_main__7688_45653454__&#34;
```

 Ensure that your `tealium_visitor_id` is formatted correctly before proceeding. Incorrectly formatted parameters will cause errors in AudienceStream and may not track properly.

Example JSON:

```json
{
    &#34;tealium_account&#34;    : &#34;my-account&#34;,
    &#34;tealium_profile&#34;    : &#34;main&#34;,
    &#34;tealium_event&#34;      : &#34;user_login&#34;,
    &#34;email_address&#34;      : &#34;user@example.com&#34;,
    &#34;tealium_visitor_id&#34; : &#34;__my-account_main__7688_45653454__&#34;
}
```

Whether you use anonymous visitors or known visitors, if your API calls do not contain a consistent `tealium_visitor_id`, each event generates a new visit and visitor stitching is not possible.

### User Identifiers

When using AudienceStream, pass a known user identifier with a tracking call. For example, `email_address` or `login_id`.

A user identifier is also needed if you are using EventStream and need to provide an ID to a vendor connector.

In AudienceStream, these user identifiers are used to enrich [visitor ID attributes]().

## Permission requirements

* Server-side publisher permission

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().