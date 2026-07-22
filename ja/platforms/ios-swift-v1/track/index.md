---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/track/
---
<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[iOS（Swift）用Tealium 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)をご覧ください。
</blockquote>


## ビューのトラッキング

[`trackView()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#trackview)メソッドは、関連データを持つ画面ビューを追跡し、オプションでコールバック関数をトリガーします。

```swift
let mydata = ["KEY": "VALUE"]
// タイプ指定と完了ブロックでのトラックコール
tealium?.trackView(title: "EVENT_NAME",
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
//...
})
```


<blockquote>
`title`に渡された値はデータレイヤーで`tealium_event`変数として表示されます。
</blockquote>


## イベントのトラッキング

[`track()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#track)メソッドは、関連データを持つイベントを追跡し、オプションでコールバック関数をトリガーします。

```swift
let mydata = ["KEY": "VALUE"]
// タイプ指定と完了ブロックでのトラックコール
tealium?.track(title: "EVENT_NAME",
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
 //...
})
```


<blockquote>
`title`に渡された値はデータレイヤーで`tealium_event`変数として表示されます。
</blockquote>


## トレース

### トレースへの参加

[`joinTrace()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#jointrace)メソッドは、指定されたIDでトレースに参加します。Tealium Customer Data Hubのトレース機能について[詳しくはこちら](https://docs.tealium.com/manage-traces/)。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(traceId: "TRACE_ID")
		// ...
	}
}
```

### トレースの離脱

アプリセッションの間、トレースはアクティブな状態が続きますが、[`leaveTrace()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#leavetrace)メソッドが呼ばれると、以前に参加したトレースを離れ、訪問セッションが終了します。

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

訪問の終了時に構成されたコネクタアクションは、セッションが終了するまで実行されません。

トレースを離れる際に訪問セッションを保持するには、次の例に示すようにオプショナル引数`false`を渡します：

```swift
tealium?.leaveTrace(killVisitorSession: false)
```