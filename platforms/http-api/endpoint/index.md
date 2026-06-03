---
title: Endpoint Specification
description: This article describes how to send data to the Tealium Customer Data Hub using the HTTP API for events.
url: https://docs.tealium.com/platforms/http-api/endpoint/
---
This article provides the specification for the direct HTTP endpoint, which is used in any application that sends HTTP requests.

## Tealium Collect URL

Tealium Collect is located at the following root URL: 

```bash
https://collect.tealiumiq.com/event
```

## Rate limits

The Tealium Collect API supports a maximum rate limit of 100 requests/second.

If your business needs require higher call limits, contact your Tealium account manager.

## Standard parameters

Tealium Collect supports the following standard parameters in each request:

* `tealium_account`: The name of your Tealium account.
* `tealium_profile`: The name of your Tealium profile. The default is **main**.
* `tealium_datasource`: (Optional) The data source key from Customer Data Hub. See [About data sources]() for more information.
* `tealium_event`: Recommended. The name of the event for tracking purposes.
* `tealium_visitor_id`: Required for AudienceStream. A unique identifier for the visitor associated with the event (see the [Visitor identifiers](#visitor-identifiers) section). Depending on the source of the data, this identifier may be an anonymous GUID (Globally Unique Identifier) that is associated with a device the visitor is using, or may be based on a known user identifier for the visitor.
* `tealium_trace_id`: (Optional) For use with [Trace]().

The format of the request varies depending on the HTTP method used. In the examples below, placeholder values are represented with curly braces in the following format: `{VALUE}`.

## Custom event parameters

Additional event attributes are sent as custom parameters according to your tracking needs. These parameters should also be defined as event attributes in the Customer Data Hub. For more information about event attributes, see [About attributes]().

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

 Ensure that your `tealium_visitor_id` is formatted correctly before proceeding. Incorrectly formatted parameters cause errors in AudienceStream and may not track properly.

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

 Whether you use anonymous visitors or known visitors, if your API calls do not contain a consistent `tealium_visitor_id`, each event  generates a new visit and visitor stitching will not be possible.

### User Identifiers

When using AudienceStream, you can pass a known user identifier with a tracking call. For example, `email_address` or `login_id`.

A user identifier is also needed if you are using EventStream and need to provide an ID to a vendor connector.

In AudienceStream, these user identifiers are used to enrich [visitor ID attributes]().

### Visitor switching

When a first-party cookie is unavailable, the server side uses incoming data in the following order of precedence to determine the ID of a visitor:

* The `TAPID` cookie, also called the `tealium_thirdparty_visitor_id`
* The `tealium_visitor_id`
* The `utag_main v_id`, also called the `tealium_firstparty_visitor_id`

Because AudienceStream gives the ID in `TAPID` precedence over other IDs to determine the visitor profile to use, this can cause problems with tracking multiple users on the same device.

For example, if a user logs in and their ID is added to the `TAPID`, traffic from all the anonymous users on the device is logged to that user. If a second user logs in to that device, assuming that the anonymous cookie is not cleared, AudienceStream will continue logging activity to the first user. If the visitors use a shared smart television or a public kiosk, this can cause contamination of data in the visitors’ profiles.

Use the following parameters to control how the endpoint handles the `tealium_visitor_id` and `tealium_thirdparty_visitor_id` values in the event:

| Parameter                              | Type       | Description |
| -------------------------------------- | ---------- | ----------- |
| `tealium_override_tapid`               | string     |  Override  `tealium_visitor_id` and `tealium_thirdparty_visitor_id` with this value.           |
| `tealium_skip_3rd_party_vid_cookies`   | boolean    |  Set to `true` to skip collecting the `TAPID` third-party cookie.          |
| `tealium_delete_3rd_party_vid_cookies` | boolean    |  Set to `true` to delete the `TAPID` third-party cookie.           |

* A `tealium_override_tapid` value prevents the `tealium_delete_3rd_party_vid_cookies` parameter from deleting the cookie.
* If removing the `account/profile` information from TAPID empties that cookie, `set-cookie maxAge=0` is returned to delete that cookie from the client.

## Bot filtering

Server-side bot filtering is essential for maintaining the accuracy of data collected through Tealium server-side products.

Bot traffic refers to non-human visits to a site or app. Tealium server-side products automatically filter out bot traffic by comparing the user agent of each event to a list of known bots. Filtered events are not processed and do not count towards your usage.

For more information and a complete list of user agents recognized as bots, see .

## Methods

 When sending Collect API traffic from a browser, the GET method bases the page URL on the HTTP referrer URL for the request, which includes only the host name of the current page. Using the GET method does not include the query parameters or pathname of the current page. To include this information, use the POST method.

### GET

The GET method is used to request data from a specified resource. It passes data using key-value pairs in the query string of the endpoint, and returns a 1x1 transparent GIF to make it compatible with HTML-based implementations.

Example using curl:

```bash
curl -i -X GET &#34;https://collect.tealiumiq.com/event?tealium_account={ACCOUNT}&amp;tealium_profile={PROFILE}&amp;tealium_event=user_login&amp;email_address=user@example.com&#34; 
```

### POST

The POST method is used to send data to a server to create/update a resource. It supports JSON payloads where the request header must be set to `Content-Type: application/json` and the payload must be formatted as a valid JSON string. 

Example of `user_login` event:

```javascript
{
    &#34;tealium_account&#34;   : &#34;ACCOUNT&#34;,
    &#34;tealium_profile&#34;   : &#34;PROFILE&#34;,
    &#34;tealium_event&#34;     : &#34;EVENT_NAME&#34;,
    &#34;email_address&#34;     : &#34;EMAIL_ADDRESS&#34;
}
```

Example using curl:

```bash
curl -X POST -H &#39;Content-type: application/json&#39;
--data &#39;{&#34;tealium_account&#34;:&#34;{ACCOUNT}&#34;,&#34;tealium_profile&#34;:&#34;{PROFILE}&#34;,&#34;tealium_event&#34;:&#34;user_login&#34;,&#34;email_address&#34;:&#34;user@example.com&#34;}&#39;
https://collect.tealiumiq.com/event
```

## Status codes

The following table summarizes Tealium&#39;s HTTP response status codes:

| Status Code | Description |
| --- | --- |
| `200 Status OK` | The request succeeded |
| `400 Bad Request` | The server does not understand the request |

The `400 Bad Request` status code occurs when at least one of the following is true:

- The JSON key contains a period, is invalid, or exceeds 1 MB in size.
- The file-type parameter contains a value other than `json` or `javascript`.
- The combination of `account`, `profile`, and `datalayer_id` exceeds 250 characters in length, or contains restricted characters.
- `tealium_account` or `tealium_profile` is missing, or contains typographical errors.
- The request body is empty.

The following is an example of a `400 Bad Request` response, shown in the `X-Error` header, when the required `tealium_account` or `tealium_profile` parameter values are missing:

```
&gt; GET /event?tealium_account=jentest-as&amp;tealium_profile=&amp;tealium_visitor_id=sendgeteventhttps@testing.com&amp;tealium_datasource=utc2cj&amp;customer_city=Honolulu&amp;customer_state=Hawaii&amp;Flag=true&amp;Number=45&amp;String=ascent&amp;String_Array=[hello,howareyou,whatsup,yoyoyo]&amp;Number_Array=[2.222,3.000,19.12,28.3]&amp;Flag_Array=[true,false,false,true]&amp;Combo_Array=[1,salutations,2324,world,22jjfssl]&amp;Array_of_Array=[[1,2,3],heyworld]&amp;myvariable=unicorns HTTP/1.1
&gt; Host: qa21-collect.tealiumiq.com
&gt; User-Agent: curl/7.54.0
&gt; Accept: */*
&gt;
&lt; HTTP/1.1 400 Bad Request
&lt; Cache-Control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; Content-Type: application/json
&lt; Date: Wed, 23 Oct 2019 17:10:51 GMT
&lt; Expires: Wed, 23 Oct 2019 17:10:51 GMT
&lt; P3P: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; Pragma: no-cache
&lt; Vary: Origin
&lt; X-Error: Missing required tealium_account or tealium_profile param value
&lt; X-Region: us-east-1
&lt; X-ServerID: uconnect_i-9a157d19
&lt; X-ULVer: 1.0.331-SNAPSHOT
&lt; X-UUID: d4fc78d1-8204-412c-a6cb-57869d2370a7
&lt; Content-Length: 0
&lt; Connection: keep-alive
```

## Examples

### HTML example

Tealium Collect is referenced in an `&lt;img&gt;` tag within your HTML. Due to browser caching, it&#39;s important to include a cache buster, an additional parameter that contains a randomly generated value, as shown in the following example:

```javascript
var cb=Math.random()*100000000000;
```

This variable is added to the query string of the Tealium Collect pixel:

```html
&lt;img height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34; src=&#34;//collect.tealiumiq.com/event?tealium_account={ACCOUNT}&amp;tealium_profile={PROFILE}&amp;tealium_event=user_login&amp;email_address=user@example.com&amp;cb=&#39; &#43; cb &#43; &#39;&#34;/&gt;
```

### JavaScript example

Tealium Collect supports cross-domain requests, allowing you to send a POST from your website to our domain, as shown in the following example:

```javascript
var event = {
    &#34;tealium_account&#34; : &#34;ACCOUNT&#34;,
    &#34;tealium_profile&#34; : &#34;PROFILE&#34;,
    &#34;tealium_event&#34;   : &#34;EVENT_NAME&#34;,
    &#34;email_address&#34;   : &#34;EMAIL_ADDRESS&#34;};
var xhr = new XMLHttpRequest();
xhr.open(&#34;POST&#34;, &#34;https://collect.tealiumiq.com/event&#34;);
xhr.send(JSON.stringify(event));
```

The response headers include the following:  

```javascript
Access-Control-Allow-Origin: [http://your_domain.com](http://your_domain.com)
```
