---
title: SiteCatalyst Firing multiple events and Event Serialization
description: The following describes the changes available in the SiteCatalyst templates released on Sept 2, 2015. The Tag names are "SiteCatalyst" and "SiteCatalyst AppMeasurement for JS."
url: https://docs.tealium.com/client-side-tags/sitecatalyst-firing-multiple-events-and-event-serialization/
---

## How do I know that I have the latest template that has this feature?

At the top of the template is a date (timestamp) that begins with the template ID and the date in format `YYYYMMDD`. This feature is added in `20150827` template.

```
//~~tv:19004.h27.20150827
```

This timestamp is the tag template update date (which will be earlier than the date this template is made available in production).&lt;br&gt;&lt;br&gt;
You would also expect this feature in a later template (for example, `20150929`) 

## Event Serialization

If I have `myevent` in my data layer and this is mapped to `click:event5` in mapping toolbox then the following would trigger `event5` with the serialization number `12345`.

`utag.view( \{ myevent : &#34;click:12345&#34; \} );`

## Firing Multiple Events

The updated template allows for two or more events by adding another mapping and using a comma-separated list of strings in the data layer. In the example below, we have &#34;product-view:prodView&#34; in mapping and also add a &#34;product-view&#34; string in the list of values in our data layer variable &#34;myevent&#34;.

`utag.view( \{ myevent : &#34;product-view,click:12345&#34; \} );`

Because Javascript is nice enough to convert arrays to strings, and add a comma in the process, the following array works the same as a comma-separated list in a string:

`utag.view( \{ myevent : [&#34;product-view&#34;, &#34;click:12345&#34;] \} );`

### Notes

* If you expect spaces in your mapped variable then use an Extension to clean up the values, the template will not do any variable value manipulation (for instance, no string clean up).

* If there is a list of values and multiple matches in mapping, the event will only fire once (for instance, only added once to `s.events`).

* In the blog link below, it appears Adobe has another way of doing event serialization server-side. This feature appears to no longer be needed in the implementation and can be done with reporting configuration in Adobe&#39;s UI.
 
## Vendor Information

This timestamp is the tag template update date (which will be earlier than the date this template is made available in production).&lt;br&gt;&lt;br&gt;
You would also expect this feature in a later template (for example, `20150929`)

* [Event Serialization inside Omniture Sitecatalyst](https://blogs.adobe.com/digitalmarketing/analytics/event-serialization-inside-omniture-sitecatalyst/)
* [Event Serialization](https://helpx.adobe.com/analytics/using/event-serialization.html)
* [Say hello to On-Demand Metrics in Adobe Analytics](http://blogs.adobe.com/digitalmarketing/analytics/say-hello-to-on-demand-metrics-in-adobe-analytics/)
