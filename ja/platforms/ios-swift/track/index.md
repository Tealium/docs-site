---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](/ja/platforms/ios-swift/api/tealium/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

#### 例

```swift
let screenView = TealiumView(
	&#34;purchase&#34;,
	dataLayer: [
		&#34;customer_id&#34;: &#34;abc123&#34;, 
		&#34;order_total&#34;: 10.00, 
		&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
		&#34;order_id&#34;: &#34;0123456789&#34;
	]
)
tealium?.track(screenView)
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(tealiumEvent:dataLayer:)` のインスタンスを [`track()`](/ja/platforms/ios-swift/api/tealium/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

#### 例

```swift
let tealEvent = TealiumEvent(
	&#34;cart_add&#34;, 
	dataLayer: [
		&#34;customer_id&#34;: &#34;abc123&#34;, 
		&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
		&#34;product_price&#34;: [4.00, 6.00]
	]
)
tealium?.track(tealEvent)
```

## タイムドイベント

[タイムドイベント](/ja/platforms/getting-started-mobile/timed-events/)は、単一のイベントの持続時間または二つのイベント間の時間を測定します。タイムドイベントは自動的または手動でトリガーされます。

### 自動トリガー

イベント間の持続時間を自動的に追跡するには、[`timedEventTriggers`](/ja/platforms/ios-swift/api/tealium-config/#timedeventtriggers) を `TimedEventTrigger` オブジェクトのリストに構成し、開始と停止のイベント名を指定します。

自動トリガーでタイムドイベントを追跡する例は以下の通りです：

```swift
config.timedEventTriggers = [TimedEventTrigger(
    start: &#34;cart_add&#34;,
    stop: &#34;purchase&#34;)]
```

### 手動トリガー

カスタムロジックに基づいてイベントの持続時間を手動で追跡するには、イベントの持続時間の追跡を [`startTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#starttimedevent) で開始します：  
```swift
tealium.startTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

タイムドイベントを [`stopTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#stoptimedevent) で停止します：    
```swift
tealium.stopTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

以前に開始したタイムドイベントを [`cancelTimedEvent()`](/ja/platforms/android-kotlin/api/tealium/#canceltimedevent) でキャンセルします：    
```swift
tealium.cancelTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

以前に開始したすべてのタイムドイベントを [`clearAllTimedEvents()`](/ja/platforms/ios-swift/api/tealium/#clearalltimedevents) でクリアします：    
```swift
tealium?.clearAllTimedEvents()
```

## トレース

### トレースに参加

[`joinTrace()`](/ja/platforms/ios-swift/api/tealium/#jointrace) メソッドは指定されたIDでトレースに参加します。Tealium Customer Data Hubの[トレース]()機能についてもっと学びましょう。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(id: &#34;TRACE_ID&#34;)
		// ...
	}
}
```
`TRACE_ID` を参加したいトレースのIDに置き換えてください。

### トレースを離れる

トレースはアプリセッションの間有効であり、[`leaveTrace()`](/ja/platforms/ios-swift/api/tealium/#leavetrace) メソッドが呼ばれると、以前に参加したトレースを離れ、訪問セッションが終了します。

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

セッションが終了するまで、&#34;訪問の終了時&#34;に構成されたコネクタアクションは実行されません。

トレースを離れる際に訪問セッションを保持するには、次の例に示すようにオプションの引数 `false` を渡します：

```swift
tealium?.leaveTrace(killVisitorSession: false)
```