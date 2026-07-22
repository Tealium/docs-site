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


<blockquote>
If your business needs require higher call limits, contact your Tealium account manager.
</blockquote>


## Standard parameters

Tealium Collect supports the following standard parameters in each request:

* `tealium_account`: The name of your Tealium account.
* `tealium_profile`: The name of your Tealium profile. The default is **main**.
* `tealium_datasource`: (Optional) The data source key from Customer Data Hub. See [About data sources](https://docs.tealium.com/about-data-sources/) for more information.
* `tealium_event`: Recommended. The name of the event for tracking purposes.
* `tealium_visitor_id`: Required for AudienceStream. A unique identifier for the visitor associated with the event (see the [Visitor identifiers](#visitor-identifiers) section). Depending on the source of the data, this identifier may be an anonymous GUID (Globally Unique Identifier) that is associated with a device the visitor is using, or may be based on a known user identifier for the visitor.
* `tealium_trace_id`: (Optional) For use with [Trace](https://docs.tealium.com/about-trace/).

The format of the request varies depending on the HTTP method used. In the examples below, placeholder values are represented with curly braces in the following format: `{VALUE}`.

## Custom event parameters

Additional event attributes are sent as custom parameters according to your tracking needs. These parameters should also be defined as event attributes in the Customer Data Hub. For more information about event attributes, see [About attributes](https://docs.tealium.com/about-attributes/).

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
Ensure that your `tealium_visitor_id` is formatted correctly before proceeding. Incorrectly formatted parameters cause errors in AudienceStream and may not track properly.
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
Whether you use anonymous visitors or known visitors, if your API calls do not contain a consistent `tealium_visitor_id`, each event  generates a new visit and visitor stitching will not be possible.
</blockquote>


### User Identifiers

When using AudienceStream, you can pass a known user identifier with a tracking call. For example, `email_address` or `login_id`.

A user identifier is also needed if you are using EventStream and need to provide an ID to a vendor connector.

In AudienceStream, these user identifiers are used to enrich [visitor ID attributes](https://docs.tealium.com/visitor-id-attribute/).

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

For more information and a complete list of user agents recognized as bots, see [server-side-bot-filtering](https://docs.tealium.com/server-side-bot-filtering/).

## Methods


<blockquote>
When sending Collect API traffic from a browser, the GET method bases the page URL on the HTTP referrer URL for the request, which includes only the host name of the current page. Using the GET method does not include the query parameters or pathname of the current page. To include this information, use the POST method.
</blockquote>


### GET

The GET method is used to request data from a specified resource. It passes data using key-value pairs in the query string of the endpoint, and returns a 1x1 transparent GIF to make it compatible with HTML-based implementations.

Example using curl:

```bash
curl -i -X GET "https://collect.tealiumiq.com/event?tealium_account={ACCOUNT}&tealium_profile={PROFILE}&tealium_event=user_login&email_address=user@example.com" 
```

### POST

The POST method is used to send data to a server to create/update a resource. It supports JSON payloads where the request header must be set to `Content-Type: application/json` and the payload must be formatted as a valid JSON string. 

Example of `user_login` event:

```javascript
{
    "tealium_account"   : "ACCOUNT",
    "tealium_profile"   : "PROFILE",
    "tealium_event"     : "EVENT_NAME",
    "email_address"     : "EMAIL_ADDRESS"
}
```

Example using curl:

```bash
curl -X POST -H 'Content-type: application/json'
--data '{"tealium_account":"{ACCOUNT}","tealium_profile":"{PROFILE}","tealium_event":"user_login","email_address":"user@example.com"}'
https://collect.tealiumiq.com/event
```

## Status codes

The following table summarizes Tealium's HTTP response status codes:

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
> GET /event?tealium_account=jentest-as&tealium_profile=&tealium_visitor_id=sendgeteventhttps@testing.com&tealium_datasource=utc2cj&customer_city=Honolulu&customer_state=Hawaii&Flag=true&Number=45&String=ascent&String_Array=[hello,howareyou,whatsup,yoyoyo]&Number_Array=[2.222,3.000,19.12,28.3]&Flag_Array=[true,false,false,true]&Combo_Array=[1,salutations,2324,world,22jjfssl]&Array_of_Array=[[1,2,3],heyworld]&myvariable=unicorns HTTP/1.1
> Host: qa21-collect.tealiumiq.com
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 400 Bad Request
< Cache-Control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< Content-Type: application/json
< Date: Wed, 23 Oct 2019 17:10:51 GMT
< Expires: Wed, 23 Oct 2019 17:10:51 GMT
< P3P: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< Pragma: no-cache
< Vary: Origin
< X-Error: Missing required tealium_account or tealium_profile param value
< X-Region: us-east-1
< X-ServerID: uconnect_i-9a157d19
< X-ULVer: 1.0.331-SNAPSHOT
< X-UUID: d4fc78d1-8204-412c-a6cb-57869d2370a7
< Content-Length: 0
< Connection: keep-alive
```

## Examples

### HTML example

Tealium Collect is referenced in an `<img>` tag within your HTML. Due to browser caching, it's important to include a cache buster, an additional parameter that contains a randomly generated value, as shown in the following example:

```javascript
var cb=Math.random()*100000000000;
```

This variable is added to the query string of the Tealium Collect pixel:

```html
<img height="1" width="1" style="display:none" src="//collect.tealiumiq.com/event?tealium_account={ACCOUNT}&tealium_profile={PROFILE}&tealium_event=user_login&email_address=user@example.com&cb=' + cb + '"/>
```

### JavaScript example

Tealium Collect supports cross-domain requests, allowing you to send a POST from your website to our domain, as shown in the following example:

```javascript
var event = {
    "tealium_account" : "ACCOUNT",
    "tealium_profile" : "PROFILE",
    "tealium_event"   : "EVENT_NAME",
    "email_address"   : "EMAIL_ADDRESS"};
var xhr = new XMLHttpRequest();
xhr.open("POST", "https://collect.tealiumiq.com/event");
xhr.send(JSON.stringify(event));
```

The response headers include the following:  

```javascript
Access-Control-Allow-Origin: [http://your_domain.com](http://your_domain.com)
```
