---
title: バリア
description: Tealium Prism SDKで、バリアとディスパッチャーごとのバリア構成を使用してイベント配信を制御します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/barriers/
---
バリアは、Tealium Prism SDKでディスパッチがディスパッチャーに送信されるタイミングを制御します。バリアはゲートとして機能し、ネットワーク接続、バッチサイズの要件、カスタムビジネスロジックなどの条件に基づいて、イベントのフローをブロックまたは許可します。

## 仕組み

バリアは、イベントディスパッチパイプライン内のゲートです。SDKがイベントをディスパッチャーに送信する前に、構成された各バリアがディスパッチを続行するかどうかを確認します。バリアが閉じている場合、イベントはバリアが開くまでキューに格納されます。

各バリアは、**開いている**（ディスパッチを続行）または**閉じている**（ディスパッチをキューに格納）のいずれかの状態になります。

バリアのスコープによって、適用対象のディスパッチャーが決まります。すべてのディスパッチャー、またはIDで指定した特定のディスパッチャーのいずれかです。

バリアはフラッシュ可能として指定できます。これは、イベントキューを手動でフラッシュしたときに、そのバリアがバイパスされることを意味します。


<blockquote>
フラッシュ不可のバリアが1つでも閉じている場合、フラッシュ可能なバリアの状態にかかわらず、ディスパッチは続行されません。
</blockquote>


## UIでバリアを構成する

アプリのコードを変更せずに、モバイルプロファイルでバリアを構成できます。

UIでバリアを追加するには、次の手順を実行します。

1. モバイルプロファイルにログインし、**Barriers**に移動します。
1. **Add Barrier**を選択し、バリアタイプを選択します。
1. バリア構成を構成します。
1. 変更を保存して公開します。

SDKは、次回のリモート構成の更新時またはアプリの起動時に、更新されたバリア構成を取得します。

## 組み込みバリア

SDKには、接続バリアとバッチ処理バリアという2つの組み込みバリアがあります。デフォルトでは、接続バリアのスコープはCollectディスパッチャーに構成され、バッチ処理バリアは無効になっています。

### 接続バリア

接続バリアは、ネットワーク接続を利用できない場合や、接続が指定された要件を満たしていない場合にディスパッチをブロックします。

動作：

* ネットワーク接続を利用できない場合、ディスパッチをブロックします。
* `wifi_only`が有効な場合、必要に応じてモバイル回線接続をブロックします。
* いずれかのネットワーク接続を利用できる場合は、フラッシュ可能です。
* 接続が復旧すると自動的に開きます。

### バッチ処理バリア

バッチ処理バリアは、ディスパッチャーのキューに指定された数のイベントが格納されるまで、ディスパッチをブロックします。

動作：

* キューサイズが構成されたバッチサイズに達するまで、ディスパッチをブロックします。
* 構成値が`Dispatcher.dispatchLimit`を超える場合、バッチサイズとして`Dispatcher.dispatchLimit`を使用します。
* 構成値が負の値またはゼロの場合、バッチサイズとして1を使用します。
* フラッシュ操作中は常にフラッシュ可能です。

## 高度な構成

構成が実行時の条件に依存する場合や、リモートから変更されないように固定する必要がある場合は、プログラムでバリアを構成します。たとえば、ディスク容量が少ないデバイスではバッチ処理バリアのキューサイズを小さくしたり、本番ビルドではWi-Fi接続のみでディスパッチするよう強制したりできます。これにより、リモート構成の変更によって予期しないデータ使用量が発生するのを防止できます。

### プログラムによる構成


<blockquote>
React Nativeでは、プログラムによるバリア構成を利用できません。Tealiumモバイルプロファイルまたは構成JSONでバリアを構成してください。
</blockquote>


#### 接続バリア

構成オプション：

* `wifi_only`：`true`の場合、Wi-FiまたはEthernet接続経由のディスパッチのみを許可します。



```kotlin
// WiFi-only, scoped to the Collect dispatcher
config.addBarrier(
    Barriers.connectivity {
        it.setScope(BarrierScope.Dispatchers(Modules.Types.COLLECT))
            .setWifiOnly(true)
    }
)

// Allow any network connection, scoped to all dispatchers
config.addBarrier(
    Barriers.connectivity { it.setScope(BarrierScope.All) }
)
```


```swift
// WiFi-only, scoped to the Collect dispatcher
config.addBarrier(
    Barriers.connectivity(forcingSettings: { enforcedSettings in
        enforcedSettings.setScope(.dispatchers([Modules.Types.collect]))
            .setWifiOnly(true)
    })
)

// Allow any network connection, scoped to all dispatchers
config.addBarrier(
    Barriers.connectivity(forcingSettings: { $0.setScope(.all) })
)
```



