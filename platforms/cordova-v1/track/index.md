---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/cordova-v1/track/
---

<blockquote>
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](https://docs.tealium.com/platforms/cordova/).
</blockquote>


## Track Views
The [`trackView()`](https://docs.tealium.com/platforms/cordova-v1/api/#trackview) method tracks every time a user opens or changes a screen in the app, as shown in the following example:

```js
tealium.trackView({tealium_event : "SCREEN_NAME", "KEY1": "VALUE1"}, "INSTANCE");
```

## Track Events

The [`trackEvent()`](https://docs.tealium.com/platforms/cordova-v1/api/#trackevent) method tracks all non-view activity, as shown in the following example:

```js
tealium.trackEvent({"tealium_event": "EVENT_NAME"}, "INSTANCE");
```
