---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/cordova/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer:)` to the [`track()`](https://docs.tealium.com/platforms/cordova/api/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.




```js
var Dispatch = tealium.utils.Dispatch;

var screenView = Dispatch.view(
  'purchase', 
  {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123456789"
  }
);
tealium.track(screenView);
```




```js
let screenView = new TealiumView(
  "purchase", 
  new Map<string, any>([
    ["customer_id": "abc123"], 
    ["order_total": 10.00],
    ["product_id": ["PROD123", "PROD456"]], 
    ["order_id": "0123456789"]
  ])
);
Tealium.track(screenView);
```




## Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent:dataLayer:)` to the [`track()`](https://docs.tealium.com/platforms/cordova/api/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.




```js
var Dispatch = tealium.utils.Dispatch;

var tealEvent = Dispatch.event(
  'cart_add', 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
);
tealium.track(tealEvent);
```




```js
let tealEvent = new TealiumEvent(
  "cart_add", 
  new Map<string, any>([
    ["customer_id": "abc123"], 
    ["product_id": ["PROD123", "PROD456"]], 
    ["product_price": [4.00, 6.00]]
  ])
);
Tealium.track(tealEvent);
```


