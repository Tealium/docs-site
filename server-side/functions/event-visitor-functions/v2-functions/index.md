---
title: Event and visitor functions V2
description: This article provides information on event and visitor functions that use the V2 runtime.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/v2-functions/
---
The Action V2 runtime is obsolete and is no longer supported. Functions that use the V2 runtime are still executing but you cannot save code changes. To save code changes, you need to update the runtime version, which may require changes to the function code. For information on the required code changes, see [Migrate a V2 function to the V3 runtime]().

New functions use the V3 runtime by default. For more information, see [Event and Visitor Functions V3]().

## Named exports

The Tealium module exports five named exports for event and visitor functions: `auth`, `event`, `visitor`, `store`, and `tealium`. Functions import these named exports as follows:

```js
import { auth, visitor, event, store, tealium } from &#34;tealium&#34;; 
```

## Auth object: auth.get()

Event and visitor functions require authentication to access some service providers, such as Facebook or Google. For more information, see [Adding an Authentication to a Function](). When you add an authentication, an access token is returned.

The access token is passed to the `auth.get()` method, which returns an ID for the authentication that can be used in HTTP requests.

| **Parameter** | **Data Type** | **Description** |
| --- | --- | --- |
| authName | string | Specifies the name of the authentication, which is the name entered when the authentication was added to the function. |

## Event object

Event functions cannot change an event because these functions are invoked after Tealium has processed the event. To change an event, use either event attribute enrichments or an event transformation function. You can also change the event at the data source before it is sent to Tealium.

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
  &#34;account&#34;: &#34;your-account&#34;,
  &#34;profile&#34;: &#34;main&#34;,
  &#34;event_id&#34;: &#34;run-test-event-id&#34;,
  &#34;visitor_id&#34;: &#34;run-test-visitor-id&#34;,
  &#34;data&#34;: {
    &#34;dom&#34;: {
      &#34;viewport_height&#34;: 766,
      &#34;referrer&#34;: &#34;&#34;,
      &#34;viewport_width&#34;: 1440,
      &#34;domain&#34;: &#34;www.example.com&#34;,
      &#34;title&#34;: &#34;Home Page&#34;,
      &#34;query_string&#34;: &#34;q=help&#34;,
      &#34;hash&#34;: &#34;&#34;,
      &#34;url&#34;: &#34;https://www.example.com/?q=help&#34;,
      &#34;pathname&#34;: &#34;/&#34;
    },
    &#34;udo&#34;: {
      &#34;tealium_event&#34;: &#34;page_view&#34;,
      &#34;ut.account&#34;: &#34;your-account&#34;,
      &#34;ut.visitor_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;page_name&#34;: &#34;Home Page&#34;,
      &#34;ut.event&#34;: &#34;view&#34;,
      &#34;search_keyword&#34;: &#34;help&#34;,
      &#34;ut.domain&#34;: &#34;example.com&#34;,
      &#34;tealium_profile&#34;: &#34;main&#34;,
      &#34;ut.version&#34;: &#34;ut4.46.202006020705&#34;,
      &#34;tealium_session_id&#34;: &#34;1609910608323&#34;,
      &#34;tealium_account&#34;: &#34;your-account&#34;,
      &#34;ut.profile&#34;: &#34;main&#34;,
    },
    &#34;firstparty_tealium_cookies&#34;: {
      &#34;utag_main__sn&#34;: &#34;12&#34;,
      &#34;utag_main_dc_visit&#34;: &#34;12&#34;,
      &#34;utag_main_ses_id&#34;: &#34;1609910610822&#34;,
      &#34;utag_main_dc_region&#34;: &#34;us-east-1&#34;,
      &#34;utag_main__st&#34;: &#34;1609913306118&#34;,
      &#34;utag_main_v_id&#34;: &#34;0176cb4f3482110a5ba4702e147b0006d005a065104f2&#34;,
      &#34;utag_main__se&#34;: &#34;66&#34;,
      &#34;utag_main__ss&#34;: &#34;0&#34;,
      &#34;utag_main_dc_event&#34;: &#34;60&#34;,
      &#34;utag_main__pn&#34;: &#34;5&#34;
    }
  },
  &#34;env&#34;: &#34;prod&#34;,
  &#34;post_time&#34;: 1537305808000
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

Visitor functions cannot change a visitor profile because these functions are invoked after Tealium has processed the visitor profile. To change a visitor profile, use visit or visitor attribute enrichments.

The `visitor` object is available when a function is triggered by the audience feed and contains the visitor data.

