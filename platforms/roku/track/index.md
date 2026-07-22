---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/roku/track/
---
## Track Events

The [`TrackEvent()`](https://docs.tealium.com/platforms/roku/api/#trackevent) method tracks events, as shown in the following example:

```javascript
data = CreateObject("roAssociativeArray")
data.someKey = "KEY_VALUE"
teal.TrackEvent("EVENT_NAME", data)
```