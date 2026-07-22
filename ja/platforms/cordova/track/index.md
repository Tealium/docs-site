---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/cordova/track/
---
## 画面ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(tealiumEvent, dataLayer:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/cordova/api/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書があります。




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




## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/cordova/api/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書があります。




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


