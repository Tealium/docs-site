---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/track/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## ビューの追跡

次の例に示すように、[`trackView()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#trackview) メソッドは画面ビューを追跡します：

```dart
Tealium.trackView("SCREEN_NAME");
```

## イベントの追跡

次の例に示すように、[`trackEvent()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#trackevent) メソッドはビュー以外のイベントを追跡します：

```dart
Tealium.trackEvent("EVENT_NAME");
```