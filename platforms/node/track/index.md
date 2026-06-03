---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/node/track/
---
## Track Events / Views

The [`track()`](/platforms/node/api/#track) method tracks all events and page views, as shown in the following example:


```javascript
tealium.track(&#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```

## Track Visitors

If your application tracks user activity and you want to associate events with a visitor, include the `tealium_visitor_id` attribute in the data object as shown in the following example:

```javascript
var myVisitorId = myVisitorIdFunction();

tealium.track(&#34;page_view&#34;, {
    &#34;tealium_visitor_id&#34; : myVisitorId,
    &#34;some_key&#34;           : &#34;KEY&#34;
});
```

This event attribute uniquely identifies the current user, either anonymously or with a personal identifier such as an email address.
