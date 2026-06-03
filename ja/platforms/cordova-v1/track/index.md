---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/track/
---
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](/ja/platforms/cordova/)をご覧ください。

## 画面のトラッキング
次の例に示すように、[`trackView()`](/ja/platforms/cordova-v1/api/#trackview) メソッドは、ユーザーがアプリ内で画面を開いたり変更したりするたびに追跡します：

```js
tealium.trackView({tealium_event : &#34;SCREEN_NAME&#34;, &#34;KEY1&#34;: &#34;VALUE1&#34;}, &#34;INSTANCE&#34;);
```

## イベントのトラッキング

次の例に示すように、[`trackEvent()`](/ja/platforms/cordova-v1/api/#trackevent) メソッドは、画面表示以外のすべての活動を追跡します：

```js
tealium.trackEvent({&#34;tealium_event&#34;: &#34;EVENT_NAME&#34;}, &#34;INSTANCE&#34;);
```