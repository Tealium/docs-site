---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/react-native-v1/track/
---
これはTealiumのReact Native用の以前のバージョン（1.x）です。  
現在のバージョンは[Tealium for React Native 2.x](/ja/platforms/react-native/)を参照してください。

### ビューのトラッキング

以下の例に示すように、[`trackView()`](/ja/platforms/react-native-v1/api/#trackview)メソッドは画面ビューを追跡します：

```javascript
Tealium.trackView(&#34;VIEW_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;});
```

複数のTealiumインスタンスが動作している場合は、以下の例に示すように[`trackViewForInstanceName()`](/ja/platforms/react-native-v1/api/#trackviewforinstancename)メソッドを使用します：

```javascript
Tealium.trackViewForInstanceName(&#34;INSTANCE&#34;, &#34;SCREEN_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;});
```

### イベントのトラッキング

以下の例に示すように、[`trackEvent()`](/ja/platforms/react-native-v1/api/#trackevent)メソッドはビュー以外のイベントを追跡します：

```javascript
Tealium.trackEvent(&#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```

複数のTealiumインスタンスが動作している場合は、以下の例に示すように[`trackEventForInstanceName()`](/ja/platforms/react-native-v1/api/#trackeventforinstancename)メソッドを使用します：

```javascript
Tealium.trackEventForInstanceName(&#34;INSTANCE&#34;, &#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```