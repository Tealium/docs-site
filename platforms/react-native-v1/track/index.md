---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/react-native-v1/track/
---
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](/platforms/react-native/).

### Track Views

The [`trackView()`](/platforms/react-native-v1/api/#trackview) method tracks screen views, as shown in the following example:

```javascript
Tealium.trackView(&#34;VIEW_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;});
```

If multiple instances of Tealium are running, use the [`trackViewForInstanceName()`](/platforms/react-native-v1/api/#trackviewforinstancename) method, as shown in the following example:

```javascript
Tealium.trackViewForInstanceName(&#34;INSTANCE&#34;, &#34;SCREEN_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;});
```

### Track Events

The [`trackEvent()`](/platforms/react-native-v1/api/#trackevent) method tracks non-view events, as shown in the following example:

```javascript
Tealium.trackEvent(&#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```

If multiple instances of Tealium are running, use the [`trackEventForInstanceName()`](/platforms/react-native-v1/api/#trackeventforinstancename) method, as shown in the following example:

```javascript
Tealium.trackEventForInstanceName(&#34;INSTANCE&#34;, &#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```
