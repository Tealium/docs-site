---
title: Webhook actions and parameters
description: This article describes the supported webhook actions and parameters.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/actions-and-parameters/
---
## Actions

The following actions are available for all HTTP-based webhook connectors, regardless of the authentication type.


<blockquote>
To use a webhook to send data to a JDBC-compatible database, see [Webhook JDBC](https://docs.tealium.com/webhook-jdbc/).
</blockquote>


### Send Event Data via HTTP Request

| Parameter      | Description |
|:------------------|:-------------|
| Method       | <ul><li>(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.</li><li>If **GET** is selected, the event data is delivered as a JSON URL-encoded query string parameter with the `data` key.</li></ul>     |
| URL       | <ul><li>(Required) Provide URL to submit request to.</li><li>Template Support: reference template name to generate URL from template.</li></ul>    |
| URL Parameters     | <ul><li>(Optional) Provide parameters to append to URL.</li><li>Template Support: reference template name to generate parameter value from template.</li></ul>  |
| Headers      | <ul><li>(Optional) Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>     |
| Cookies     | <ul><li>(Optional) Map cookie values to cookie names.</li><li>Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`</li><li>Template Support: reference template name to generate cookie value from template.</li></ul>     |
| Body Content Type     | <ul><li>(Optional) Select available type or provide custom value.</li><li>All types are UTF-8 encoded and added as a header. For example: `Content-Type: text/plain; charset=UTF-8`</li><li>Content type is required if body data is provided.</li></ul>      |
| Template Variables    | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>   |
| Templates             | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.</li></ul> |
| Print Attribute Names | <ul><li>If attribute names are updated, the names in the payload reflects the update.</li></ul>   |
| Redirection           | <ul><li>Allow redirection only if the method is GET.</li></ul>  |

### Send Visitor Data via HTTP Request

| Parameter   | Description      |
|:----------------|:------------------|
| Method       | <ul><li>(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.</li><li>If **GET** is selected, the event data is delivered as a JSON URL-encoded query string parameter with the `data` key.</li></ul>     |
| URL       | <ul><li>(Required) Provide URL to submit request to.</li><li>Template Support: reference template name to generate URL from template.</li></ul>    |
| URL Parameters     | <ul><li>(Optional) Provide parameters to append to URL.</li><li>Template Support: reference template name to generate parameter value from template.</li></ul>  |
| Headers      | <ul><li>(Optional) Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>     |
| Cookies     | <ul><li>(Optional) Map cookie values to cookie names.</li><li>Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`</li><li>Template Support: reference template name to generate cookie value from template.</li></ul>     |
| Body Content Type     | <ul><li>(Optional) Select available type or provide custom value.</li><li>All types are UTF-8 encoded and added as a header. For example: `Content-Type: text/plain; charset=UTF-8`</li><li>Content type is required if body data is provided.</li></ul>      |
| Template Variables    | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>   |
| Templates             | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.</li></ul> |
| Include Current Visit Data With Visitor Data | <ul><li>Add the current visit data to the payload.</li><li>This includes event visit data if Exclude Current Visit Event Data isn't selected.</li></ul> |
| Exclude Current Visit Event Data | <ul><li>Exclude event data from the current visit data.</li></ul> |
| Print Attribute Names      | <ul><li>If attribute names are updated, the names in the payload reflect the update.</li></ul>     |
| Redirection    | <ul><li>Allow redirection only if the method is GET.</li></ul>    |

### Send Customized Data via HTTP Request (Advanced)

If your custom request requires a complex payload, such as nested JSON or XML, use the **Templates** option to construct a payload in the format needed by the vendor's endpoint. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).

| Parameter     | Description    |
|:-------------------|:---------------------|
| Method    | <ul><li>(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.</li></ul>     |
| URL     | <ul><li>(Required) Provide URL to submit request to.</li><li>Template Support: reference template name to generate URL from template.</li></ul>     |
| URL Parameters     | <ul><li>(Optional) Provide parameters to append to URL.</li><li>Template Support: reference template name to generate parameter value from template.</li></ul>|
| Headers    | <ul><li>(Optional) Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>   |
| Cookies  | <ul><li>(Optional) Map cookie values to cookie names.</li><li>Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`</li><li>Template Support: reference template name to generate cookie value from template.</li></ul>    |
| Body Content Type  | <ul><li>(Optional) Select available type or provide custom value.</li><li>All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`</li><li>Content type is required if body data is provided.</li></ul>     |
| Body Data   | <ul><li>(Optional) Provide data to construct message body.</li><li>Template Support: reference template name to generate body data from template.</li><li>Map values to names if body content type is `multipart/form-data` or `application/x-www-form-urlencoded`, otherwise reference template name and select only the **Body** option.</li></ul>   |
| Template Variables | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>  |
| Templates     | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}} `refers to the token returned by the authentication request.</li></ul> |
| Redirection    | <ul><li>Allow redirection only if the method is GET.</li></ul>    |

### Send Batched Data via HTTP Request 

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 16 MB

#### Parameters

| Parameter      | Description      |
|:------------|:------------------|
| Method       | <ul><li>(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.</li></ul>     |
| URL     | <ul><li>(Required) Provide URL to submit request to.</li><li>Template Support: reference template name to generate URL from template.</li></ul>     |
| URL Parameters   | <ul><li>(Optional) Provide parameters to append to URL.</li><li>Template Support: reference template name to generate parameter value from template.</li></ul> |
| Headers   | <ul><li>(Optional) Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>    |
| Cookies    | <ul><li>(Optional) Map cookie values to cookie names.</li><li>Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`</li><li>Template Support: reference template name to generate cookie value from template.</li></ul>  |
| Body Content Type     | <ul><li>(Optional) Select available type or provide custom value.</li><li>All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`</li><li>Content type is required if body data is provided.</li></ul>     |
| Template Variables    | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>   |
| Templates   | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.</li></ul> |
| Include Current Visit Data | <ul><li>Select this checkbox if you want to include current visit data.</li></ul>   |
| Exclude Current Visit Event Data | <ul><li>Exclude event data from the current visit data.</li></ul> |
| Print Attribute Names      | <ul><li>If attribute names are updated, the names in the payload reflect the update.</li></ul>     |
| Redirection    | <ul><li>Allow redirection only if the method is GET.</li></ul>    |
| Timeout | Set the maximum time (in seconds) the system will wait for batch actions to complete when sending data through `HTTP` requests. The minimum value is `1` and the maximum value is `10`. |

### Send Batched Customized Data via HTTP Request (Advanced)

If your custom request requires a complex payload, such as nested JSON or XML, use the **Templates** option to construct a payload in the format needed by the vendor's endpoint. For more information on using templates for custom requests, see [Send Custom Request - Template Variables Guide](https://docs.tealium.com/connector-template-variables/).


<blockquote>
Batching is ignored when using [Trace](https://docs.tealium.com/about-trace/).
</blockquote>


#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Maximum number of requests: 100
* Time since oldest request (Time to Live, TTL): Between 1 and 60 minutes
* Maximum size of requests: 16 MB

#### Parameters

| Parameter      | Description      |
|:------------|:------------------|
| Method       |  <ul><li>(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.</li></ul>      |
| URL     | <ul><li>(Required) Provide URL to submit request to.</li><li>Template Support: reference template name to generate URL from template.</li></ul>     |
| Body Content Type     | <ul><li>(Optional) Select available type or provide custom value.</li><li>All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`</li><li>Content type is required if body data is provided.</li></ul>     |
| Body Data    | <ul><li>(Optional) Provide data to construct message body.</li><li>Template Support: reference template name to generate body data from template.</li><li>Map values to names if body content type is `multipart/form-data` or `application/x-www-form-urlencoded`, otherwise reference a template name and select only the `Body` option.</li></ul>     |
| Prefix |  A non-repeating portion of the request that precedes Body Data. The JSON array prefix is the opening bracket character (`[`). Map `Custom [` to **Prefix**. For example:<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| Joiner |  A character or string that separates individual data items in Body Data. The JSON objects joiner is the comma (`,`). Map `Custom ,` to **Joiner**. For example: <br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },  {     "editable_in_signup": true,     "displayed_for_customers": true   } ]`  |
| Suffix |  A non-repeating portion of the request that follows Body Data. The JSON array prefix is the closing bracket character (`]`). Map `Custom ]` to **Suffix**. For example:<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| Record Count Maximum   | <ul><li>Maximum record count.</li></ul>     |
| Time To Live (minutes) | <ul><li>Time to live, in minutes.</li></ul>       |
| URL Parameters   | <ul><li>(Optional) Provide parameters to append to URL.</li><li>Template Support: reference template name to generate parameter value from template.</li></ul> |
| Headers   | <ul><li>(Optional) >Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>    |
| Headers   | <ul><li>(Optional) Map HTTP header values to header names.</li><li>Template Support: reference template name to generate header value from template.</li></ul>    |
| Template Variables    | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>   |
| Templates   | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.</li></ul> |
| Timeout | Set the maximum time (in seconds) the system will wait for batch actions to complete when sending data through `HTTP` requests. The minimum value is `1` and the maximum value is `10`. |

## Event Data JSON

The expected JSON payload for events includes all of the standard attributes that are part of the event, as well as additional attributes that are native to the platform that sent the event. For example, events received from a website include DOM and cookie attributes, and events received from a mobile device include device and carrier attributes.

Event data JSON object format example:

```json
{
    "account": "tealium",
    "profile": "main",
    "env": "prod",
    "data": {
        "dom": {
            "referrer": "",
            "domain": "tealium.com",
            "title": "Tealium | Customer Data Hub and Enterprise Tag Management",
            "query_string": "",
            "url": "http://tealium.com/",
            "pathname": "/"
        },
        "udo": {
            "tealium_event": "page_view",
            "page_name": "Tealium | Customer Data Hub and Enterprise Tag Management",
            "page_type": "home",
            "device_type": "desktop"
        },
        "firstparty_tealium_cookies": {
            "trace_id": "",
            "s_fid": "3EF757DF6253B144-0D0194366CD4479B",
            "utag_main_ses_id": 1383677957942,
            "s_cc": "true",
            "utag_main__st": 1383678970903,
            "TID": "2cff51e585ed4a5a9330324d5dbc6bb7",
            "s_sq": "[[B]]"
        }
    },
    "post_time": 1500999541000,
    "useragent": "PostmanRuntime/6.1.6",
    "event_id": "1a1ee055-1456-46f8-ab4d-779628c05dd4",
    "visitor_id": "1a1ee055145646f8ab4d779628c05dd4"
}

