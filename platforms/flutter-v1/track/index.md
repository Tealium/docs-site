---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/flutter-v1/track/
---
<blockquote>
This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Track views

The [`trackView()`](https://docs.tealium.com/platforms/flutter-v1/api/#trackview) method tracks screen views, as shown in the following example:

```dart
Tealium.trackView("SCREEN_NAME");
```

## Track events

The [`trackEvent()`](https://docs.tealium.com/platforms/flutter-v1/api/#trackevent) method tracks non-view events, as shown in the following example:

```dart
Tealium.trackEvent("EVENT_NAME");
```
