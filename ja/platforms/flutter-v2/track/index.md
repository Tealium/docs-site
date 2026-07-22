---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/track/
---
<blockquote>
これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## 画面ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView` オブジェクトを作成し、[`track()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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

## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent` オブジェクトを作成し、[`track()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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