---
title: EventStore data guide
description: This article provides a summary of event-level data points made available through EventStore.
url: https://docs.tealium.com/server-side/data-storage/audiencestore-eventstore/eventstore-data-guide/
---
EventStore provides the most efficient way for collecting and exporting event-level data from your site.

## How it works

1. The [Tealium Collect]() tag captures the [live event feed]() on your site and feeds the events to EventStore, which lets you view and download the underlying data.
1. The captured data is then compressed into a flattened JSON file and made available for download from Tealium’s Amazon S3 bucket. Each JSON object in the file may contain one or more rows of name-value pairs associated with the event.  
      If you send your event data (event feeds), to another location, such as your S3 bucket or server, the feeds are not displayed in EventStore.
1. After the S3 bucket reaches a size of 100 MB (uncompressed) or after 1 hour has elapsed, whichever comes first, the data is compressed and prepared for Redshift.
1. The compressed data is then copied and imported into the Redshift database for your account.

## Tealium Collect tag data

The Tealium Collect tag sends several predefined variables and data from the page, as described in the following sections.

Ignore legacy values prefixed by `_t` in your data log files.

### Default variables

| Variable | Description |
|---| ---|
|`visitorid`| The unique ID of the visitor.|
|`eventid`| An alphanumeric identifier unique to the event.|
|`eventtime`| The UNIX/epoch timestamp of the event, based on UTC time zone.|
|`useragent`| The user-agent header.|

### DOM variables

| Variable | Description |
|---| ---|
|`dom_domain`| Domain of the site.|
|`dom_pathname`| Pathname of the URL.|
|`dom_query_string`| Querystring portion of the URL following the question mark (`?`) character.|
|`dom_url`| The entire URL of the HTML document.|
|`dom_title`| Title of the HTML document.|
|`dom_viewport_width`| Device screen width.|
|`dom_viewport_height`| Device screen height.|

### Page URL variables

| Variable | Description |
|---| ---|
|`pageurl_scheme`| The Uniform Resource Identifier (URI) protocol, such as `http` or `https`.|
|`pageurl_domain`| Domain of the site.|
|`pageurl_path`| Pathname of the URL.|
|`pageurl_querystring`| Querystring portion of the URL following the question mark (`?`) character.|
|`pageurl_query_params_key`| For each querystring parameter, there is a data point that contains the parameter key and value.|
|`pageurl_full_url`| The URL of the HTML document without querystring parameters.|

### Referrer URL variables

| Variable | Description |
|---| ---|
|`referrerurl_scheme`| The URI protocol of referring URL, such as `http` or `https`.|
|`referrerurl_domain`| Domain of the referring URL site.|
|`referrerurl_path`| Pathname of the referring URL.|
|`referrerurl_querystring`| Querystring portion of the referring URL following the &#34;?&#34; character.|
|`referrerurl_query_params_key`| For each querystring parameter, there is a data point that contains the parameter key and value.|
|`referrerurl_full_url`| The entire URL of the referring page.|

### Tags executed

| Variable | Description |
|---| ---|
|`tags_profile_tag-uid_executed`|  &lt;ul&gt;&lt;li&gt;The profile and tag that successfully executed.&lt;/li&gt;&lt;li&gt;Each successful tag trigger includes its own entry.&lt;/li&gt;&lt;/ul&gt; |

### Environment detail variables

| Variable | Description |
|---| ---|
|`ut.account`| Tealium iQ account.|
|`ut.profile`| Tealium iQ profile.|
|`ut.env`| The publish environment associated with the `utag.js` file.|

### Tealium built-in variables

