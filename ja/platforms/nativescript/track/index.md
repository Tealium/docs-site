---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/nativescript/track/
---
### ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(tealiumEvent,dataLayer)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書もあります。

```javascript
let screenView = new TealiumView('purchase', new Map([['customer_id', 'abc123', 'order_total', 10.00, 'product_id', ["PROD123", "PROD456"], 'order_id': 10]]));
Tealium.track(screenView);
```

### イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumView(tealiumEvent,dataLayer)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書もあります。

```javascript
let tealEvent = new TealiumEvent('cart_add', new Map([["customer_id": "abc123", "product_id": ["PROD123", "PROD456"], "product_price": [4.00, 6.00]]));
Tealium.track(tealEvent);
```