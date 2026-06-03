---
title: Event parameter
description: This article provides information on the `event` parameter for data transformation functions.
url: https://docs.tealium.com/server-side/functions/data-transformation-functions/event-parameter/
---
Data transformation functions for events from Tealium Collect have one parameter named `event`. The `event` parameter is a metadata object that contains several properties and nested objects describing the event. The actual event data is referenced in the object `event.data.udo`.

For more information, see [Event data object](#event-data-object).

 For transformation functions used with cloud data sources, see [Data record object]().

## Event parameter object

The `event` parameter object contains the following properties:

|**Property**| **Type**| **Description**| **Writable**|
|---| ---| ---| ---|
|`account`| String| Account information.| No|
|`client_ip`| String| Client IP address.| No|
|`data`| Object| See [Event Data Object](#event-data-object).| No|
|`dataSourcePlatform`| String| Name of the data source platform.| No|
|`enrichmentOnly`| Boolean| Always `false` for live events. If `false` DataAccess is enabled, the event can be sent to DataAccess. May be `true` for bulk import events (when `event.type=&#34;BULK_IMPORT&#34;`). If `true`, event data can be used only for enrichment. File import events are not supported for data transformation functions.| No|
|`env`| String| Specifies the execution environment (dev or prod).| No|
|`event_id`| String| Event ID.| No|
|`new_visitor`| Boolean| `true` if this event is the first visit for the user, otherwise `false`.| No|
|`page_url`| Object| An object of URL properties. See [URL Object.](#url-object)&lt;br&gt; Omitted for mobile events.| No|
|`post_time`| Number| Time stamp for the event.| No|
|`profile`| String| Profile for the account.| No|
|`referrer_url`| Object| An object of URL properties. See [URL Object.](#url-object)&lt;br&gt; Omitted for mobile events.| No|
|`type`| String| Specifies whether the event is from a live visit or a bulk import event. Values are `LIVE` or `BULK_IMPORT`. File import events are not currently supported for data transformation functions.| No|
|`useragent`| String| Specifies the software the user is using, such as the web browser.| No|
|`visitor_id`| String| Visitor ID.| No|
|`_forwarding_visitor_ids`| String[]| Contains the IDs of the visitors forwarding this event. Used in the visitor stitching process.| No|

### Data source platform values

The value of the `dataSourcePlatform` property can be one of the following: `default`, `adobe_launch`, `affirm`, `android`, `braze`, `cordova`, `cSharp`, `fileImport`, `googleAMP`, `google_tag_manager`, `http_api_flattened`, `hubspot_wf`, `intercom`, `iOS`, `iterable`, `java`, `javascript`, `mailchimp`, `python`, `RES`, `roku`, `salesforce`, `sendgrid`, `slack`, `swift`, `tiqJavascript`, `tvOS`, `watchOS`, `zapier`.

File import events are not currently supported for data transformation functions.

## Event data object

The `event.data` object represents the incoming event and contains the `event.data.udo` object that can be transformed:

| Property | Type | Description | Writable |
|---| ---| ---| ---|
|`dom`| Object| Contains information about the page on which the event occurred (domain, query string, etc.) Omitted for mobile events. For more information, see [Data Layer](https://docs.tealium.com/platforms/javascript/data-layer/).| No|
|`firstparty_tealium_cookies`| Object| Object contains cookie properties specified in your data layer.&lt;br&gt; Omitted for mobile events.| No|
|`js`| Object| Object contains JavaScript variable properties specified in your data layer.&lt;br&gt; Omitted for mobile events.| No|
|`meta`| Object| Object contains metadata properties specified in your data layer.&lt;br&gt; Omitted for mobile events.| No|
|`udo`| Object| Object contains the properties of the incoming event. Some properties are read-only. See [Writable Properties](#writable-properties).| Yes|

### Writable properties

All custom event attributes in `event.data.udo` are writable, but only some `tealium_` properties can be modified.

The following `tealium_` properties can be modified, but not deleted:

* `event.data.udo.tealium_datasource`
* `event.data.udo.tealium_environment`
* `event.data.udo.tealium_event`
* `event.data.udo.tealium_firstparty_visitor_id`
* `event.data.udo.tealium_thirdparty_visitor_id`
* `event.data.udo.tealium_library_name`
* `event.data.udo.tealium_library_version`
* `event.data.udo.tealium_random`
* `event.data.udo.tealium_timestamp_epoch`
* `event.data.udo.tealium_timestamp_local`
* `event.data.udo.tealium_timestamp_utc`
* `event.data.udo.tealium_session_number`

### Read-Only properties

The following object properties are read-only and cannot be modified:

* `event.data.udo.tealium_cf_ttl`
* `event.data.udo._dc_ttl_`
* `event.data.udo.platform`
* `event.data.udo.tealium_visitor_id`
* `event.data.udo.tealium_account`
* `event.data.udo.tealium_profile`
* `event.data.udo.tealium_session_id`

## URL object

The URL object contains the following standard URL properties:

| Property | Type | Description | Writable |
|---| ---| ---| ---|
|`domain`| String| Domain of the URL.| No|
|`full_url`| String| Full URL.| No|
|`path`| String| Path from the URL. May be empty.| No|
|`query_params`| Object| An Object that contains one or more key.value pairs. Each key-value pair specifies a query string in the URL. For example:&lt;br&gt; ```&#34;query_params&#34;: { &#34;utm_medium&#34;: &#34;PPC&#34;, &#34;utm_source&#34;: &#34;LinkedIn&#34; }```| No|
|`querystring`| String| Query string from the URL.| No|
|`scheme`| String| Specifies the protocol to use for the web site, such as HTTP or HTTPS.| No|

## Example event parameter object

The following shows an example `event` parameter object:

```json
{
    &#34;account&#34;: &#34;XYZ_admin_acct&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;env&#34;: &#34;prod&#34;,
    &#34;data&#34;: {
        &#34;dom&#34;: {
            &#34;url&#34;: &#34;https://www.example.com&#34;,
            &#34;pathname&#34;: &#34;/&#34;,
            &#34;domain&#34;: &#34;example.com&#34;,
            &#34;hash&#34;: &#34;&#34;,
            &#34;query_string&#34;: &#34;&#34;,
            &#34;title&#34;: &#34;Homepage&#34;
        },
	&#34;js&#34;: {},
	&#34;meta&#34;: {},
	&#34;udo&#34;: {
            &#34;page_view&#34;: &#34;view&#34;,
            &#34;tealium_account&#34;: &#34;XYZ_admin_acct&#34;,
            &#34;tealium_profile&#34;: &#34;main&#34;,
            &#34;page_name&#34;: &#34;Homepage&#34;,
            &#34;page_type&#34;: &#34;main&#34;,
            &#34;tealium_event&#34;: &#34;page_view&#34;,
            &#34;user&#34;: {
                &#34;browser_lang&#34;: &#34;en-us&#34;,
                &#34;ipcinfo&#34;: &#34;en-us&#34;,
                &#34;signedin&#34;: false,
                &#34;city&#34;: &#34;san diego&#34;,
                &#34;country&#34;: &#34;us&#34;,
                &#34;country_name&#34;: &#34;united states&#34;,
                &#34;registry_city&#34;: &#34;san diego&#34;,
                &#34;registry_country_code&#34;: &#34;us&#34;,
                &#34;registry_state&#34;: &#34;ca&#34;,
                &#34;state&#34;: &#34;ca&#34;
            }
        },
        &#34;firstparty_tealium_cookies&#34;: {
             &#34;trace_id&#34;: &#34;&#34;
        }
    },
    &#34;type&#34;: &#34;LIVE&#34;,
    &#34;enrichmentOnly&#34;: false,
    &#34;event_id&#34;: &#34;example-event-id&#34;,
    &#34;visitor_id&#34;: &#34;example-visitor-id&#34;,
    &#34;post_time&#34;: 1655410928993,
    &#34;useragent&#34;: &#34;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36&#34;,
    &#34;client_ip&#34;: &#34;&#34;,
    &#34;new_visitor&#34;: false
}
```