---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/roku/track/
---
## トラックイベント

[`TrackEvent()`](/ja/platforms/roku/api/#trackevent) メソッドは、以下の例のようにイベントを追跡します：

```javascript
data = CreateObject(&#34;roAssociativeArray&#34;)
data.someKey = &#34;KEY_VALUE&#34;
teal.TrackEvent(&#34;EVENT_NAME&#34;, data)
```
