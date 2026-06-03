---
title: Webhook actions and parameters
description: This article describes the supported webhook actions and parameters.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/actions-and-parameters/
---
## Actions

The following actions are available for all HTTP-based webhook connectors, regardless of the authentication type.

To use a webhook to send data to a JDBC-compatible database, see [Webhook JDBC]().

### Send Event Data via HTTP Request

| Parameter      | Description |
|:------------------|:-------------|
| Method       | &lt;ul&gt;&lt;li&gt;(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.&lt;/li&gt;&lt;li&gt;If **GET** is selected, the event data is delivered as a JSON URL-encoded query string parameter with the `data` key.&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(Required) Provide URL to submit request to.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate URL from template.&lt;/li&gt;&lt;/ul&gt;    |
| URL Parameters     | &lt;ul&gt;&lt;li&gt;(Optional) Provide parameters to append to URL.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate parameter value from template.&lt;/li&gt;&lt;/ul&gt;  |
| Headers      | &lt;ul&gt;&lt;li&gt;(Optional) Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;     |
| Cookies     | &lt;ul&gt;&lt;li&gt;(Optional) Map cookie values to cookie names.&lt;/li&gt;&lt;li&gt;Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate cookie value from template.&lt;/li&gt;&lt;/ul&gt;     |
| Body Content Type     | &lt;ul&gt;&lt;li&gt;(Optional) Select available type or provide custom value.&lt;/li&gt;&lt;li&gt;All types are UTF-8 encoded and added as a header. For example: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;Content type is required if body data is provided.&lt;/li&gt;&lt;/ul&gt;      |
| Template Variables    | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;   |
| Templates             | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |
| Print Attribute Names | &lt;ul&gt;&lt;li&gt;If attribute names are updated, the names in the payload reflects the update.&lt;/li&gt;&lt;/ul&gt;   |
| Redirection           | &lt;ul&gt;&lt;li&gt;Allow redirection only if the method is GET.&lt;/li&gt;&lt;/ul&gt;  |

### Send Visitor Data via HTTP Request

| Parameter   | Description      |
|:----------------|:------------------|
| Method       | &lt;ul&gt;&lt;li&gt;(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.&lt;/li&gt;&lt;li&gt;If **GET** is selected, the event data is delivered as a JSON URL-encoded query string parameter with the `data` key.&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(Required) Provide URL to submit request to.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate URL from template.&lt;/li&gt;&lt;/ul&gt;    |
| URL Parameters     | &lt;ul&gt;&lt;li&gt;(Optional) Provide parameters to append to URL.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate parameter value from template.&lt;/li&gt;&lt;/ul&gt;  |
| Headers      | &lt;ul&gt;&lt;li&gt;(Optional) Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;     |
| Cookies     | &lt;ul&gt;&lt;li&gt;(Optional) Map cookie values to cookie names.&lt;/li&gt;&lt;li&gt;Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate cookie value from template.&lt;/li&gt;&lt;/ul&gt;     |
| Body Content Type     | &lt;ul&gt;&lt;li&gt;(Optional) Select available type or provide custom value.&lt;/li&gt;&lt;li&gt;All types are UTF-8 encoded and added as a header. For example: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;Content type is required if body data is provided.&lt;/li&gt;&lt;/ul&gt;      |
| Template Variables    | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;   |
| Templates             | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |
| Include Current Visit Data With Visitor Data | &lt;ul&gt;&lt;li&gt;Add the current visit data to the payload.&lt;/li&gt;&lt;li&gt;This includes event visit data if Exclude Current Visit Event Data isn&#39;t selected.&lt;/li&gt;&lt;/ul&gt; |
| Exclude Current Visit Event Data | &lt;ul&gt;&lt;li&gt;Exclude event data from the current visit data.&lt;/li&gt;&lt;/ul&gt; |
| Print Attribute Names      | &lt;ul&gt;&lt;li&gt;If attribute names are updated, the names in the payload reflect the update.&lt;/li&gt;&lt;/ul&gt;     |
| Redirection    | &lt;ul&gt;&lt;li&gt;Allow redirection only if the method is GET.&lt;/li&gt;&lt;/ul&gt;    |

### Send Customized Data via HTTP Request (Advanced)

If your custom request requires a complex payload, such as nested JSON or XML, use the **Templates** option to construct a payload in the format needed by the vendor&#39;s endpoint. For more information, see .

| Parameter     | Description    |
|:-------------------|:---------------------|
| Method    | &lt;ul&gt;&lt;li&gt;(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(Required) Provide URL to submit request to.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate URL from template.&lt;/li&gt;&lt;/ul&gt;     |
| URL Parameters     | &lt;ul&gt;&lt;li&gt;(Optional) Provide parameters to append to URL.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate parameter value from template.&lt;/li&gt;&lt;/ul&gt;|
| Headers    | &lt;ul&gt;&lt;li&gt;(Optional) Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;   |
| Cookies  | &lt;ul&gt;&lt;li&gt;(Optional) Map cookie values to cookie names.&lt;/li&gt;&lt;li&gt;Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate cookie value from template.&lt;/li&gt;&lt;/ul&gt;    |
| Body Content Type  | &lt;ul&gt;&lt;li&gt;(Optional) Select available type or provide custom value.&lt;/li&gt;&lt;li&gt;All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;Content type is required if body data is provided.&lt;/li&gt;&lt;/ul&gt;     |
| Body Data   | &lt;ul&gt;&lt;li&gt;(Optional) Provide data to construct message body.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate body data from template.&lt;/li&gt;&lt;li&gt;Map values to names if body content type is `multipart/form-data` or `application/x-www-form-urlencoded`, otherwise reference template name and select only the **Body** option.&lt;/li&gt;&lt;/ul&gt;   |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;  |
| Templates     | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}} `refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |
| Redirection    | &lt;ul&gt;&lt;li&gt;Allow redirection only if the method is GET.&lt;/li&gt;&lt;/ul&gt;    |

### Send Batched Data via HTTP Request 

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 16 MB

#### Parameters

| Parameter      | Description      |
|:------------|:------------------|
| Method       | &lt;ul&gt;&lt;li&gt;(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(Required) Provide URL to submit request to.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate URL from template.&lt;/li&gt;&lt;/ul&gt;     |
| URL Parameters   | &lt;ul&gt;&lt;li&gt;(Optional) Provide parameters to append to URL.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate parameter value from template.&lt;/li&gt;&lt;/ul&gt; |
| Headers   | &lt;ul&gt;&lt;li&gt;(Optional) Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;    |
| Cookies    | &lt;ul&gt;&lt;li&gt;(Optional) Map cookie values to cookie names.&lt;/li&gt;&lt;li&gt;Cookies are added as single HTTP header value. For example: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate cookie value from template.&lt;/li&gt;&lt;/ul&gt;  |
| Body Content Type     | &lt;ul&gt;&lt;li&gt;(Optional) Select available type or provide custom value.&lt;/li&gt;&lt;li&gt;All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;Content type is required if body data is provided.&lt;/li&gt;&lt;/ul&gt;     |
| Template Variables    | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;   |
| Templates   | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |
| Include Current Visit Data | &lt;ul&gt;&lt;li&gt;Select this checkbox if you want to include current visit data.&lt;/li&gt;&lt;/ul&gt;   |
| Exclude Current Visit Event Data | &lt;ul&gt;&lt;li&gt;Exclude event data from the current visit data.&lt;/li&gt;&lt;/ul&gt; |
| Print Attribute Names      | &lt;ul&gt;&lt;li&gt;If attribute names are updated, the names in the payload reflect the update.&lt;/li&gt;&lt;/ul&gt;     |
| Redirection    | &lt;ul&gt;&lt;li&gt;Allow redirection only if the method is GET.&lt;/li&gt;&lt;/ul&gt;    |
| Timeout | Set the maximum time (in seconds) the system will wait for batch actions to complete when sending data through `HTTP` requests. The minimum value is `1` and the maximum value is `10`. |

### Send Batched Customized Data via HTTP Request (Advanced)

If your custom request requires a complex payload, such as nested JSON or XML, use the **Templates** option to construct a payload in the format needed by the vendor&#39;s endpoint. For more information on using templates for custom requests, see [Send Custom Request - Template Variables Guide]().

 Batching is ignored when using [Trace]().

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Maximum number of requests: 100
* Time since oldest request (Time to Live, TTL): Between 1 and 60 minutes
* Maximum size of requests: 16 MB

#### Parameters

| Parameter      | Description      |
|:------------|:------------------|
| Method       |  &lt;ul&gt;&lt;li&gt;(Required) Select the request method: `GET`, `POST`, `PUT`, `DELETE`, or `PATCH`.&lt;/li&gt;&lt;/ul&gt;      |
| URL     | &lt;ul&gt;&lt;li&gt;(Required) Provide URL to submit request to.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate URL from template.&lt;/li&gt;&lt;/ul&gt;     |
| Body Content Type     | &lt;ul&gt;&lt;li&gt;(Optional) Select available type or provide custom value.&lt;/li&gt;&lt;li&gt;All types are UTF-8 encoded and are added as a header. For example: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;Content type is required if body data is provided.&lt;/li&gt;&lt;/ul&gt;     |
| Body Data    | &lt;ul&gt;&lt;li&gt;(Optional) Provide data to construct message body.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate body data from template.&lt;/li&gt;&lt;li&gt;Map values to names if body content type is `multipart/form-data` or `application/x-www-form-urlencoded`, otherwise reference a template name and select only the `Body` option.&lt;/li&gt;&lt;/ul&gt;     |
| Prefix |  A non-repeating portion of the request that precedes Body Data. The JSON array prefix is the opening bracket character (`[`). Map `Custom [` to **Prefix**. For example:&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| Joiner |  A character or string that separates individual data items in Body Data. The JSON objects joiner is the comma (`,`). Map `Custom ,` to **Joiner**. For example: &lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },  {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ]`  |
| Suffix |  A non-repeating portion of the request that follows Body Data. The JSON array prefix is the closing bracket character (`]`). Map `Custom ]` to **Suffix**. For example:&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| Record Count Maximum   | &lt;ul&gt;&lt;li&gt;Maximum record count.&lt;/li&gt;&lt;/ul&gt;     |
| Time To Live (minutes) | &lt;ul&gt;&lt;li&gt;Time to live, in minutes.&lt;/li&gt;&lt;/ul&gt;       |
| URL Parameters   | &lt;ul&gt;&lt;li&gt;(Optional) Provide parameters to append to URL.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate parameter value from template.&lt;/li&gt;&lt;/ul&gt; |
| Headers   | &lt;ul&gt;&lt;li&gt;(Optional) &gt;Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;    |
| Headers   | &lt;ul&gt;&lt;li&gt;(Optional) Map HTTP header values to header names.&lt;/li&gt;&lt;li&gt;Template Support: reference template name to generate header value from template.&lt;/li&gt;&lt;/ul&gt;    |
| Template Variables    | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;   |
| Templates   | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |
| Timeout | Set the maximum time (in seconds) the system will wait for batch actions to complete when sending data through `HTTP` requests. The minimum value is `1` and the maximum value is `10`. |

## Event Data JSON

The expected JSON payload for events includes all of the standard attributes that are part of the event, as well as additional attributes that are native to the platform that sent the event. For example, events received from a website include DOM and cookie attributes, and events received from a mobile device include device and carrier attributes.

Event data JSON object format example:

```json
{
    &#34;account&#34;: &#34;tealium&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;env&#34;: &#34;prod&#34;,
    &#34;data&#34;: {
        &#34;dom&#34;: {
            &#34;referrer&#34;: &#34;&#34;,
            &#34;domain&#34;: &#34;tealium.com&#34;,
            &#34;title&#34;: &#34;Tealium | Customer Data Hub and Enterprise Tag Management&#34;,
            &#34;query_string&#34;: &#34;&#34;,
            &#34;url&#34;: &#34;http://tealium.com/&#34;,
            &#34;pathname&#34;: &#34;/&#34;
        },
        &#34;udo&#34;: {
            &#34;tealium_event&#34;: &#34;page_view&#34;,
            &#34;page_name&#34;: &#34;Tealium | Customer Data Hub and Enterprise Tag Management&#34;,
            &#34;page_type&#34;: &#34;home&#34;,
            &#34;device_type&#34;: &#34;desktop&#34;
        },
        &#34;firstparty_tealium_cookies&#34;: {
            &#34;trace_id&#34;: &#34;&#34;,
            &#34;s_fid&#34;: &#34;3EF757DF6253B144-0D0194366CD4479B&#34;,
            &#34;utag_main_ses_id&#34;: 1383677957942,
            &#34;s_cc&#34;: &#34;true&#34;,
            &#34;utag_main__st&#34;: 1383678970903,
            &#34;TID&#34;: &#34;2cff51e585ed4a5a9330324d5dbc6bb7&#34;,
            &#34;s_sq&#34;: &#34;[[B]]&#34;
        }
    },
    &#34;post_time&#34;: 1500999541000,
    &#34;useragent&#34;: &#34;PostmanRuntime/6.1.6&#34;,
    &#34;event_id&#34;: &#34;1a1ee055-1456-46f8-ab4d-779628c05dd4&#34;,
    &#34;visitor_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;
}

```

## Visitor Data JSON

The expected JSON payload for visitors includes all of the applicable Visitor attributes for that visitor. The data object is organized by attribute type. If an attribute is not assigned it does not appear in the visitor object. The data for the current visit is also included under the `current_visit` key.

Visitor data JSON object format example:

```json
{
    &#34;metrics&#34;: {
        &#34;Weeks since first visit&#34;: 0.0,
        &#34;Lifetime visit count&#34;: 1.0,
        &#34;Lifetime event count&#34;: 1.0,
        &#34;Total direct visits&#34;: 1.0
    },
    &#34;dates&#34;: {
        &#34;Last visit&#34;: 1500999541000,
        &#34;last_visit_start_ts&#34;: 1500999541000,
        &#34;First visit&#34;: 1500999541000
    },
    &#34;properties&#34;: {
        &#34;profile&#34;: &#34;main&#34;,
        &#34;visitor_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;,
        &#34;account&#34;: &#34;tealium&#34;
    },
    &#34;flags&#34;: {
        &#34;Is Registered&#34;: false
    },
    &#34;audiences&#34;: [
        &#34;New Users&#34;
    ],
    &#34;badges&#34;: [
        &#34;Product Browser&#34;
    ],
    &#34;preloaded&#34;: false,
    &#34;creation_ts&#34;: 1500999541000,
    &#34;_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;,
    &#34;_partition&#34;: 0,
    &#34;shard_token&#34;: 0,
    &#34;current_visit&#34;: {
        &#34;metrics&#34;: {
            &#34;Event count&#34;: 1.0
        },
        &#34;dates&#34;: {
            &#34;Visit start&#34;: 1500999541000,
            &#34;last_event_ts&#34;: 1500999541000
        },
        &#34;properties&#34;: {
            &#34;Active browser type&#34;: &#34;Chrome&#34;,
            &#34;Active operating system&#34;: &#34;MacOS&#34;,
            &#34;Active browser version&#34;: &#34;53&#34;,
            &#34;Active platform&#34;: &#34;browser&#34;,
            &#34;Active device&#34;: &#34;other&#34;
        },
        &#34;flags&#34;: {
            &#34;Direct visit&#34;: true
        },
        &#34;property_sets&#34;: {
            &#34;Active devices&#34;: [
                &#34;other&#34;
            ],
            &#34;Active browser versions&#34;: [
                &#34;53&#34;
            ],
            &#34;Active operating systems&#34;: [
                &#34;MacOS&#34;
            ],
            &#34;Active platforms&#34;: [
                &#34;browser&#34;
            ],
            &#34;Active browser types&#34;: [
                &#34;Chrome&#34;
            ]
        },
        &#34;creation_ts&#34;: 1500999541000,
        &#34;_id&#34;: &#34;9a20caf81d4adc55cfb958da81a513feff62e3324e9f840ed8bf28ca8a39a37d&#34;,
        &#34;shard_token&#34;: 0,
        &#34;_dc_ttl_&#34;: 60000,
        &#34;total_event_count&#34;: 1,
        &#34;events_compressed&#34;: false
    },
    &#34;_dctrace&#34;: [
        &#34;local_visitor_processor_visitor_processor&#34;
    ],
    &#34;new_visitor&#34;: true,
    &#34;audiences_joined_at&#34;: {
        &#34;tealium_main_101&#34;: 1500999542434
    }
}
```