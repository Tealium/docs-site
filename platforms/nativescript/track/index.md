---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/nativescript/track/
---
### Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent,dataLayer)` to the [`track()`](/platforms/nativescript/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let screenView = new TealiumView(&#39;purchase&#39;, new Map([[&#39;customer_id&#39;, &#39;abc123&#39;, &#39;order_total&#39;, 10.00, &#39;product_id&#39;, [&#34;PROD123&#34;, &#34;PROD456&#34;], &#39;order_id&#39;: 10]]));
Tealium.track(screenView);
```

### Track Events

To track non-view events, pass an instance of `TealiumView(tealiumEvent,dataLayer)` to the [`track()`](/platforms/nativescript/api/tealium/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let tealEvent = new TealiumEvent(&#39;cart_add&#39;, new Map([[&#34;customer_id&#34;: &#34;abc123&#34;, &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], &#34;product_price&#34;: [4.00, 6.00]]));
Tealium.track(tealEvent);
```
