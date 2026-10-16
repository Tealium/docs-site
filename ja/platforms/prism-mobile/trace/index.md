---
title: トレース
description: Tealium Prism SDKの実装をデバッグおよび検証するためのトレースセッションを使用します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/trace/
---
トレースモジュールは、Tealium Prism SDKのデバッグとテスト機能を提供します。リアルタイムイベントモニタリングのためのトレースセッションを使用して、イベントが正しく追跡およびディスパッチされていることを確認します。トレースがアクティブな場合、トレースIDはすべてのトラッキングイベントに自動的に追加され、サーバー側のフィルタリングと分析のために使用されます。

トレースツールについての詳細は、[トレースでデバッグ](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/)を参照してください。

## 収集されるデータポイント

トレースセッションがアクティブな場合、トレースモジュールは以下のデータを収集します：

| データポイント | キー | 説明 |
|:-----------|:----|:------------|
| トレースID | `cp.trace_id` | アクティブなトレースセッションの一意の識別子（レガシー互換性） |
| トレースID | `tealium_trace_id` | アクティブなトレースセッションの一意の識別子 |

## インストール

トレースモジュールは、プログラム、リモートJSON、またはローカルJSON構成を使用して構成できます。


<blockquote>
React Nativeでは、Tealium構成JSONを介してトレースモジュールが有効になります。プログラム構成は必要ありません。
</blockquote>




Tealium構成にトレースモジュールを追加します：

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.trace())
.build()
```

強制構成で構成する場合：

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.trace {
    setEnabled(true)
    setTrackErrors(true)
})
.build()
```


Tealium構成にトレースモジュールを追加します：

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.trace(),
                              // 他のモジュール...
                          ])
```

強制構成で構成する場合：

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.trace(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setTrackErrors(true)
                              }),
                              // 他のモジュール...
                          ])
```



### JSON構成

ローカルまたはリモートの構成JSONファイルでトレースモジュールを構成します：

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

## トレースセッションに参加する

トレースセッションを開始するには、トレースIDを指定して`trace.join()`を呼び出します。トレースIDは、`leave()`を呼び出すかセッションが期限切れになるまで、すべての将来のイベントに追加されます。



```kotlin
tealium.trace.join("your-trace-id")
    .subscribe { result ->
        // 必要に応じてここで結果を処理します
    }
```


```swift
tealium.trace.join(id: "your-trace-id").subscribe { result in
    // 必要に応じてここで結果を処理します
}
```


```javascript
await tealium.trace.join("your-trace-id");
```



## トレースセッションを終了する

トレースセッションを停止するには、`trace.leave()`を呼び出します。これにより、将来のイベントからトレースIDが削除されます。



```kotlin
tealium.trace.leave()
    .subscribe { result ->
        // 必要に応じてここで結果を処理します
    }
```


```swift
tealium.trace.leave().subscribe { result in
    // 必要に応じてここで結果を処理します
}
```


```javascript
await tealium.trace.leave();
```



## 訪問の強制終了

AudienceStreamで「訪問の終了」アクションをテストするために、セッションが期限切れになるのを待たずに、セッションを直ちに終了させます：



```kotlin
tealium.trace.forceEndOfVisit()
    .subscribe { result ->
        // トラック結果を処理します
    }
```


```swift
tealium.trace.forceEndOfVisit().subscribe { result in
    // トラック結果を処理します
}
```


```javascript
await tealium.trace.forceEndOfVisit();
```



トレースは`leave()`が呼ばれるまでアクティブのままです。`forceEndOfVisit()`メソッドは、セッションを終了するトラックコールをディスパッチし、標準のデキュー処理に従います。

## エラートラッキング

エラートラッキングが有効になっている場合（`track_errors: true`）、トレースモジュールはアクティブなトレースセッション中に発生したSDKエラーを自動的に追跡します。重複するエラーレポートを防ぐために、モジュールはカテゴリ別にエラーを重複排除します：

* 各カテゴリからの最初のエラーのみがトレースセッションごとに追跡されます
* 同じカテゴリからの後続のエラーは、新しいトレースセッションが始まるまで無視されます
* 新しいトレースセッションに参加するか、現在のセッションを離れると、重複排除キャッシュがリセットされます

## QRトレース

ディープリンクから直接トレースを開始することもできます。開かれたURLに適切なクエリパラメータが含まれている場合、トレースは自動的に開始されます。これは通常、TealiumプラットフォームのQRトレースツールで行われます。詳細は、[トレースでデバッグ](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/)を参照してください。

## APIリファレンス

詳細なクラスとメソッドの署名については、APIリファレンスドキュメントを参照してください：

* [Trace (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)
* [TraceSettingsBuilder (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/TraceSettingsBuilder.html)
* [Trace (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)
* [Trace (React Native)](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html)