---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/android-java/track/
---
## ビューの追跡

[`trackView()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackview) メソッドは、以下の例のように画面ビューを追跡します：

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE_NAME").trackView("EVENT_NAME", data);
```


<blockquote>
最初のパラメータとして渡される値は、データレイヤー内で `tealium_event` という変数として表示されます。
</blockquote>


## イベントの追跡

[`trackEvent()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackevent) メソッドは、以下の例のように非ビューイベントを追跡します：

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE_NAME").trackEvent("EVENT_NAME", data);
```
