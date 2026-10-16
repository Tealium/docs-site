---
title: バリア
description: Tealium Prism SDKでのイベント配信制御とディスパッチャーごとのバリア構成について。
url: https://docs.tealium.com/ja/platforms/prism-mobile/barriers/
---
バリアはTealium Prism SDK内でディスパッチャーへのディスパッチが送信されるタイミングを制御します。これらは、ネットワーク接続、バッチサイズ要件、またはカスタムビジネスロジックなどの条件に基づいてイベントの流れをブロックまたは許可するゲートとして機能します。

## 動作原理

バリアはイベントディスパッチパイプライン内のゲートです。SDKがイベントをディスパッチャーに送信する前に、構成された各バリアがディスパッチを進行させるかどうかをチェックします。バリアが閉じている場合、イベントはバリアが開くまでキューに入れられます。

各バリアは、**開いている**（ディスパッチが進行する）か**閉じている**（ディスパッチがキューに入る）のどちらかです。

バリアの範囲は、それが適用されるディスパッチャーを決定します：すべてのディスパッチャーまたはIDによる特定のディスパッチャー。

バリアはフラッシュ可能とマークされることがあり、これはイベントキューが手動でフラッシュされるときにバイパスされることを意味します。


<blockquote>
フラッシュ不可能なバリアが閉じている場合、フラッシュ可能なバリアの状態に関わらずディスパッチは進行しません。
</blockquote>


## UIでのバリアの構成

アプリコードを変更することなく、モバイルプロファイルでバリアを構成します。

UIでバリアを追加するには：

1. モバイルプロファイルにログインし、**バリア**に移動します。
1. **バリア追加**を選択し、バリアタイプを選びます。
1. バリア構成を構成します。
1. 変更を保存して公開します。

SDKは次のリモート構成のリフレッシュまたはアプリの起動時に更新されたバリア構成を取得します。

## 組み込みのバリア

SDKには、接続バリアとバッチングバリアの2つの組み込みバリアが提供されています。デフォルトでは、接続バリアはCollectディスパッチャーに適用され、バッチングバリアは無効化されています。

### 接続バリア

接続バリアは、ネットワーク接続が利用不可能または指定された要件を満たしていない場合にディスパッチをブロックします。

動作：

* ネットワーク接続が利用不可能な場合にディスパッチをブロックします。
* `wifi_only`が有効になっている場合、セルラー接続をオプションでブロックします。
* 任意のネットワーク接続が利用可能な場合はフラッシュ可能です。
* 接続が復旧すると自動的に開きます。

### バッチングバリア

バッチングバリアは、ディスパッチャーにキューされたイベントの指定された数に達するまでディスパッチをブロックします。

動作：

* キューサイズが構成されたバッチサイズに達するまでディスパッチをブロックします。
* 構成された値が`Dispatcher.dispatchLimit`を超える場合は、バッチサイズとして`Dispatcher.dispatchLimit`を使用します。
* 構成された値が負またはゼロの場合は、バッチサイズを1として使用します。
* フラッシュ操作中は常にフラッシュ可能です。

## 高度な構成

実行時の条件に依存する構成が必要な場合や、リモート変更に対してロックをかける必要がある場合には、プログラムでバリアを構成します。たとえば、ディスクスペースが少ないデバイスでバッチングバリアのキューサイズを減らすか、予期しないデータ使用を防ぐために本番ビルドでwifiのみのディスパッチを強制することが考えられます。

### プログラムによる構成


<blockquote>
プログラムによるバリア構成はReact Nativeでは利用できません。Tealiumのモバイルプロファイルまたは構成JSONでバリアを構成してください。
</blockquote>


#### 接続バリア

構成オプション：

* `wifi_only`: `true`の場合、WiFiまたはEthernet接続でのみディスパッチを許可します。



```kotlin
// WiFiのみ、Collectディスパッチャーに適用
config.addBarrier(
    Barriers.connectivity(
        defaultScopes = listOf(BarrierScope.dispatcher("collect_dispatcher")),
        configuration = mapOf("wifi_only" to true)
    )
)

// すべてのネットワーク接続を許可、すべてのディスパッチャーに適用
config.addBarrier(
    Barriers.connectivity(defaultScopes = listOf(BarrierScope.ALL))
)
```


