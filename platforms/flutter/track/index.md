---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/flutter/track/
---
## Track views

To track a screen view, create a `TealiumView` object and pass it to the [`track()`](https://docs.tealium.com/platforms/flutter/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional object of event data.

```dart
final screenView = TealiumView(
  'purchase', 
  {
    'customer_id': 'abc123', 
    'order_total': 10.00, 
    'product_id': ["PROD123", "PROD456"], 
    'order_id': "0123456789"
  }
);
Tealium.track(screenView);
```

## Track events

To track a non-view event, create a `TealiumEvent` object and pass it to the [`track()`](https://docs.tealium.com/platforms/flutter/api/tealium/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional object of event data.

```dart
final tealEvent = TealiumEvent(
  'cart_add', 
  {
    'customer_id': 'abc123', 
    'product_id': ["PROD123", "PROD456"], 
    'product_price': [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```
