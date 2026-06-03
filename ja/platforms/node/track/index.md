---
title: トラッキング
description: ユーザーアクティビティをトラッキングするためのメソッドについて説明します。
url: https://docs.tealium.com/ja/platforms/node/track/
---
## イベント/ビューのトラッキング

[`track()`](/ja/platforms/node/api/#track)メソッドは、次の例に示すように、すべてのイベントとページビューをトラッキングします。


```javascript
tealium.track(&#34;EVENT_NAME&#34;, {&#34;KEY&#34;: &#34;VALUE&#34;}); 
```

## 訪問のトラッキング

アプリケーションでユーザーアクティビティをトラッキングしていて、イベントを訪問に関連付ける場合には、次の例に示すように、データオブジェクト内の`tealium_visitor_id`属性をインクルードします。

```javascript
var myVisitorId = myVisitorIdFunction();

tealium.track(&#34;page_view&#34;, {
    &#34;tealium_visitor_id&#34; : myVisitorId,
    &#34;some_key&#34;           : &#34;KEY&#34;
});
```

このイベント属性により、匿名で、またはメールアドレスなどの個人識別子を使用して、現在のユーザーを一意に特定できます。
