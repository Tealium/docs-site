---
title: 時間計測イベント
description: イベントの継続時間を追跡する方法について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/timed-events/
---
## サポート対象プラットフォーム

次のプラットフォームは時間計測イベントをサポートしています。

- [Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/)
- [iOS（Swift v2.x）](https://docs.tealium.com/ja/platforms/ios-swift/)

## 仕組み

時間計測イベントは、イベントの継続時間または2つのイベント間の時間を計測し、自動トリガーまたは手動トリガーを使用して構成します。時間計測イベントが完了すると、その時間計測イベントの名前と計測の詳細を含む `timed_event` という名前のイベントが Event Streaming に送信されます。

アプリですでに追跡されている Tealium イベント間の時間を計測するには、自動トリガーを使用します。指定した開始イベントが発生すると時間計測イベントが自動的に開始され、指定した停止イベントが発生すると終了します。

Tealium で追跡されていないイベント間の時間や、複雑な一連のイベントに要する時間を計測するには、手動トリガーを使用します。カスタムロジックに基づいてアプリコード内で時間計測イベントを開始および停止することで、手動でトリガーします。

各時間計測イベントには名前があり、イベント属性 `timed_event_name` に構成されます。時間計測イベントの終了後はイベント名を再利用できますが、同時に実行される複数の時間計測イベントで同じ名前を使用することはできません。

時間計測イベントは永続化されないため、イベントが終了する前にアプリが終了すると破棄されます。

時間計測イベントの使用方法については、以下を参照してください。

- [Android Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/track/#timed-events)
- [iOS（Swift v2.x）](https://docs.tealium.com/ja/platforms/ios-swift/track/#timed-events)

### 自動トリガー

自動トリガーを使用して時間計測イベントを追跡するには、開始および停止の Tealium イベント名を指定します。これらのイベントは、アプリですでに追跡されている必要があります。自動時間計測イベントの名前は、開始イベント名と停止イベント名を2つのコロン（`::`）で連結して生成されます。たとえば、`cart_add` イベントと `purchase` イベントの間の時間を追跡するように自動トリガーを構成すると、イベント属性 `timed_event_name` は `cart_add::purchase` に構成されます。



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



自動トリガーによって生成される時間計測イベントは次のとおりです。  

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

手動トリガーを使用して時間計測イベントを追跡するには、時間計測イベントの名前を指定し、アプリコード内で時間計測イベントを手動で開始および停止します。たとえば、ユーザーが商品の閲覧に費やした時間を手動で追跡するには、商品画面が読み込まれたときに時間計測イベントを開始し、ユーザーが商品画面から離れたときに停止します。時間計測イベントに使用した名前が、イベント属性 `timed_event_name` の値に構成されます。

時間計測イベントを手動で開始します。
  
```swift
tealium.startTimedEvent(name: "TimeSpentViewingProduct")
```

時間計測イベントを手動で停止します。

```swift
tealium.stopTimedEvent(name: "TimeSpentViewingProduct")
```

手動トリガーによって生成される時間計測イベントは次のとおりです。  

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

時間計測イベントは、イベント名 `timed_event` と次の属性を使用して追跡されます。

| 属性名 | データ型 | 値 |
| ---------------------- | --------- | ------------------------------------ |
| `tealium_event`        | `String`  | `"timed_event"` |
| `timed_event_name`     | `String`  | 時間計測イベントの名前（自動トリガーのデフォルトは `"start_event_name::stop_event_name"`） |
| `timed_event_start`    | `String`  | 時間計測イベントの開始時刻（ミリ秒単位の UNIX 時刻） |
| `timed_event_end`      | `String`  | 時間計測イベントの終了時刻（ミリ秒単位の UNIX 時刻） |
| `timed_event_duration` | `String`  | 時間計測イベントの継続時間（合計ミリ秒：`timed_event_end` - `timed_event_start`） |

時間計測イベントの例を次に示します。  

```bash
{
  "tealium_event": "timed_event",
  "timed_event_name": "cart_add::purchase",
  "timed_event_start": "1605645967299",
  "timed_event_end": "1605645968401",
  "timed_event_duration": "1102"
}
```