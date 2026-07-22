---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/react-native-v1/track/
---

<blockquote>
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](https://docs.tealium.com/platforms/react-native/).
</blockquote>


### Track Views

The [`trackView()`](https://docs.tealium.com/platforms/react-native-v1/api/#trackview) method tracks screen views, as shown in the following example:

```javascript
Tealium.trackView("VIEW_NAME", {"KEY": "VALUE"});
```

If multiple instances of Tealium are running, use the [`trackViewForInstanceName()`](https://docs.tealium.com/platforms/react-native-v1/api/#trackviewforinstancename) method, as shown in the following example:

```javascript
Tealium.trackViewForInstanceName("INSTANCE", "SCREEN_NAME", {"KEY": "VALUE"});
```

### Track Events

The [`trackEvent()`](https://docs.tealium.com/platforms/react-native-v1/api/#trackevent) method tracks non-view events, as shown in the following example:

```javascript
Tealium.trackEvent("EVENT_NAME", {"KEY": "VALUE"}); 
```

If multiple instances of Tealium are running, use the [`trackEventForInstanceName()`](https://docs.tealium.com/platforms/react-native-v1/api/#trackeventforinstancename) method, as shown in the following example:

```javascript
Tealium.trackEventForInstanceName("INSTANCE", "EVENT_NAME", {"KEY": "VALUE"}); 
```
