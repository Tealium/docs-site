---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/flutter/track/
---
## Track views

To track a screen view, create a `TealiumView` object and pass it to the [`track()`](/platforms/flutter/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional object of event data.

```dart
final screenView = TealiumView(
  &#39;purchase&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;order_total&#39;: 10.00, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;order_id&#39;: &#34;0123456789&#34;
  }
);
Tealium.track(screenView);
```

## Track events

To track a non-view event, create a `TealiumEvent` object and pass it to the [`track()`](/platforms/flutter/api/tealium/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional object of event data.

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```
