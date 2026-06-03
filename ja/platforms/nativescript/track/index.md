---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/nativescript/track/
---
### ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(tealiumEvent,dataLayer)` のインスタンスを [`track()`](/ja/platforms/nativescript/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書もあります。

```javascript
let screenView = new TealiumView(&#39;purchase&#39;, new Map([[&#39;customer_id&#39;, &#39;abc123&#39;, &#39;order_total&#39;, 10.00, &#39;product_id&#39;, [&#34;PROD123&#34;, &#34;PROD456&#34;], &#39;order_id&#39;: 10]]));
Tealium.track(screenView);
```

### イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumView(tealiumEvent,dataLayer)` のインスタンスを [`track()`](/ja/platforms/nativescript/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書もあります。

```javascript
let tealEvent = new TealiumEvent(&#39;cart_add&#39;, new Map([[&#34;customer_id&#34;: &#34;abc123&#34;, &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], &#34;product_price&#34;: [4.00, 6.00]]));
Tealium.track(tealEvent);
```