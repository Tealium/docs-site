---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView` オブジェクトを作成し、[`track()`](/ja/platforms/flutter/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent` オブジェクトを作成し、[`track()`](/ja/platforms/flutter/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、イベントデータのオプショナルオブジェクトがあります。

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