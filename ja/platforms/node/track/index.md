---
title: トラッキング
description: ユーザーアクティビティをトラッキングするためのメソッドについて説明します。
url: https://docs.tealium.com/ja/platforms/node/track/
---
## イベント/ビューのトラッキング

[`track()`](https://docs.tealium.com/ja/platforms/node/api/#track)メソッドは、次の例に示すように、すべてのイベントとページビューをトラッキングします。


```javascript
tealium.track("EVENT_NAME", {"KEY": "VALUE"}); 
```

## 訪問のトラッキング

アプリケーションでユーザーアクティビティをトラッキングしていて、イベントを訪問に関連付ける場合には、次の例に示すように、データオブジェクト内の`tealium_visitor_id`属性をインクルードします。

```javascript
var myVisitorId = myVisitorIdFunction();

tealium.track("page_view", {
    "tealium_visitor_id" : myVisitorId,
    "some_key"           : "KEY"
});
```

このイベント属性により、匿名で、またはメールアドレスなどの個人識別子を使用して、現在のユーザーを一意に特定できます。
