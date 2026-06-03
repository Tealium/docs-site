---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/track/
---これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](/ja/platforms/flutter/)をご覧ください。

## 画面ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView` オブジェクトを作成し、[`track()`](/ja/platforms/flutter-v2/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

```dart
final screenView = TealiumView(
  &#39;purchase&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;order_total&#39;: 10.00, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;order_id&#39;: &#34;0123456789&#34;
  }
);
Tealium.track(screenView);
```

## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent` オブジェクトを作成し、[`track()`](/ja/platforms/flutter-v2/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```