| **Property** | **Data Type** | **Description** |
| --- | --- | --- |
| `visitor.metrics` | Record&amp;lt;string, number&amp;gt; | Visitor metrics. |
| `visitor.metrics_sets` | Tally&amp;lt;string, number&amp;gt; |     |
| `visitor.dates` | Record&amp;lt;string, number&amp;gt; | Visitor dates. |
| `visitor.audiences_joined_at` | Record&amp;lt;string, number&amp;gt; | Timestamp when the visitor joined audiences. |
| `visitor.properties` | Record&amp;lt;string, any&amp;gt; | Visitor properties. |
| `visitor.properties.account` | string | Tealium Account. |
| `visitor.properties.profile` | string | Tealium Profile. |
| `visitor.properties.visitor_id` | string | Tealium Visitor ID. |
| `visitor.property_sets` | Set&amp;lt;string, any&amp;gt; |     |
| `visitor.audiences` | string\[\] | List of joined audiences. |
| `visitor.badges` | string\[\] | List of badges. |
| `visitor.creation_ts` | number | Visitor creation timestamp. |
| `visitor.flags` | Map&amp;lt;string, Boolean&amp;gt; |     |
| `visitor.current_visit` | Record&amp;lt;string, any&amp;gt; | Current visit object. |
| `visitor.current_visit.metrics` | Record&amp;lt;string, number&amp;gt; | Current visit metrics. |
| `visitor.current_visit.metrics_sets` | Tally&amp;lt;string, number&amp;gt; |     |
| `visitor.current_visit.dates` | Record&amp;lt;string, number&amp;gt; | Current visit dates. |
| `visitor.current_visit.properties` | Record&amp;lt;string, any&amp;gt; | Current visit properties. |
| `visitor.current_visit.flags` | Map&amp;lt;string, Boolean&amp;gt; | Current visit flags. |
| `visitor.current_visit.property_sets` | Set&amp;lt;string, any&amp;gt; | Current visit property sets. |
| `visitor.current_visit.creation_ts` | number | Current visit creation timestamp. |
| `visitor.current_visit.total_event_count` | number | Current visit total event count. |
| `visitor.current_visit.events_compressed` | boolean | Current visit events compressed. |
| `function getAttributeNameById(id)` | string | Returns a string containing the name of the specified attribute. `id` is a string that specifies the attribute ID. |
| `function getAttributeValueById(id)` | any | Returns the value of the specified attribute. `id` is a string that specifies the attribute ID. |

### Visitor object example

The following is an example of visitor object data:

```
{
  &#34;metrics&#34;: {
    &#34;Metric 1&#34;: 1,
    &#34;Metric 2&#34;: 2
  },
  &#34;dates&#34;: {
    &#34;Date 1&#34;: 1603373790000,
    &#34;Date 2&#34;: 1603373522000,
  },
  &#34;properties&#34;: {
    &#34;profile&#34;: &#34;username&#34;,
    &#34;visitor_id&#34;: &#34;017560818b67001bc185a07f1cd703078003405000b7e&#34;,
    &#34;account&#34;: &#34;user-account&#34;,
  },
  &#34;audiences&#34;: [
    &#34;Audience 1&#34;,
    &#34;Audience 2&#34;
  ],
  &#34;badges&#34;: [
    &#34;Badge 1&#34;,
    &#34;Badge 2&#34;
  ],
  &#34;creation_ts&#34;: 1603373522000,
  &#34;current_visit&#34;: {
    &#34;metrics&#34;: {
      &#34;Metric 1&#34;: 1.3,
      &#34;Metric 2&#34;: 6,
    },
    &#34;dates&#34;: {
      &#34;Date 1&#34;: 1603373868000,
      &#34;Date 2&#34;: 1603373790000,
    },
    &#34;properties&#34;: {
      &#34;Property 1&#34;: &#34;Chrome&#34;,
      &#34;Property 2&#34;: &#34;https://URL-for-website &#34;,
    },
    &#34;flags&#34;: {
      &#34;Flag 1&#34;: true,
      &#34;Flag 2&#34;: false
    },
    &#34;property_sets&#34;: {
      &#34;Property Set 1&#34;: [
        &#34;Mac desktop&#34;
      ],
      &#34;Property Set 2&#34;: [
        &#34;Chrome&#34;
      ]
    },
    &#34;creation_ts&#34;: 1603373790000,
    &#34;total_event_count&#34;: 2,
    &#34;events_compressed&#34;: false
  },
  &#34;audiences_joined_at&#34;: {
    &#34;Audience 1&#34;: 1603363523014,
    &#34;Audience 2&#34;: 1603363523014
  }
}
```