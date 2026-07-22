---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView` オブジェクトを作成し、[`track()`](https://docs.tealium.com/ja/platforms/flutter/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent` オブジェクトを作成し、[`track()`](https://docs.tealium.com/ja/platforms/flutter/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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