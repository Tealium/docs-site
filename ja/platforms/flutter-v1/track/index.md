---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/track/
---これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)をご覧ください。

## ビューの追跡

次の例に示すように、[`trackView()`](/ja/platforms/flutter-v1/api/#trackview) メソッドは画面ビューを追跡します：

```dart
Tealium.trackView(&#34;SCREEN_NAME&#34;);
```

## イベントの追跡

次の例に示すように、[`trackEvent()`](/ja/platforms/flutter-v1/api/#trackevent) メソッドはビュー以外のイベントを追跡します：

```dart
Tealium.trackEvent(&#34;EVENT_NAME&#34;);
```