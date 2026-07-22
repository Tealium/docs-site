---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/roku/track/
---
## トラックイベント

[`TrackEvent()`](https://docs.tealium.com/ja/platforms/roku/api/#trackevent) メソッドは、以下の例のようにイベントを追跡します：

```javascript
data = CreateObject("roAssociativeArray")
data.someKey = "KEY_VALUE"
teal.TrackEvent("EVENT_NAME", data)
```
