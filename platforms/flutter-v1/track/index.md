---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/flutter-v1/track/
---This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

## Track views

The [`trackView()`](/platforms/flutter-v1/api/#trackview) method tracks screen views, as shown in the following example:

```dart
Tealium.trackView(&#34;SCREEN_NAME&#34;);
```

## Track events

The [`trackEvent()`](/platforms/flutter-v1/api/#trackevent) method tracks non-view events, as shown in the following example:

```dart
Tealium.trackEvent(&#34;EVENT_NAME&#34;);
```