#### バッチ処理バリア

構成オプション：

* `batch_size`：バリアが開くために必要な、キューに格納されたイベントの数。




```kotlin
// Batch 10 events before dispatching, scoped to all dispatchers
config.addBarrier(
    Barriers.batching {
        it.setScope(BarrierScope.All)
            .setBatchSize(10)
    }
)

// Use default batch size, scoped to the Collect dispatcher
config.addBarrier(Barriers.batching())
```


```swift
// Batch 10 events before dispatching, scoped to all dispatchers
config.addBarrier(
    Barriers.batching(forcingSettings: { enforcedSettings in
        enforcedSettings.setScope(.all)
            .setBatchSize(10)
    })
)

// Use default batch size, scoped to the Collect dispatcher
config.addBarrier(Barriers.batching())
```



### JSON構成

バリア構成は、リモート構成またはローカルJSONファイルを通じて処理されます。バリアは、ファクトリによって作成されるときに構成を受け取ります。

```json
{
  "barriers": {
    "ConnectivityBarrier": {
      "barrier_id": "ConnectivityBarrier",
      "scope": "all",
      "configuration": {
        "wifi_only": true
      }
    },
    "BatchingBarrier": {
      "barrier_id": "BatchingBarrier",
      "scope": ["analytics_dispatcher", "Collect"],
      "configuration": {
        "batch_size": 10
      }
    }
  }
}
```

構成が変更されると、バリアは自動的に`updateConfiguration()`の呼び出しを受け取ります。

## カスタムバリアを作成する

### 構成可能なバリア

リモート構成またはローカル構成を通じて構成できるバリアを作成します。




```kotlin
class CustomBusinessLogicBarrier(configuration: DataObject) : ConfigurableBarrier {
    companion object {
        const val ID = "CustomBusinessLogicBarrier"
    }

    override val id: String = ID

    private var settings = BusinessLogicSettings(configuration)
    private val stateSubject = Observables.stateSubject(BarrierState.Open)

    override fun onState(dispatcherId: String): Observable<BarrierState> = stateSubject

    override fun updateConfiguration(configuration: DataObject) {
        settings = BusinessLogicSettings(configuration)
        updateBarrierState()
    }

    override val isFlushable: Observable<Boolean> = Observables.just(false)

    private fun updateBarrierState() {
        val shouldBlock = settings.maintenanceMode
        stateSubject.onNext(if (shouldBlock) BarrierState.Closed else BarrierState.Open)
    }
}
```


```swift
class CustomBusinessLogicBarrier: ConfigurableBarrier {
    static let id: String = "CustomBusinessLogicBarrier"

    @StateSubject(.open)
    private var state: ObservableState<BarrierState>

    private var settings: BusinessLogicSettings

    init(configuration: DataObject) {
        self.settings = BusinessLogicSettings(dataObject: configuration)
        updateBarrierState()
    }

    func onState(for dispatcherId: String) -> Observable<BarrierState> {
        state
    }

    func updateConfiguration(_ configuration: DataObject) {
        settings = BusinessLogicSettings(dataObject: configuration)
        updateBarrierState()
    }

    var isFlushable: Observable<Bool> {
        Observables.just(false)
    }

    private func updateBarrierState() {
        let shouldBlock = settings.maintenanceMode
        _state.value = shouldBlock ? .closed : .open
    }
}
```


### バリアの登録

SDK の初期化時にカスタムバリアを登録します。




```kotlin
config.addBarrier(
    CustomBusinessLogicBarrier.Factory(defaultScope = BarrierScope.All)
)
```


```swift
config.addBarrier(
    CustomBusinessLogicBarrier.Factory(defaultScope: .all)
)
```



### 実行時のバリア管理

モジュール実装で実行時にバリアを登録する必要がある場合は、`BarrierRegistrar` を使用します。

```swift
// Get the barrier registrar from TealiumContext
let barrierRegistrar = context.barrierRegistrar

// Create and register a custom barrier
let customBarrier = CustomTimerBarrier(interval: 30.0)
barrierRegistrar.registerScopedBarrier(
    customBarrier,
    scope: .dispatchers(["my_dispatcher"])
)

// Unregister when no longer needed
barrierRegistrar.unregisterScopedBarrier(customBarrier)
```

## API リファレンス

クラスおよびメソッドの詳しいシグネチャについては、API リファレンスドキュメントを参照してください。

* [バリア（Swift）](https://docs.tealium.com/tealium-prism-swift/Barriers.html)
* [Barrier（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Barrier.html)
* [ConfigurableBarrier（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/ConfigurableBarrier.html)
* [バリア（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/)