---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/react-native/track/
---
### Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`track()`](https://docs.tealium.com/platforms/react-native/api/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```js
let screenView = new TealiumView(
  'purchase', 
  {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123456789"
  }
);
Tealium.track(screenView);
```

### Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`track()`](https://docs.tealium.com/platforms/react-native/api/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

To track a non-view event, create a `TealiumEvent` object and pass it to the [`track()`](https://docs.tealium.com/platforms/react-native/api/#track) method:

```js
let tealEvent = new TealiumEvent(
  'cart_add', 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```
