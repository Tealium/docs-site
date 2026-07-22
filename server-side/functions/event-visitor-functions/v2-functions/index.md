---
title: Event and visitor functions V2
description: This article provides information on event and visitor functions that use the V2 runtime.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/v2-functions/
---

<blockquote>
The Action V2 runtime is obsolete and is no longer supported. Functions that use the V2 runtime are still executing but you cannot save code changes. To save code changes, you need to update the runtime version, which may require changes to the function code. For information on the required code changes, see [Migrate a V2 function to the V3 runtime]().
</blockquote>


New functions use the V3 runtime by default. For more information, see [Event and Visitor Functions V3]().

## Named exports

The Tealium module exports five named exports for event and visitor functions: `auth`, `event`, `visitor`, `store`, and `tealium`. Functions import these named exports as follows:

```js
import { auth, visitor, event, store, tealium } from "tealium"; 
```

## Auth object: auth.get()

Event and visitor functions require authentication to access some service providers, such as Facebook or Google. For more information, see [Adding an Authentication to a Function](). When you add an authentication, an access token is returned.

The access token is passed to the `auth.get()` method, which returns an ID for the authentication that can be used in HTTP requests.

| **Parameter** | **Data Type** | **Description** |
| --- | --- | --- |
| authName | string | Specifies the name of the authentication, which is the name entered when the authentication was added to the function. |

## Event object


<blockquote>
Event functions cannot change an event because these functions are invoked after Tealium has processed the event. To change an event, use either event attribute enrichments or an event transformation function. You can also change the event at the data source before it is sent to Tealium.
</blockquote>


The `event` object is available when a function is triggered by the event feed and contains the event data.

| **Property** | **Data Type** | **Description** |
| --- | --- | --- |
| `event.id` | string | Tealium Event ID. |
| `event.visitor_id` | string | Tealium Visitor ID. |
| `event.account` | string | Tealium Account. |
| `event.profile` | string | Tealium Profile. |
| `event.data` | object | An object that contains event attribute data, such as `event.data.udo.page_category` or `event.data.udo.order_id`. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute. `id` is a string that specifies the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute. `id` is a string that specifies the attribute ID. |

### Event object example

The following shows an example of event object data:

```
{
  "account": "your-account",
  "profile": "main",
  "event_id": "run-test-event-id",
  "visitor_id": "run-test-visitor-id",
  "data": {
    "dom": {
      "viewport_height": 766,
      "referrer": "",
      "viewport_width": 1440,
      "domain": "www.example.com",
      "title": "Home Page",
      "query_string": "q=help",
      "hash": "",
      "url": "https://www.example.com/?q=help",
      "pathname": "/"
    },
    "udo": {
      "tealium_event": "page_view",
      "ut.account": "your-account",
      "ut.visitor_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "page_name": "Home Page",
      "ut.event": "view",
      "search_keyword": "help",
      "ut.domain": "example.com",
      "tealium_profile": "main",
      "ut.version": "ut4.46.202006020705",
      "tealium_session_id": "1609910608323",
      "tealium_account": "your-account",
      "ut.profile": "main",
    },
    "firstparty_tealium_cookies": {
      "utag_main__sn": "12",
      "utag_main_dc_visit": "12",
      "utag_main_ses_id": "1609910610822",
      "utag_main_dc_region": "us-east-1",
      "utag_main__st": "1609913306118",
      "utag_main_v_id": "0176cb4f3482110a5ba4702e147b0006d005a065104f2",
      "utag_main__se": "66",
      "utag_main__ss": "0",
      "utag_main_dc_event": "60",
      "utag_main__pn": "5"
    }
  },
  "env": "prod",
  "post_time": 1537305808000
}
```

Event data can be accessed in a function as follows:

```
const data = {};
    // DOM variables are stored in event.dom
    data.current_url = event?.dom?.url;
    // Standard UDO event variables are stored in event.data.udo
    data.session_id = event?.data?.udo?.tealium_session_id;
    // First Party cookies are stored in event.firstparty_tealium_cookies
    data.trace_id = event?.firstparty_tealium_cookies?.trace_id;
    // Meta variables are stored in event.meta
    data.meta_description = event?.meta?.description;
    data.tealium_event = event?.data?.udo?.tealium_event;
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
```

## Store object: store.get()

The `store` object is used to store key-value pairs, referred to as global variables, which can be used to share data with multiple functions. The key is the name of the variable. The value can be a numeric or string constant. You can add, edit, and delete global variables on the **Code** tab of the functions code editor. Functions can retrieve the value of a global variable, but cannot modify it.

V2 functions can retrieve a value for a key by calling the `store.get()` method and passing the key as the parameter.

