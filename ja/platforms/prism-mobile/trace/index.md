---
title: トレース
description: Tealium Prism SDK の実装をデバッグおよび検証するためにトレースセッションを使用します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/trace/
---
Trace モジュールは、Tealium Prism SDK のデバッグおよびテスト機能を提供します。トレースセッションを使用してイベントをリアルタイムで監視し、イベントが正しくトラッキングおよび送信されていることを確認します。トレースがアクティブな間は、サーバー側でのフィルタリングと分析のため、すべてのトラッキングイベントにトレース ID が自動的に追加されます。

トレースツールの詳細については、[トレースによるデバッグ](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/)を参照してください。

## 収集されるデータポイント

トレースセッションがアクティブな場合、Trace モジュールは次のデータを収集します。

| データポイント | キー | 説明 |
|:-----------|:----|:------------|
| トレース ID | `cp.trace_id` | アクティブなトレースセッションの一意の識別子（レガシー互換性用） |
| トレース ID | `tealium_trace_id` | アクティブなトレースセッションの一意の識別子 |

## インストール

Trace モジュールは、プログラム、リモート JSON、またはローカル JSON の構成を使用して構成できます。

トレース ID を含めるイベントを制限するには、モバイルプロファイルに Trace モジュールを追加し、ルールを割り当てます。詳細については、[ルール](https://docs.tealium.com/rules/)を参照してください。


<blockquote>
React Native では、Tealium 構成 JSON を使用して Trace モジュールを有効にします。プログラムによる構成は必要ありません。
</blockquote>




Tealium 構成に Trace モジュールを追加します。

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev",
    modules = listOf(Modules.trace())
).build()
```

強制構成を使用して構成するには、次のようにします。

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev",
    modules = listOf(Modules.trace {
        it.setEnabled(true)
            .setTrackErrors(true)
    })
).build()
```


Tealium 構成に Trace モジュールを追加します。

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.trace(),
                              // other modules...
                          ])
```

強制構成を使用して構成するには、次のようにします。

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.trace(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setTrackErrors(true)
                              }),
                              // other modules...
                          ])
```



### JSON 構成

ローカルまたはリモートの構成 JSON ファイルで Trace モジュールを構成します。

```json
{
    "modules": {
        "Trace": {
            "module_type": "Trace",
            "enabled": true,
            "configuration": {
                "track_errors": true
            }
        }
    }
}
```

## トレースセッションへの参加

トレースセッションを開始するには、トレース ID を指定して `trace.join()` を呼び出します。`leave()` を呼び出すかセッションが期限切れになるまで、以降のすべてのイベントにトレース ID が追加されます。



```kotlin
tealium.trace.join("your-trace-id")
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.trace.join(id: "your-trace-id").subscribe { result in
    // Optionally handle result here
}
```


```javascript
await tealium.trace.join("your-trace-id");
```



## トレースセッションからの退出

トレースセッションを停止するには、`trace.leave()` を呼び出します。これにより、以降のイベントからトレース ID が削除されます。



```kotlin
tealium.trace.leave()
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.trace.leave().subscribe { result in
    // Optionally handle result here
}
```


```javascript
await tealium.trace.leave();
```



## 訪問の強制終了

AudienceStream の「End of Visit」アクションをテストするには、セッションが期限切れになるのを待たず、セッションを直ちに強制終了します。



```kotlin
tealium.trace.forceEndOfVisit()
    .subscribe { result ->
        // Handle the track result
    }
```


```swift
tealium.trace.forceEndOfVisit().subscribe { result in
    // Handle the track result
}
```


```javascript
await tealium.trace.forceEndOfVisit();
```



`leave()` が呼び出されるまで、トレースはアクティブなままです。`forceEndOfVisit()` メソッドは、標準のデキュー処理フローに従って、セッションの終了を通知するトラッキング呼び出しを送信します。

## エラートラッキング

エラートラッキングが有効な場合（`track_errors: true`）、Trace モジュールは、アクティブなトレースセッション中に発生した SDK エラーを自動的にトラッキングします。重複するエラーレポートを防ぐため、モジュールはカテゴリ別にエラーを重複排除します。

* トレースセッションごとに、各カテゴリの最初のエラーのみがトラッキングされます
* 同じカテゴリの後続エラーは、新しいトレースセッションが開始されるまで無視されます
* 新しいトレースセッションへの参加または現在のセッションからの退出により、重複排除キャッシュがリセットされます

## QR トレース

ディープリンクから直接トレースを開始することもできます。開いた URL に適切なクエリパラメータが含まれている場合、トレースが自動的に開始されます。通常、これは Tealium プラットフォームの QR トレースツールを使用して行います。詳細については、[トレースによるデバッグ](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/)を参照してください。

## API リファレンス

クラスおよびメソッドの詳細なシグネチャについては、API リファレンスドキュメントを参照してください。

* [Trace（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)
* [TraceSettingsBuilder（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/TraceSettingsBuilder.html)
* [Trace（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/)
* [Trace（React Native）](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html)