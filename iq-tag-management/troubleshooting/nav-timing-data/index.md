---
title: Navigation timing data
description: This article explains how to enable navigation timing data, which you can use to measure the performance of a website.
url: https://docs.tealium.com/iq-tag-management/troubleshooting/nav-timing-data/
---
The [Navigation Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API &#34;Navigation Timing API&#34;) provides data that can be used to measure the performance of a website. Unlike other JavaScript-based mechanisms that have been used for the same purpose, this API can provide end-to-end latency data that can be more useful and accurate.

## Enable navigation timing data

1. Update your Tealium Collect template to the latest version of the template.
1. Set the sampling rate for the percentage of traffic you&#39;d like to gather information.
    The sampling rate is exclusive to the event data being collected, meaning if sampling is set to 5% Tealium will still trigger 100% of event data to AudienceStream, EventStore, and/or EventDB (Tealium Collect).
1. Save/Publish the update.

## The data

The following data points are captured within the Tealium Collect tag:

* `timing.domain` = The domain where the timing data was collected
* `timing.pathname` = The path name (web page) where the timing data was collected
* `timing.query_string` = The query string value in URL where the timing data was collected
* `timing.timestamp` = The date and time when the timing data was collected (epoch time of client&#39;s web browser)
* `timing.dns` = `t.domainLookupEnd` - `t.domainLookupStart`
* `timing.connect` = `t.connectEnd` - `t.connectStart`
* `timing.response` = `t.responseEnd` - `t.responseStart`
* `timing.dom_loading_to_interactive` = `t.domInteractive` - `t.domLoading`
* `timing.dom_interactive_to_complete` = `t.domComplete` - `t.domInteractive`
* `timing.load` = `t.loadEventEnd` - `t.loadEventStart`
* `timing.time_to_first_byte` = `t.responseStart` - `t.connectEnd`
* `timing.front_end` = `t.loadEventStart` - `t.responseEnd`
* `timing.fetch_to_response` = `t.responseStart` - `t.fetchStart`
* `timing.fetch_to_complete` = `t.domComplete` - `t.fetchStart`
* `timing.fetch_to_interactive` = `t.domInteractive` - `t.fetchStart`

This data is stored in local storage in key `tealium_timing`.

On the next page load, local storage is read and the data is added to the Data Layer.

We can’t send the Navigation TIming data on the same page event call because we don’t have all the data. For example, we don’t have timing data for the load event because most likely we’ve fired the Collect tag on the `interactive` event. This means we would have to trigger another call, effectively doubling, which effects the number of events set in the contract. Therefore, we send on the next page view to prevent a negative effect to the event count of the contract.

## EventDB requirements

To declare the data sources in EventDB, perform the following steps:

1. Navigate to **iQ Tag Management &gt; Data Layer**.
1. Click the **Add Data Source** drop-down menu and select **Bulk Import Data Sources from CSV**
1. Paste the following into the interface:

```
&#34;timing.domain&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;www.tealiumecommerce.com&#34;
&#34;timing.pathname&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;/&#34;
&#34;timing.query\_string&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;&#34;
&#34;timing.timestamp&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1459274326166
&#34;timing.dns&#34;,&#34;UDO Variable&#34;,&#34;&#34;,75
&#34;timing.connect&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1
&#34;timing.response&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1
&#34;timing.dom\_loading\_to\_interactive&#34;,&#34;UDO Variable&#34;,&#34;&#34;,3987
&#34;timing.dom\_interactive\_to\_complete&#34;,&#34;UDO Variable&#34;,&#34;&#34;,3570
&#34;timing.load&#34;,&#34;UDO Variable&#34;,&#34;&#34;,2
&#34;timing.time\_to\_first\_byte&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1002
&#34;timing.front\_end&#34;,&#34;UDO Variable&#34;,&#34;&#34;,7570
&#34;timing.fetch\_to\_response&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1082
&#34;timing.fetch\_to\_complete&#34;,&#34;UDO Variable&#34;,&#34;&#34;,8653
&#34;timing.fetch\_to\_interactive&#34;,&#34;UDO Variable&#34;,&#34;&#34;,5083
```

This will declare the data sources so visualization tools have access to the data. This step is not needed for EventStore.

Here is a sample report where you can see how long pages are taking to load. For example, if you have requirements that pages must load in under 3 seconds (3000 milliseconds) then you know the &#34;Chelsa Tee&#34; and &#34;Tealium Ecommerce Demo&#34; pages need improvement.

![](/images/iq-tag-management/page-performance-visualization.png)