| **Parameter** | **Data Type** | **Description** |
| --- | --- | --- |
| globalParameterKey | string | Specifies the key of the global variable to get. |

For more information on adding, editing, and using global variables, see [Manage global variables]().

## Tealium object: sendCollectEvent()

The `sendCollectEvent()` method sends an event to Tealium Collect HTTP API and returns a string.

| **Parameter** | **Data Type** | **Description** |
| --- | --- | --- |
| event | EventsClientEventObject | An event object to send to Tealium Collect HTTP API. |
| account | string | (Optional) If specified, replaces the value of event.tealium_account. |
| profile | string | (Optional) If specified, replaces the value of event.tealium_profile. |
| dataSourceId | string | (Optional) If specified, replaces the value of event.tealium_datasource. |

The `Response` interface of the Tealium Collect HTTP API represents the response to a request. The `Response` model is the same as for `fetch` API, except that the URL is not available in the result from the collect client.

## Visitor object


<blockquote>
Visitor functions cannot change a visitor profile because these functions are invoked after Tealium has processed the visitor profile. To change a visitor profile, use visit or visitor attribute enrichments.
</blockquote>


The `visitor` object is available when a function is triggered by the audience feed and contains the visitor data.

| **Property** | **Data Type** | **Description** |
| --- | --- | --- |
| `visitor.metrics` | Record&lt;string, number&gt; | Visitor metrics. |
| `visitor.metrics_sets` | Tally&lt;string, number&gt; |     |
| `visitor.dates` | Record&lt;string, number&gt; | Visitor dates. |
| `visitor.audiences_joined_at` | Record&lt;string, number&gt; | Timestamp when the visitor joined audiences. |
| `visitor.properties` | Record&lt;string, any&gt; | Visitor properties. |
| `visitor.properties.account` | string | Tealium Account. |
| `visitor.properties.profile` | string | Tealium Profile. |
| `visitor.properties.visitor_id` | string | Tealium Visitor ID. |
| `visitor.property_sets` | Set&lt;string, any&gt; |     |
| `visitor.audiences` | string\[\] | List of joined audiences. |
| `visitor.badges` | string\[\] | List of badges. |
| `visitor.creation_ts` | number | Visitor creation timestamp. |
| `visitor.flags` | Map&lt;string, Boolean&gt; |     |
| `visitor.current_visit` | Record&lt;string, any&gt; | Current visit object. |
| `visitor.current_visit.metrics` | Record&lt;string, number&gt; | Current visit metrics. |
| `visitor.current_visit.metrics_sets` | Tally&lt;string, number&gt; |     |
| `visitor.current_visit.dates` | Record&lt;string, number&gt; | Current visit dates. |
| `visitor.current_visit.properties` | Record&lt;string, any&gt; | Current visit properties. |
| `visitor.current_visit.flags` | Map&lt;string, Boolean&gt; | Current visit flags. |
| `visitor.current_visit.property_sets` | Set&lt;string, any&gt; | Current visit property sets. |
| `visitor.current_visit.creation_ts` | number | Current visit creation timestamp. |
| `visitor.current_visit.total_event_count` | number | Current visit total event count. |
| `visitor.current_visit.events_compressed` | boolean | Current visit events compressed. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute. `id` is a string that specifies the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute. `id` is a string that specifies the attribute ID. |

### Visitor object example

The following is an example of visitor object data:

```
{
  "metrics": {
    "Metric 1": 1,
    "Metric 2": 2
  },
  "dates": {
    "Date 1": 1603373790000,
    "Date 2": 1603373522000,
  },
  "properties": {
    "profile": "username",
    "visitor_id": "017560818b67001bc185a07f1cd703078003405000b7e",
    "account": "user-account",
  },
  "audiences": [
    "Audience 1",
    "Audience 2"
  ],
  "badges": [
    "Badge 1",
    "Badge 2"
  ],
  "creation_ts": 1603373522000,
  "current_visit": {
    "metrics": {
      "Metric 1": 1.3,
      "Metric 2": 6,
    },
    "dates": {
      "Date 1": 1603373868000,
      "Date 2": 1603373790000,
    },
    "properties": {
      "Property 1": "Chrome",
      "Property 2": "https://URL-for-website ",
    },
    "flags": {
      "Flag 1": true,
      "Flag 2": false
    },
    "property_sets": {
      "Property Set 1": [
        "Mac desktop"
      ],
      "Property Set 2": [
        "Chrome"
      ]
    },
    "creation_ts": 1603373790000,
    "total_event_count": 2,
    "events_compressed": false
  },
  "audiences_joined_at": {
    "Audience 1": 1603363523014,
    "Audience 2": 1603363523014
  }
}
```