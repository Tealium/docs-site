---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/react-native/track/
---
### Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`track()`](/platforms/react-native/api/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```js
let screenView = new TealiumView(
  &#39;purchase&#39;, 
  {
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;order_total&#34;: 10.00, 
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;order_id&#34;: &#34;0123456789&#34;
  }
);
Tealium.track(screenView);
```

### Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`track()`](/platforms/react-native/api/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

To track a non-view event, create a `TealiumEvent` object and pass it to the [`track()`](/platforms/react-native/api/#track) method:

```js
let tealEvent = new TealiumEvent(
  &#39;cart_add&#39;, 
  {
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;product_price&#34;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```
