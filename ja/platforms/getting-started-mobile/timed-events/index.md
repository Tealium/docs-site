---
title: タイムドイベント
description: イベントの持続時間を追跡する方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/timed-events/
---
## サポートされているプラットフォーム

以下のプラットフォームではタイムドイベントがサポートされています：

- [Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/)
- [iOS (Swift v2.x)](https://docs.tealium.com/ja/platforms/ios-swift/)

## 仕組み

タイムドイベントは、イベントの持続時間や2つのイベント間の時間を測定し、自動または手動のトリガーで構成します。タイムドイベントが完了すると、タイムドイベントの名前とタイミングの詳細を持つ`timed_event`という名前のイベントをTealium EventStreamに送信します。

すでにアプリで追跡されているTealiumイベント間の持続時間を測定するために自動トリガーを使用します。指定した開始イベントが発生すると自動的にタイムドイベントがトリガーされ、指定した停止イベントが発生すると停止します。

Tealiumで追跡されていないイベントや、複雑なイベントのシーケンスを含むイベント間の持続時間を測定するために手動トリガーを使用します。タイムドイベントは、カスタムロジックに基づいてアプリコードでタイムドイベントを開始および停止することで手動でトリガーされます。

各タイムドイベントには、イベント属性`timed_event_name`に構成された名前があります。タイムドイベントが終了した後にイベント名を再利用することは可能ですが、同時に複数のタイムドイベントが同じ名前を使用することはできません。

タイムドイベントは永続的ではなく、イベントが終了する前にアプリが終了すると破棄されます。

タイムドイベントの使用方法を学びましょう：

- [Android Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/track/#timed-events)
- [iOS (Swift v2.x)](https://docs.tealium.com/ja/platforms/ios-swift/track/#timed-events)

### 自動トリガー

自動トリガーでタイムドイベントを追跡するには、開始と停止のTealiumイベント名を指定します。これらのイベントはすでにアプリで追跡されている必要があります。自動タイムドイベントの名前は、開始と停止のイベント名を二つのコロン(`::`)で結合して生成されます。例えば、`cart_add`イベントと`purchase`イベントの間の持続時間を追跡するために自動トリガーを構成すると、イベント属性`timed_event_name`は`cart_add::purchase`に構成されます。



```kotlin
val config = TealiumConfig(…).apply {
   timedEventTriggers = mutableListOf(EventTrigger.forEventName(
        "cart_add",
        "purchase"))
}
```


```swift
let config = TealiumConfig(...)
config.timedEventTriggers = [TimedEventTrigger(
    start: "cart_add",
    stop: "purchase")]
```



自動トリガーからの結果となるタイムドイベント：  

```bash
{
  "tealium_event": "timed_event",
  "timed_event_name": "cart_add::purchase",
  "timed_event_start": "1605645967299",
  "timed_event_end": "1605645968401",
  "timed_event_duration": "1102"
}
```

### 手動トリガー

手動トリガーでタイムドイベントを追跡するには、タイムドイベントの名前を指定し、アプリコードでタイムドイベントを手動で開始および停止します。例えば、ユーザーが製品を閲覧する時間を手動で追跡するには、製品画面がロードされたときにタイムドイベントを開始し、ユーザーが製品画面を離れたときにタイムドイベントを停止します。タイムドイベントに使用する名前は、イベント属性`timed_event_name`の値に構成されます。

手動でタイムドイベントを開始する：
  
```swift
tealium.startTimedEvent(name: "TimeSpentViewingProduct")
```

手動でタイムドイベントを停止する：

```swift
tealium.stopTimedEvent(name: "TimeSpentViewingProduct")
```

手動トリガーからの結果となるタイムドイベント：  

```bash
{
  "tealium_event": "timed_event",
  "timed_event_name": "TimeSpentViewingProduct",
  "timed_event_start": "1605645967299",
  "timed_event_end": "1605645968401",
  "timed_event_duration": "1102"
}
```

## データレイヤー

タイムドイベントは、イベント名`timed_event`と以下の属性で追跡されます：

| 属性名                  | データタイプ | 値 |
| ---------------------- | --------- | ------------------------------------ |
| `tealium_event`        | `String`  | `"timed_event"` |
| `timed_event_name`     | `String`  | タイムドイベントの名前（自動トリガーの場合はデフォルトで`"start_event_name::stop_event_name"`）  |
| `timed_event_start`    | `String`  | タイムドイベントの開始時間（UNIX時間、ミリ秒） |
| `timed_event_end`      | `String`  | タイムドイベントの終了時間（UNIX時間、ミリ秒）   |
| `timed_event_duration` | `String`  | タイムドイベントの持続時間（合計ミリ秒：`timed_event_end` - `timed_event_start`）   |

以下はタイムドイベントの例です：  

```bash
{
  "tealium_event": "timed_event",
  "timed_event_name": "cart_add::purchase",
  "timed_event_start": "1605645967299",
  "timed_event_end": "1605645968401",
  "timed_event_duration": "1102"
}
```
