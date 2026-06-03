---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/android-java/track/
---
## Track Views

The [`trackView()`](/platforms/android-java/api/tealium/#trackview) method tracks screen views, as shown in the following example:

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE_NAME&#34;).trackView(&#34;EVENT_NAME&#34;, data);
```

The value passed as the first parameter will appear in the data layer as the variable `tealium_event`.

## Track Events

The [`trackEvent()`](/platforms/android-java/api/tealium/#trackevent) method tracks non-view events, as shown in the following example:

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE_NAME&#34;).trackEvent(&#34;EVENT_NAME&#34;, data);
```
