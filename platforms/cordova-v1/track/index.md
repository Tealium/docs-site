---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/cordova-v1/track/
---
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](/platforms/cordova/).

## Track Views
The [`trackView()`](/platforms/cordova-v1/api/#trackview) method tracks every time a user opens or changes a screen in the app, as shown in the following example:

```js
tealium.trackView({tealium_event : &#34;SCREEN_NAME&#34;, &#34;KEY1&#34;: &#34;VALUE1&#34;}, &#34;INSTANCE&#34;);
```

## Track Events

The [`trackEvent()`](/platforms/cordova-v1/api/#trackevent) method tracks all non-view activity, as shown in the following example:

```js
tealium.trackEvent({&#34;tealium_event&#34;: &#34;EVENT_NAME&#34;}, &#34;INSTANCE&#34;);
```
