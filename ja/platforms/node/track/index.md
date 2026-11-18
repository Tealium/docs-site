---
title: トラッキング
description: ユーザーアクティビティをトラッキングする方法について説明します。
url: https://docs.tealium.com/ja/platforms/node/track/
---
## イベント／ビューのトラッキング

[`track()`](https://docs.tealium.com/ja/platforms/node/api/#track) メソッドは、次の例に示すように、すべてのイベントとページビューをトラッキングします。

```javascript
tealium.track("EVENT_NAME", {"KEY": "VALUE"}); 
```

## 訪問のトラッキング

アプリケーションでユーザーアクティビティをトラッキングし、イベントを訪問に関連付ける場合は、次の例に示すように、データオブジェクトに `tealium_visitor_id` 属性を含めます。

```javascript
var myVisitorId = myVisitorIdFunction();

tealium.track("page_view", {
    "tealium_visitor_id" : myVisitorId,
    "some_key"           : "KEY"
});
```

このイベント属性は、匿名またはメールアドレスなどの個人識別子を使用して、現在のユーザーを一意に識別します。