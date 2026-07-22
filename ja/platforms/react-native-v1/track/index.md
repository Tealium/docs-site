---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/react-native-v1/track/
---

<blockquote>
これはTealiumのReact Native用の以前のバージョン（1.x）です。  
現在のバージョンは[Tealium for React Native 2.x](https://docs.tealium.com/ja/platforms/react-native/)を参照してください。
</blockquote>


### ビューのトラッキング

以下の例に示すように、[`trackView()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#trackview)メソッドは画面ビューを追跡します：

```javascript
Tealium.trackView("VIEW_NAME", {"KEY": "VALUE"});
```

複数のTealiumインスタンスが動作している場合は、以下の例に示すように[`trackViewForInstanceName()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#trackviewforinstancename)メソッドを使用します：

```javascript
Tealium.trackViewForInstanceName("INSTANCE", "SCREEN_NAME", {"KEY": "VALUE"});
```

### イベントのトラッキング

以下の例に示すように、[`trackEvent()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#trackevent)メソッドはビュー以外のイベントを追跡します：

```javascript
Tealium.trackEvent("EVENT_NAME", {"KEY": "VALUE"}); 
```

複数のTealiumインスタンスが動作している場合は、以下の例に示すように[`trackEventForInstanceName()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#trackeventforinstancename)メソッドを使用します：

```javascript
Tealium.trackEventForInstanceName("INSTANCE", "EVENT_NAME", {"KEY": "VALUE"}); 
```