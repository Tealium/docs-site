---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/roku/track/
---
## Track Events

The [`TrackEvent()`](/platforms/roku/api/#trackevent) method tracks events, as shown in the following example:

```javascript
data = CreateObject(&#34;roAssociativeArray&#34;)
data.someKey = &#34;KEY_VALUE&#34;
teal.TrackEvent(&#34;EVENT_NAME&#34;, data)
```