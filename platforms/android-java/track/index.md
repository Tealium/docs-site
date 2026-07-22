---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/android-java/track/
---
## Track Views

The [`trackView()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackview) method tracks screen views, as shown in the following example:

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE_NAME").trackView("EVENT_NAME", data);
```


<blockquote>
The value passed as the first parameter will appear in the data layer as the variable `tealium_event`.
</blockquote>


## Track Events

The [`trackEvent()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackevent) method tracks non-view events, as shown in the following example:

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE_NAME").trackEvent("EVENT_NAME", data);
```
