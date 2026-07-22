---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/track/
---

<blockquote>
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](https://docs.tealium.com/ja/platforms/cordova/)をご覧ください。
</blockquote>


## 画面のトラッキング
次の例に示すように、[`trackView()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#trackview) メソッドは、ユーザーがアプリ内で画面を開いたり変更したりするたびに追跡します：

```js
tealium.trackView({tealium_event : "SCREEN_NAME", "KEY1": "VALUE1"}, "INSTANCE");
```

## イベントのトラッキング

次の例に示すように、[`trackEvent()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#trackevent) メソッドは、画面表示以外のすべての活動を追跡します：

```js
tealium.trackEvent({"tealium_event": "EVENT_NAME"}, "INSTANCE");
```