---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/csharp/track/
---
## トラックイベント

Tealiumオブジェクトが定義されたら、[`Track()`](https://docs.tealium.com/ja/platforms/csharp/api/#track)メソッドを使用してイベントの追跡を開始します。

次の例は、イベント名のみで呼び出しを追跡します：  
```csharp
tealium.Track("EVENT_NAME");
```  

次の例は、イベント名とオプションのデータ辞書で呼び出しを追跡します：  
```csharp
Dictionary<string, object> customData = new Dictionary() {
    {"KEY1", new string[]{"STRING1","STRING2"}},
    {"KEY2", "VALUE2"},
    {"KEY3", "VALUE3"}};
tealium.Track("EVENT_NAME", customData);
```

次の例は、イベント名、オプションのデータ辞書、およびトラック完了で呼び出しを追跡します：  
```csharp
Dictionary<string, object> customData = new Dictionary() {
    {"KEY1", new string[]{"STRING1","STRING2"}},
    {"KEY2", "VALUE2"},
    {"KEY3", "VALUE3"}};
tealium.Track("EVENT_NAME,
    customData,
    (success, info, error)=>) {
        Debug.WriteLine("eventTrackComplete: was successful: " + success);
});
```

## トレース

このライブラリは[HTTP API](https://docs.tealium.com/ja/platforms/http-api/)を使用し、デバッグ目的でTrace IDを送信することをサポートしています。

### トレースに参加

[`JoinTrace()`](https://docs.tealium.com/ja/platforms/csharp/api/#jointrace)メソッドは、次の例に示すように、トレースに参加します：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
```

### トレースを離れる

[`LeaveTrace()`](https://docs.tealium.com/ja/platforms/csharp/api/#leavetrace)メソッドは、次の例に示すように、トレースを離れます：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
//...
instance.LeaveTrace();
```

`tealium_trace_id`は、今後のイベントで自動的に入力されなくなります。

### トレースを終了

[`KillTraceSession()`](https://docs.tealium.com/ja/platforms/csharp/api/#killtracesession)メソッドは、次の例に示すように、トレースを終了します：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
//...
instance.KillTraceSession();
```

`KillTraceSession()`メソッドは、サーバーで訪問のトレースセッションを終了/終了するイベントをトリガーします。これは、Tealium Customer Data Hub構成での訪問終了時の動作をテストするのに便利です。

また、このメソッドは[`LeaveTrace()`](https://docs.tealium.com/ja/platforms/csharp/api/#leavetrace)メソッドを呼び出して、期限切れの`tealium_trace_id`を削除し、以前のトレースIDで送信されるイベントを停止します。