A full list of Tealium built-in variables is provided in the [Built-In Data Layer Variables](https://docs.tealium.com/platforms/javascript/built-in-variables/) article.

| Variable | Description |
|---| ---|
|`ut.event`|  The name of the event being tracked, such as a view or link. |
|`ut.version`|  The `utag.js` version number, followed by the publish timestamp. |
|`ut.domain`|  The top-level domain of the currently loaded web page. |
|`tealium_session_number`|  A duplicate of the existing value in `cp.utag_main__sn`. |
|`tealium_session_event_number`|  A new cookie value in `cp.utag_main__se` that counts the number of utag.link/view/track calls in the current session (visit) Useful for Single Page Apps (SPAs) where there is always &#39;one page&#39; and many events on that page |

### First-party Tealium cookies

| Variable | Description |
|---| ---|
|`_ses_id`|  A unique identifier for the session. Requires `utag.js` version 4.27 and later. |
|`_st`|  The time at which the visitor session expires if the visitor does nothing more. This is the visitor&#39;s current time, plus the session timeout time. This timeout period is normally 30 minutes (1800000 milliseconds) unless configured otherwise. The value of `utag.cfg.session_timeout`, which can be overridden by changing this variable using a [JavaScript Extension](). Requires `utag.js` version 4.26 and later. |
|`_v_id`|  The ID value unique to the visitor to ensure compliance with data privacy and consent rules. Requires `utag.js` version 4.26 and later. For more information, see [`utag.js` version 4.50](). |
|`_se`| The number of events during the current session. |
|`_ss`|  A flag value indicating the start of session. Values are `0` or `1`. Requires `utag.js` version 4.26 and later. |
|`_pn`|  The page number value. Starts over at `1` with each new session and increments each time `utag.js` loads. Requires `utag.js` version 4.28 and later. |
|`_sn`|  The session count. Requires `utag.js` version 4.28 and later. |
|`_dc_group`|  A random number to use with the **Sample Size** setting in the Tealium Collect tag to determine which events are sampled. |
|`_dc_visit`|  The number of sessions for which the Collect tag has fired. Starts at `1` for the first visit. |
|`_dc_event`|  The number of events for which the Collect tag has fired. Starts at `1` for the first page view of a visit. |
|`_dc_region`|  The AudienceStream region where the visit session is stored, collected from the HTTP response header. This cookie is used for determining the endpoints for [data layer enrichment](). |

### Additional variables

The tag collects a variety of other data from the page, including:

* Data points defined in your data layer. The maximum character length for any one value is 255 characters.
* Webpage elements, such as metadata, cookie parameters, and JavaScript page variables.
* Performance timing metrics for gathering Real User Monitoring (RUM) data. This data can be used to understand a user&#39;s experience. For example, the browser time to DOM interactive state for pages on your site.  

| Performance timing variable | Description |
|---| ---|
|`timing.domain`| The domain where the timing data was collected.|
|`timing.pathname`| The path name (web page) where the timing data was collected.|
|`timing.query_string`| The query string value in URL where the timing data was collected.|
|`timing.timestamp`| The date/time when the timing data was collected (epoch time of client&#39;s web browser).|
|`timing.dns`| `t.domainLookupStart`|
|`timing.connect`| `t.connectStart`|
|`timing.response`| `t.responseStart`|
|`timing.dom_loading_to_interactive`| `t.domInteractive` minus `t.domLoading`|
|`timing.dom_interactive_to_complete`| `t.domComplete` minus `t.domInteractive`|
|`timing.load`| `t.loadEventEnd` minus `t.loadEventStart`|
|`timing.time_to_first_byte`| `t.responseStart` minus `t.connectEnd`|
|`timing.front_end`| `t.loadEventStart` minus `t.responseEnd`|
|`timing.fetch_to_response`| `t.responseStart` minus `t.fetchStart`|
|`timing.fetch_to_complete`| `t.domComplete` minus `t.fetchStart`|
|`timing.fetch_to_interactive`| `t.domInteractive` minus `t.fetchStart `|
  
If the value of a data point equals zero, no timing information was captured. You can ignore the zero values when reporting or averaging.

## Calculate visitor timezone

The timezone for a visitor is not sent in the EventStore data. You can calculate the timezone by viewing the difference between `EventTime` and `_ses_id` on the record where `_ss` is `1`, since that record is the start of the session.

If `utag.cfg.session_timeout` is known, you can calculate the current local time for the user by subtracting `utag.cfg.session_timeout` from `_st`, and then calculating the timezone by looking at the difference between the current time and `EventTime`. This approach can be used for any record.

## Versions of utag.js

For detailed information about individual utag versions, see the [utag.js Release Notes]().

## Sample JSON object

```json
{
    &#34;visitorid&#34;: &#34;014fb34a718e001ad754191d58ff1c074003a06c00c48&#34;,
    &#34;eventid&#34;: &#34;65f61a4b-54ca-4adf-b757-657e1711f6e7&#34;,
    &#34;eventtime&#34;: 1441822083000,
    &#34;useragent&#34;: &#34;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5) AppleWebKit/600.8.9 (KHTML, like Gecko) Version/8.0.8 Safari/600.8.9&#34;,
    &#34;dom_domain&#34;: &#34;tealium.com&#34;,
    &#34;dom_pathname&#34;: &#34;/products/audiencestream/&#34;,
    &#34;dom_query_string&#34;: &#34;&#34;,
    &#34;dom_url&#34;: &#34;http://tealium.com/products/audiencestream/&#34;,
    &#34;dom_title&#34;: &#34;AudienceStream | Real-time Data Action Engine | Tealium&#34;,
    &#34;dom_viewport_width&#34;: &#34;1670&#34;,
    &#34;dom_viewport_height&#34;: &#34;1059&#34;,
    &#34;pageurl_scheme&#34;: &#34;http&#34;,
    &#34;pageurl_domain&#34;: &#34;tealium.com&#34;,
    &#34;pageurl_path&#34;: &#34;/products/audiencestream/&#34;,
    &#34;pageurl_querystring&#34;: &#34;&#34;,
    &#34;pageurl_full_url&#34;: &#34;http://tealium.com/products/audiencestream/&#34;,
    &#34;referrerurl_scheme&#34;: &#34;https&#34;,
    &#34;referrerurl_domain&#34;: &#34;google.com&#34;,
    &#34;referrerurl_path&#34;: &#34;&#34;,
    &#34;referrerurl_querystring&#34;: &#34;&#34;,
    &#34;referrerurl_full_url&#34;: &#34;https://www.google.com/&#34;,
    &#34;tags_tiq_as_3_executed&#34;: true,
    &#34;tags_tiq_as_1_executed&#34;: true,
    &#34;udo_ut_account&#34;: &#34;tealium&#34;,
    &#34;udo_ut_profile&#34;: &#34;main&#34;,
    &#34;udo_ut_env&#34;: &#34;prod&#34;,
    &#34;udo_ut_event&#34;: &#34;view&#34;,
    &#34;udo_ut_version&#34;: &#34;ut4.39.201509091709&#34;,
    &#34;udo_ut_domain&#34;: &#34;tealium.com&#34;,
    &#34;firstpartycookies_utag_main_ses_id&#34;: &#34;1441822044558&#34;,
    &#34;firstpartycookies_utag_main__st&#34;: &#34;1441823881730&#34;,
    &#34;firstpartycookies_utag_main_v_id&#34;: &#34;014fb34a718e001ad754191d58ff1c074003a06c00c48&#34;,
    &#34;firstpartycookies_utag_main__ss&#34;: &#34;0&#34;,
    &#34;firstpartycookies_utag_main__pn&#34;: &#34;2&#34;,
    &#34;firstpartycookies_utag_main__sn&#34;: &#34;1&#34;,
    &#34;firstpartycookies_utag_main_dc_visit&#34;: &#34;1&#34;,
    &#34;firstpartycookies_utag_main_dc_event&#34;: &#34;2&#34;,
    &#34;firstpartycookies_utag_main_dc_region&#34;: &#34;us-west-1&#34;,
    &#34;firstpartycookies__gat&#34;: &#34;1&#34;,
    &#34;firstpartycookies__ga&#34;: &#34;GA1.2.2095105468.1441822080&#34;,
    &#34;js_page.is_mobile&#34;: &#34;false&#34;,
    &#34;js_page.is_tablet&#34;: &#34;false&#34;,
    &#34;device_type&#34;: &#34;desktop&#34;,
    &#34;udo_page_name&#34;: &#34;AudienceStream | Real-time Data Action Engine | Tealium&#34;,
    &#34;udo_site_name&#34;: &#34;Tealium&#34;,
    &#34;udo_site_description&#34;: &#34;Tag Management and Audience Segmentation&#34;,
    &#34;udo_page_type&#34;: &#34;page&#34;,
    &#34;udo_post_author&#34;: &#34;tealium&#34;,
    &#34;udo_post_date&#34;: &#34;2014/11/26&#34;,
}
```

## Performance timing metrics

For additional information about performance timing metrics, see the following:

* [A Practical Guide to Navigation Timing](http://calendar.perfplanet.com/2011/a-practical-guide-to-the-navigation-timing-api/)
* [Web APIs &gt; Navigation Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API)