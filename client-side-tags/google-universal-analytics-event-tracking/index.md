---
title: Google Universal Analytics Event Tracking
description: This guides shows two methods for tracking custom events in the Google Universal Analytics tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-event-tracking/
---
 As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](). 

## Overview

There are two main methods for configuring custom events for Google Universal Analytics (GUA) in your iQ Tag Management account. The first method uses data mapping to set each event attribute individually. This is the most common approach and cover the majority of scenarios. The second method uses JavaScript and is more advanced, but lets you trigger multiple events at once.

* Single Events Using Data Mapping
* Multiple Events Using &#34;GA Events&#34; Array

## Tracking events with data mapping

This method uses data mapping to map your data layer variables to the required GUA event variables (learn more about [event fields expected by Google Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)). It requires creating variables for each of the GUA event fields:

* eventCategory
* eventAction
* eventLabel
* eventValue

Because these variables will be specific to GUA we recommend that you prefix the names with &#34;ga\_&#34; to easily distinguish them from your other event variables. You will then use a Set Data Values extension to set the GUA event variables to the expected values for each event.

Follow these steps to configure GUA event tracking using data mapping:

1. **Create Event Variables**  
Create a variable for each of the GUA event fields. (Learn more about [adding data layer variables]().)
  * ga\_eventaction
  * ga\_eventCategory
  * ga\_eventLabel
  * ga\_eventValue
1. **Add Data Mappings**  
Add a data mapping for each variable to the corresponding GUA field. ([Learn more about data mappings](/iq-tag-management/data-mappings/manage/).)
1. **Add a Set Data Values Extension**  
For each event to be tracked in GUA, you will add a [Set Data Values extension]() to set the GUA event variables to the expected values and uses a condition that identifies the event.  
These extensions only set GUA variables, so scope them to the GUA tag.
 In this example, the condition identifies when the `video_play` event occurs on the `Fall Promo` video.  


Save and publish to test your changes.

## Tracking events with GA events array

This method uses a special array variable from the GUA tag template called `ga_events` that lets you trigger multiple events in one call or bypass mapping. This method uses just one mapping for `ga_events` then relies on JavaScript code to push GUA event objects. This method is convenient if your implementation tracks a lot of custom events in GUA because it lets you set the GUA variables and events directly rather than configuring them as extensions and mappings.

This method is only supported in Google Universal Analytics.

Follow these steps to use the `ga_events` array for GUA event tracking:

1. Create a new data layer variable named `ga_events_array`.
1. In the GUA tag, add a data mapping from to `ga_events_array` to `ga_events`.
1. Use the following code in a [Javascript Code]() extension as a template to set the `ga_events_array` variable. Set the scope to All Tags or your GUA tag.: 

```js
b.ga_events_array = [
  {eventCategory:&#34;cat1&#34;, eventAction:&#34;action1&#34;, eventLabel:&#34;label1&#34;, eventValue:&#34;1&#34;},
  {eventCategory:&#34;cat2&#34;, eventAction:&#34;action2&#34;, eventLabel:&#34;label2&#34;, eventValue:&#34;2&#34;}
]
```

## Converting GUA Tracking to Tealium Tracking

This method also makes it simple to convert existing GUA event tracking to Tealium tracking.

Example GUA code snippet for event tracking:

```js
ga(&#39;send&#39;, {
    hitType       : &#39;event&#39;,
    eventCategory : &#39;Videos&#39;,
    eventAction   : &#39;play&#39;,
    eventLabel    : &#39;Fall Campaign&#39;
});
```

You can maintain the basic naming convention and convert this to Tealium tracking by setting the `ga_events` variable with the GUA event fields:

```js
utag.link({
    ga_events : [{
        eventCategory : &#39;Videos&#39;,
        eventAction   : &#39;play&#39;,
        eventLabel    : &#39;Fall Campaign&#39;
    }]
});
```

This approach bypasses the need for a mapping by setting the GUA tag template variable directly.
