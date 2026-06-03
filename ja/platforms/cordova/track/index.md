---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/cordova/track/
---
## 画面ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(tealiumEvent, dataLayer:)` のインスタンスを [`track()`](/ja/platforms/cordova/api/#track) メソッドに渡します。`TealiumView` はビュー名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書があります。




```js
var Dispatch = tealium.utils.Dispatch;

var screenView = Dispatch.view(
  &#39;purchase&#39;, 
  {
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;order_total&#34;: 10.00, 
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;order_id&#34;: &#34;0123456789&#34;
  }
);
tealium.track(screenView);
```




```js
let screenView = new TealiumView(
  &#34;purchase&#34;, 
  new Map&lt;string, any&gt;([
    [&#34;customer_id&#34;: &#34;abc123&#34;], 
    [&#34;order_total&#34;: 10.00],
    [&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;]], 
    [&#34;order_id&#34;: &#34;0123456789&#34;]
  ])
);
Tealium.track(screenView);
```




## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](/ja/platforms/cordova/api/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、トラッキングコールでは `tealium_event` として表示され、オプションのデータ辞書があります。




```js
var Dispatch = tealium.utils.Dispatch;

var tealEvent = Dispatch.event(
  &#39;cart_add&#39;, 
  {
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;product_price&#34;: [4.00, 6.00]
  }
);
tealium.track(tealEvent);
```




```js
let tealEvent = new TealiumEvent(
  &#34;cart_add&#34;, 
  new Map&lt;string, any&gt;([
    [&#34;customer_id&#34;: &#34;abc123&#34;], 
    [&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;]], 
    [&#34;product_price&#34;: [4.00, 6.00]]
  ])
);
Tealium.track(tealEvent);
```


