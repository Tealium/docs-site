---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/nativescript/track/
---
### Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent,dataLayer)` to the [`track()`](https://docs.tealium.com/platforms/nativescript/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let screenView = new TealiumView('purchase', new Map([['customer_id', 'abc123', 'order_total', 10.00, 'product_id', ["PROD123", "PROD456"], 'order_id': 10]]));
Tealium.track(screenView);
```

### Track Events

To track non-view events, pass an instance of `TealiumView(tealiumEvent,dataLayer)` to the [`track()`](https://docs.tealium.com/platforms/nativescript/api/tealium/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let tealEvent = new TealiumEvent('cart_add', new Map([["customer_id": "abc123", "product_id": ["PROD123", "PROD456"], "product_price": [4.00, 6.00]]));
Tealium.track(tealEvent);
```
