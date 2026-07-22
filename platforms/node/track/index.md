---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/node/track/
---
## Track Events / Views

The [`track()`](https://docs.tealium.com/platforms/node/api/#track) method tracks all events and page views, as shown in the following example:


```javascript
tealium.track("EVENT_NAME", {"KEY": "VALUE"}); 
```

## Track Visitors

If your application tracks user activity and you want to associate events with a visitor, include the `tealium_visitor_id` attribute in the data object as shown in the following example:

```javascript
var myVisitorId = myVisitorIdFunction();

tealium.track("page_view", {
    "tealium_visitor_id" : myVisitorId,
    "some_key"           : "KEY"
});
```

This event attribute uniquely identifies the current user, either anonymously or with a personal identifier such as an email address.