```

## Visitor Data JSON

The expected JSON payload for visitors includes all of the applicable Visitor attributes for that visitor. The data object is organized by attribute type. If an attribute is not assigned it does not appear in the visitor object. The data for the current visit is also included under the `current_visit` key.

Visitor data JSON object format example:

```json
{
    "metrics": {
        "Weeks since first visit": 0.0,
        "Lifetime visit count": 1.0,
        "Lifetime event count": 1.0,
        "Total direct visits": 1.0
    },
    "dates": {
        "Last visit": 1500999541000,
        "last_visit_start_ts": 1500999541000,
        "First visit": 1500999541000
    },
    "properties": {
        "profile": "main",
        "visitor_id": "1a1ee055145646f8ab4d779628c05dd4",
        "account": "tealium"
    },
    "flags": {
        "Is Registered": false
    },
    "audiences": [
        "New Users"
    ],
    "badges": [
        "Product Browser"
    ],
    "preloaded": false,
    "creation_ts": 1500999541000,
    "_id": "1a1ee055145646f8ab4d779628c05dd4",
    "_partition": 0,
    "shard_token": 0,
    "current_visit": {
        "metrics": {
            "Event count": 1.0
        },
        "dates": {
            "Visit start": 1500999541000,
            "last_event_ts": 1500999541000
        },
        "properties": {
            "Active browser type": "Chrome",
            "Active operating system": "MacOS",
            "Active browser version": "53",
            "Active platform": "browser",
            "Active device": "other"
        },
        "flags": {
            "Direct visit": true
        },
        "property_sets": {
            "Active devices": [
                "other"
            ],
            "Active browser versions": [
                "53"
            ],
            "Active operating systems": [
                "MacOS"
            ],
            "Active platforms": [
                "browser"
            ],
            "Active browser types": [
                "Chrome"
            ]
        },
        "creation_ts": 1500999541000,
        "_id": "9a20caf81d4adc55cfb958da81a513feff62e3324e9f840ed8bf28ca8a39a37d",
        "shard_token": 0,
        "_dc_ttl_": 60000,
        "total_event_count": 1,
        "events_compressed": false
    },
    "_dctrace": [
        "local_visitor_processor_visitor_processor"
    ],
    "new_visitor": true,
    "audiences_joined_at": {
        "tealium_main_101": 1500999542434
    }
}
```