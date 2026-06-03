---
title: トラック
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(viewName:mutableMapOf)` のインスタンスを [`track()`](/ja/platforms/android-kotlin/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名とオプションのデータ辞書で構成されており、追跡呼び出しでは `tealium_event` として表示されます。

以下は例です：

```java
val screenView = TealiumView(
  &#34;purchase&#34;, 
  mutableMapOf(
    &#34;customer_id&#34; to &#34;abc123&#34;, 
    &#34;order_total&#34; to 10.00, 
    &#34;product_id&#34; to listOf(&#34;PROD123&#34;, &#34;PROD456&#34;),
    &#34;order_id&#34; to &#34;0123456789&#34;
  )
)
tealium.track(screenView);
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(eventName:mutableMapOf)` のインスタンスを [`track()`](/ja/platforms/android-kotlin/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名とオプションのデータ辞書で構成されており、追跡呼び出しでは `tealium_event` として表示されます。

以下は例です：

```java
val tealEvent = TealiumEvent(
  &#34;cart_add&#34;, 
  mutableMapOf(
    &#34;customer_id&#34; to &#34;abc123&#34;, 
    &#34;product_id&#34; to listOf(&#34;PROD123&#34;, &#34;PROD456&#34;), 
    &#34;product_price&#34; to listOf(4.00, 6.00)
  )
)
tealium.track(tealEvent);
```

## タイムドイベント

[タイムドイベント](/ja/platforms/getting-started-mobile/timed-events/)は、イベントの持続時間または二つのイベント間の持続時間を測定します。タイムドイベントは自動的または手動でトリガーされます。

### 自動トリガー

イベント間の持続時間を自動的に追跡するには、[`timedEventTriggers`](/ja/platforms/android-kotlin/api/tealium-config/#timedeventtriggers) を `EventTrigger` オブジェクトのリストに構成し、開始と停止のイベント名を指定します。

以下は自動トリガーでタイムドイベントを追跡する例です：

```java
timedEventTriggers = mutableListOf(EventTrigger.forEventName(
    &#34;cart_add&#34;,
    &#34;purchase&#34;))
```

### 手動トリガー

イベントの持続時間を手動で追跡するには、カスタムロジックに基づいてタイムドイベントの開始と停止を行います。

イベントの持続時間の追跡を開始するには [`startTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#starttimedevent) を使用します。  
```java
tealium.startTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

タイムドイベントを停止するには [`stopTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#stoptimedevent) を使用します：  
```java
tealium.stopTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

以前に開始したタイムドイベントをキャンセルするには [`cancelTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#canceltimedevent) を使用します：  
```java
tealium.cancelTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

## トレース

### トレースへの参加

指定されたIDでトレースに参加するには、[`joinTrace()`](/ja/platforms/android-kotlin/api/tealium/#jointrace) を呼び出します。Tealium Customer Data Hubの [トレース]() 機能についてもっと学びましょう。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.joinTrace(&#34;TRACE_ID&#34;)
```
以下を置き換えます：
* `INSTANCE_NAME`: Tealium Kotlinライブラリを初期化する際に使用したインスタンス名。
* `TRACE_ID`: 参加したいトレースのID。

### トレースからの離脱

アプリセッションの間、トレースはアクティブな状態が続きますが、[`leaveTrace()`](/ja/platforms/android-kotlin/api/tealium/#leavetrace) を呼び出すことで以前に参加したトレースを離れ、訪問セッションを終了します。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.leaveTrace()
```

訪問セッションをリモートで終了するには [`endTraceVisitorSession()`](/ja/platforms/android-kotlin/api/tealium/#endtracevisitorsession) を使用しますが、SDKセッションを終了させたり、セッションIDをリセットしたりすることはありません。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.endTraceVisitorSession()
```