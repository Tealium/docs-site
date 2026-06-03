---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/csharp/track/
---
## トラックイベント

Tealiumオブジェクトが定義されたら、[`Track()`](/ja/platforms/csharp/api/#track)メソッドを使用してイベントの追跡を開始します。

次の例は、イベント名のみで呼び出しを追跡します：  
```csharp
tealium.Track(&#34;EVENT_NAME&#34;);
```  

次の例は、イベント名とオプションのデータ辞書で呼び出しを追跡します：  
```csharp
Dictionary&lt;string, object&gt; customData = new Dictionary() {
    {&#34;KEY1&#34;, new string[]{&#34;STRING1&#34;,&#34;STRING2&#34;}},
    {&#34;KEY2&#34;, &#34;VALUE2&#34;},
    {&#34;KEY3&#34;, &#34;VALUE3&#34;}};
tealium.Track(&#34;EVENT_NAME&#34;, customData);
```

次の例は、イベント名、オプションのデータ辞書、およびトラック完了で呼び出しを追跡します：  
```csharp
Dictionary&lt;string, object&gt; customData = new Dictionary() {
    {&#34;KEY1&#34;, new string[]{&#34;STRING1&#34;,&#34;STRING2&#34;}},
    {&#34;KEY2&#34;, &#34;VALUE2&#34;},
    {&#34;KEY3&#34;, &#34;VALUE3&#34;}};
tealium.Track(&#34;EVENT_NAME,
    customData,
    (success, info, error)=&gt;) {
        Debug.WriteLine(&#34;eventTrackComplete: was successful: &#34; &#43; success);
});
```

## トレース

このライブラリは[HTTP API](/ja/platforms/http-api/)を使用し、デバッグ目的でTrace IDを送信することをサポートしています。

### トレースに参加

[`JoinTrace()`](/ja/platforms/csharp/api/#jointrace)メソッドは、次の例に示すように、トレースに参加します：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
```

### トレースを離れる

[`LeaveTrace()`](/ja/platforms/csharp/api/#leavetrace)メソッドは、次の例に示すように、トレースを離れます：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
//...
instance.LeaveTrace();
```

`tealium_trace_id`は、今後のイベントで自動的に入力されなくなります。

### トレースを終了

[`KillTraceSession()`](/ja/platforms/csharp/api/#killtracesession)メソッドは、次の例に示すように、トレースを終了します：

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
//...
instance.KillTraceSession();
```

`KillTraceSession()`メソッドは、サーバーで訪問のトレースセッションを終了/終了するイベントをトリガーします。これは、Tealium Customer Data Hub構成での訪問終了時の動作をテストするのに便利です。

また、このメソッドは[`LeaveTrace()`](/ja/platforms/csharp/api/#leavetrace)メソッドを呼び出して、期限切れの`tealium_trace_id`を削除し、以前のトレースIDで送信されるイベントを停止します。
