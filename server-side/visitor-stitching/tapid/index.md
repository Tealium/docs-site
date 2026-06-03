---
title: About TAPID cookies
description: This document explains what the TAPID cookie is and how the Tealium platform uses it.
url: https://docs.tealium.com/server-side/visitor-stitching/tapid/
---
## How it works

TAPID is an HTTP-only browser cookie. It was originally designed to facilitate cross-domain identification, and it stores the [anonymous ID]() that Tealium’s server-side products use, such as AudienceStream.

 If a visitor&#39;s computer doesn&#39;t already have a TAPID cookie set on the [Collect Tag]() target domain, the domain will generate one based on the Collect Tag payload. 

The TAPID cookie&#39;s value is set to that user&#39;s visitor ID. This value normally comes from the client device. TAPID stores the value in a concatenated list of values for the accounts and profiles that a user&#39;s device has visited, using the following format:

```
account-1/profile-1&gt;visitor_id_value-1|account-2/profile-2&gt;visitor_id_value-2
```

TAPID is usually a third-party cookie, but with [first-party domains]() it can be a first-party cookie.

Once set, the `visitor_id_value` in the cookie does not usually change.

### Account and profile values in TAPID

To find the account and profile values for a TAPID cookie on a web page, perform the following steps:

1. In your browser, open a web page that loads a Tealium Collect tag.
1. Open the browser developer console.
1. Filter **Network** requests for `teal`.
1. Refresh the page.
1. Find the collect tag reference (either `i.gif` or `/event`).
1. Examine the request header to determine the target account and profile.
1. Examine the response to see the TAPID cookie value.
1. Extract the part of the TAPID cookie that relates to the account and profile.

## Identity resolution

AudienceStream determines the visitor profile ID based on the following order:

1. The TAPID cookie, also called `tealium_thirdparty_visitor_id`.
1. The `tealium_visitor_id` event attribute.
1. The `utag_main v_id cookie`, also called `tealium_firstparty_visitor_id`.

AudienceStream always uses the TAPID identifier as the primary identifier if it is present in an incoming request. If a user is tracked across two domains, AudienceStream does not use the second domain&#39;s first party cookie to identify the user. Therefore, you cannot look up the user based on the second domain&#39;s first party cookie in AudienceStream.

### Visitor stitching issues

A visitor&#39;s profile data can be contaminated if multiple visitors use a device, such as a shared smart television or a public kiosk. If a second user logs in to that device with an anonymous cookie, AudienceStream continues to log activity to the first user. Traffic from all the anonymous users on a device are logged to the first user in the TAPID cookie.

For more information, see [Visitor Switching](/platforms/http-api/endpoint/#visitor-switching).

### Browser support

As browser support for third-party cookies continues to decline, the ability to track users anonymously across domains is becoming more difficult. With [Visitor Stitching](), AudienceStream can resolve a user across two or more domains when that user identifies themselves in the data layer.

## First-party domains and TAPID  

First-party domains allow Tealium services to use first-party requests, which can reduce data loss caused by ad blockers and similar technology.

The first-party domain is the domain that hosts the website the user is visiting. A third-party domain is any domain that does not match the current website&#39;s domain.

When you use first-party domains, the TAPID cookie remains an HTTP-only browser cookie, but it is assigned to the first-party domain that hosts your website instead of Tealium&#39;s third-party domain. Therefore, first-party domains cause the TAPID cookie to lose its cross-domain tracking functionality.

For more information, see [About First-Party Domains]().

## Change the TAPID cookie data

The API request contains three parameters that allow you to change the value of the TAPID cookie. These parameters only affect the account and profile value in TAPID related to the current incoming request. It does not change any other account and profile values.

The parameters support the following endpoints:

* `i.gif` - [Tealium Collect tag]()
* `vdata` - [Visitor Data Enrichment]()
* `/event` - [HTTP API](/platforms/http-api/endpoint/#visitor-switching)

 The `/event` endpoint can read TAPID values if they are previously set, but it cannot change values in the TAPID cookie. 

| Parameter | Type | Actions | Notes | 
|--------|--------|--------|--------|
| `tealium_override_tapid`  | String  | &lt;ul&gt;&lt;li&gt;Make AudienceStream and server-side products use the provided value as the visitor ID on this event.&lt;/li&gt;&lt;li&gt;For `i.gif` and `vdata`, but not `/event`, change the `Set-Cookie` response header to use the value you pass to change the TAPID.&lt;/li&gt;&lt;/ul&gt; |This parameter enables visitor switching based on the last known user, while retaining a TAPID for cross-domain tracking. |
| `tealium_delete_3rd_party_vid_cookies`  | Boolean |  &lt;ul&gt;&lt;li&gt;Make AudienceStream and server-side products ignore the incoming request value of the TAPID cookie when looking at its order of priority for the visitor profile ID for this event.&lt;/li&gt;&lt;li&gt;For `i.gif` and `vdata`, but not `/event`, change the `Set-Cookie` response header to remove the TAPID for the current account and profile.&lt;/li&gt;&lt;/ul&gt; | |
| `tealium_skip_3rd_party_vid_cookies`  | Boolean | AudienceStream and server-side products ignores the TAPID values for this event. | |

The parameters affect only the current event. For example, if you pass the `skip` parameter on one event and not the next, the next event does not skip the TAPID cookie. However, you can set the `override` parameter once and the TAPID changes to the value you specify.

### Examples

The following examples demonstrate how the three parameters change TAPID data.

#### Override

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie (overridden):  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

##### Event

```
{
  &#34;visitorId&#34;: &#34;user&#34;, // Overridden
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // Overridden
}
```

#### Skip

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie:  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/alt&gt;67890|tealium/main&gt;12345|;
```

##### Event

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPID skipped
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;67890&#34;
}
```

#### Delete

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie (reset):  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/main&gt;12345|;
```

If TAPID is empty after removing `account/profile` part of TAPID, `set-cookie maxAge=0` returned to delete cookie from client altogether. Only for `i.gif` and `vdata`, not `/event`

##### Event

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;,
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;
}
```

#### Override &amp; Skip

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie (overridden):  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

##### Event

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPID Skipped
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // Overridden
}
```

#### Override &amp; Delete

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie:  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

`tealium_override_tapid` has priority over `tealium_delete_3rd_party_vid_cookies`

##### Event

```
{
  &#34;visitorId&#34;: &#34;user&#34;, 
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // Overridden
}
```

#### Skip &amp; Delete

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie (reset):  Only for `i.gif` and `vdata`, not `/event`

```
TAPID=tealium/main&gt;12345|;
```

If TAPID is empty after removing `account/profile` part of TAPID, `set-cookie maxAge=0` returned to delete cookie from client altogether. Only for `i.gif` and `vdata`, not `/event`

##### Event

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPID deleted and anyway skipped
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;
}
```

#### Override, Skip, &amp; Delete

##### Request

**Body:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**Cookie:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### Response

Set Cookie:  Only for `i.gif` and `vdata`, not `/event`


```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

`tealium_override_tapid` has priority over `tealium_delete_3rd_party_vid_cookies`


##### Event

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPID Skipped
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // Overridden
}
```