```swift
// WiFiのみ、Collectディスパッチャーに適用
config.addBarrier(
    Barriers.connectivity(
        defaultScopes: [.dispatcher(id: Modules.Types.collect)],
        configuration: ["wifi_only": true]
    )
)

// すべてのネットワーク接続を許可、すべてのディスパッチャーに適用
config.addBarrier(
    Barriers.connectivity(defaultScopes: [.all])
)
```



#### バッチングバリア

構成オプション：

* `batch_size`: バリアを開く前に必要なキューイベントの数。



```kotlin
// 10イベントをバッチ処理する前にディスパッチ、すべてのディスパッチャーに適用
config.addBarrier(
    Barriers.batching(
        defaultScopes = listOf(BarrierScope.ALL),
        configuration = mapOf("batch_size" to 10)
    )
)

// デフォルトのバッチサイズを使用、Collectディスパッチャーに適用
config.addBarrier(Barriers.batching())
```


```swift
// 10イベントをバッチ処理する前にディスパッチ、すべてのディスパッチャーに適用
config.addBarrier(
    Barriers.batching(
        defaultScopes: [.all],
        configuration: ["batch_size": 10]
    )
)

// デフォルトのバッチサイズを使用、Collectディスパッチャーに適用
config.addBarrier(Barriers.batching())
```



### JSON構成

バリア構成はリモート構成またはローカルJSONファイルを通じて処理されます。バリアはファクトリによって作成されたときにその構成を受け取ります。

```json
{
  "barriers": {
    "ConnectivityBarrier": {
      "barrier_id": "ConnectivityBarrier",
      "scopes": ["all"],
      "configuration": {
        "wifi_only": true
      }
    },
    "BatchingBarrier": {
      "barrier_id": "BatchingBarrier",
      "scopes": ["analytics_dispatcher", "collect_dispatcher"],
      "configuration": {
        "batch_size": 10
      }
    }
  }
}
```

構成が変更されると、バリアは自動的に`updateConfiguration()`コールを受け取ります。

## カスタムバリアの作成

### 構成可能なバリア

リモートまたはローカルの構成を通じて構成可能なバリアを作成します：



```kotlin
class CustomBusinessLogicBarrier(configuration: DataObject) : ConfigurableBarrier {
    companion object {
        const val ID = "CustomBusinessLogicBarrier"
    }

    private var settings = BusinessLogicSettings(configuration)
    private val stateSubject = StateSubject(BarrierState.OPEN)

    override fun onState(dispatcherId: String): Observable<BarrierState> = stateSubject

    override fun updateConfiguration(configuration: DataObject) {
        settings = BusinessLogicSettings(configuration)
        updateBarrierState()
    }

    override val isFlushable: Observable<Boolean> = Observables.just(false)

    private fun updateBarrierState() {
        val shouldBlock = settings.maintenanceMode
        stateSubject.value = if (shouldBlock) BarrierState.CLOSED else BarrierState.OPEN
    }
}
```


```swift
class CustomBusinessLogicBarrier: ConfigurableBarrier {
    static var id: String = "CustomBusinessLogicBarrier"

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

SDKの初期化中にカスタムバリアを登録します：



```kotlin
config.addBarrier(
    CustomBusinessLogicBarrier.Factory(defaultScopes = listOf(BarrierScope.ALL))
)
```


```swift
config.addBarrier(
    CustomBusinessLogicBarrier.Factory(defaultScopes: [.all])
)
```


### ランタイムバリア管理

モジュール実装でランタイムでバリアを登録する必要がある場合は、`BarrierRegistrar`を使用してください：

```swift
// TealiumContextからバリアレジストラーを取得
let barrierRegistrar = context.barrierRegistrar

// カスタムバリアを作成して登録
let customBarrier = CustomTimerBarrier(interval: 30.0)
barrierRegistrar.registerScopedBarrier(
    customBarrier,
    scopes: [.dispatcher(id: "my_dispatcher")]
)

// 不要になったら登録解除
barrierRegistrar.unregisterScopedBarrier(customBarrier)
```

## APIリファレンス

詳細なクラスとメソッドのシグネチャについては、APIリファレンスドキュメントを参照してください：

* [バリア (Swift)](https://docs.tealium.com/tealium-prism-swift/Barriers.html)
* [バリア (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Barrier.html)
* [構成可能バリア (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/ConfigurableBarrier.html)
* [バリア (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)