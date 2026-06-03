---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/android-java/track/
---
## ビューの追跡

[`trackView()`](/ja/platforms/android-java/api/tealium/#trackview) メソッドは、以下の例のように画面ビューを追跡します：

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE_NAME&#34;).trackView(&#34;EVENT_NAME&#34;, data);
```

最初のパラメータとして渡される値は、データレイヤー内で `tealium_event` という変数として表示されます。

## イベントの追跡

[`trackEvent()`](/ja/platforms/android-java/api/tealium/#trackevent) メソッドは、以下の例のように非ビューイベントを追跡します：

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE_NAME&#34;).trackEvent(&#34;EVENT_NAME&#34;, data);
```
