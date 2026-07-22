---
title: トラック
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(viewName:mutableMapOf)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名とオプションのデータ辞書で構成されており、追跡呼び出しでは `tealium_event` として表示されます。

以下は例です：

```java
val screenView = TealiumView(
  "purchase", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "order_total" to 10.00, 
    "product_id" to listOf("PROD123", "PROD456"),
    "order_id" to "0123456789"
  )
)
tealium.track(screenView);
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(eventName:mutableMapOf)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名とオプションのデータ辞書で構成されており、追跡呼び出しでは `tealium_event` として表示されます。

以下は例です：

```java
val tealEvent = TealiumEvent(
  "cart_add", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "product_id" to listOf("PROD123", "PROD456"), 
    "product_price" to listOf(4.00, 6.00)
  )
)
tealium.track(tealEvent);
```

## タイムドイベント

[タイムドイベント](https://docs.tealium.com/ja/platforms/getting-started-mobile/timed-events/)は、イベントの持続時間または二つのイベント間の持続時間を測定します。タイムドイベントは自動的または手動でトリガーされます。

### 自動トリガー

イベント間の持続時間を自動的に追跡するには、[`timedEventTriggers`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#timedeventtriggers) を `EventTrigger` オブジェクトのリストに構成し、開始と停止のイベント名を指定します。

以下は自動トリガーでタイムドイベントを追跡する例です：

```java
timedEventTriggers = mutableListOf(EventTrigger.forEventName(
    "cart_add",
    "purchase"))
```

### 手動トリガー

イベントの持続時間を手動で追跡するには、カスタムロジックに基づいてタイムドイベントの開始と停止を行います。

イベントの持続時間の追跡を開始するには [`startTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#starttimedevent) を使用します。  
```java
tealium.startTimedEvent(name: "TimeSpentViewingProduct")
```

タイムドイベントを停止するには [`stopTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#stoptimedevent) を使用します：  
```java
tealium.stopTimedEvent(name: "TimeSpentViewingProduct")
```

以前に開始したタイムドイベントをキャンセルするには [`cancelTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#canceltimedevent) を使用します：  
```java
tealium.cancelTimedEvent(name: "TimeSpentViewingProduct")
```

## トレース

### トレースへの参加

指定されたIDでトレースに参加するには、[`joinTrace()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#jointrace) を呼び出します。Tealium Customer Data Hubの [トレース](https://docs.tealium.com/manage-traces/) 機能についてもっと学びましょう。

```java
Tealium["INSTANCE_NAME"]?.joinTrace("TRACE_ID")
```
以下を置き換えます：
* `INSTANCE_NAME`: Tealium Kotlinライブラリを初期化する際に使用したインスタンス名。
* `TRACE_ID`: 参加したいトレースのID。

### トレースからの離脱

アプリセッションの間、トレースはアクティブな状態が続きますが、[`leaveTrace()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#leavetrace) を呼び出すことで以前に参加したトレースを離れ、訪問セッションを終了します。

```java
Tealium["INSTANCE_NAME"]?.leaveTrace()
```

訪問セッションをリモートで終了するには [`endTraceVisitorSession()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#endtracevisitorsession) を使用しますが、SDKセッションを終了させたり、セッションIDをリセットしたりすることはありません。

```java
Tealium["INSTANCE_NAME"]?.endTraceVisitorSession()
```