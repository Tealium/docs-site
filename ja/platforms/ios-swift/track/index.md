---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

#### 例

```swift
let screenView = TealiumView(
	"purchase",
	dataLayer: [
		"customer_id": "abc123", 
		"order_total": 10.00, 
		"product_id": ["PROD123", "PROD456"], 
		"order_id": "0123456789"
	]
)
tealium?.track(screenView)
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

#### 例

```swift
let tealEvent = TealiumEvent(
	"cart_add", 
	dataLayer: [
		"customer_id": "abc123", 
		"product_id": ["PROD123", "PROD456"], 
		"product_price": [4.00, 6.00]
	]
)
tealium?.track(tealEvent)
```

## タイムドイベント

[タイムドイベント](https://docs.tealium.com/ja/platforms/getting-started-mobile/timed-events/)は、単一のイベントの持続時間または二つのイベント間の時間を測定します。タイムドイベントは自動的または手動でトリガーされます。

### 自動トリガー

イベント間の持続時間を自動的に追跡するには、[`timedEventTriggers`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#timedeventtriggers) を `TimedEventTrigger` オブジェクトのリストに構成し、開始と停止のイベント名を指定します。

自動トリガーでタイムドイベントを追跡する例は以下の通りです：

```swift
config.timedEventTriggers = [TimedEventTrigger(
    start: "cart_add",
    stop: "purchase")]
```

### 手動トリガー

カスタムロジックに基づいてイベントの持続時間を手動で追跡するには、イベントの持続時間の追跡を [`startTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#starttimedevent) で開始します：  
```swift
tealium.startTimedEvent(name: "TimeSpentViewingProduct")
```

タイムドイベントを [`stopTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#stoptimedevent) で停止します：    
```swift
tealium.stopTimedEvent(name: "TimeSpentViewingProduct")
```

以前に開始したタイムドイベントを [`cancelTimedEvent()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#canceltimedevent) でキャンセルします：    
```swift
tealium.cancelTimedEvent(name: "TimeSpentViewingProduct")
```

以前に開始したすべてのタイムドイベントを [`clearAllTimedEvents()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#clearalltimedevents) でクリアします：    
```swift
tealium?.clearAllTimedEvents()
```

## トレース

### トレースに参加

[`joinTrace()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#jointrace) メソッドは指定されたIDでトレースに参加します。Tealium Customer Data Hubの[トレース](https://docs.tealium.com/manage-traces/)機能についてもっと学びましょう。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(id: "TRACE_ID")
		// ...
	}
}
```
`TRACE_ID` を参加したいトレースのIDに置き換えてください。

### トレースを離れる

トレースはアプリセッションの間有効であり、[`leaveTrace()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#leavetrace) メソッドが呼ばれると、以前に参加したトレースを離れ、訪問セッションが終了します。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func leaveTrace() {
		tealium?.leaveTrace()
		// ...
	}
}
```

セッションが終了するまで、"訪問の終了時"に構成されたコネクタアクションは実行されません。

トレースを離れる際に訪問セッションを保持するには、次の例に示すようにオプションの引数 `false` を渡します：

```swift
tealium?.leaveTrace(killVisitorSession: false)
```