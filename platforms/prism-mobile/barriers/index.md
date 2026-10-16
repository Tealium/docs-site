---
title: Barriers
description: Control event delivery with barriers and per-dispatcher barrier configuration in the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/barriers/
---
Barriers control when dispatches are sent to dispatchers in the Tealium Prism SDK. They act as gates that block or allow the flow of events based on conditions such as network connectivity, batch size requirements, or custom business logic.

## How it works

Barriers are gates in the event dispatch pipeline. Before the SDK sends an event to a dispatcher, each configured barrier checks whether the dispatch should proceed. If a barrier is closed, the event queues until the barrier opens.

Each barrier is either **open** (the dispatch proceeds) or **closed** (the dispatch queues).

A barrier's scope determines which dispatchers it applies to: either all dispatchers or a specific one by ID.

Barriers can be marked as flushable, meaning they are bypassed when the event queue is flushed manually.


<blockquote>
If any non-flushable barriers are closed, the dispatch does not proceed regardless of the flushable barriers' states.
</blockquote>


## Configure barriers in the UI

Configure barriers in your mobile profile without changing your app code.

To add a barrier in the UI:

1. Log in to your mobile profile and go to **Barriers**.
1. Select **Add Barrier** and choose a barrier type.
1. Configure the barrier settings.
1. Save and publish your changes.

The SDK picks up the updated barrier configuration on the next remote settings refresh or app startup.

## Built-in barriers

The SDK provides two built-in barriers: the connectivity barrier and the batching barrier. By default, the connectivity barrier is scoped to the Collect dispatcher, and the batching barrier is deactivated.

### Connectivity barrier

The connectivity barrier blocks dispatches when network connectivity is unavailable or does not meet specified requirements.

Behavior:

* Blocks dispatches when no network connection is available.
* Optionally blocks cellular connections when `wifi_only` is enabled.
* Is flushable when any network connection is available.
* Automatically opens when connectivity is restored.

### Batching barrier

The batching barrier blocks dispatches until a specified number of events have been queued for a dispatcher.

Behavior:

* Blocks dispatches until queue size reaches the configured batch size.
* Uses `Dispatcher.dispatchLimit` as batch size if the configured value exceeds it.
* Uses batch size of 1 if the configured value is negative or zero.
* Always flushable during flush operations.

## Advanced

Configure barriers programmatically when the configuration depends on runtime conditions or must be locked against remote changes. For example, you might reduce the batching barrier's queue size on devices with low disk space, or enforce wifi-only dispatch in a production build to prevent unexpected data usage that a remote settings change could otherwise introduce.

### Programmatic configuration


<blockquote>
Programmatic barrier configuration is not available in React Native. Configure barriers in your Tealium mobile profile or settings JSON.
</blockquote>


#### Connectivity barrier

Configuration options:

* `wifi_only`: When `true`, only allows dispatches over WiFi or Ethernet connections.



```kotlin
// WiFi-only, scoped to the Collect dispatcher
config.addBarrier(
    Barriers.connectivity(
        defaultScopes = listOf(BarrierScope.dispatcher("collect_dispatcher")),
        configuration = mapOf("wifi_only" to true)
    )
)

// Allow any network connection, scoped to all dispatchers
config.addBarrier(
    Barriers.connectivity(defaultScopes = listOf(BarrierScope.ALL))
)
```


```swift
// WiFi-only, scoped to the Collect dispatcher
config.addBarrier(
    Barriers.connectivity(
        defaultScopes: [.dispatcher(id: Modules.Types.collect)],
        configuration: ["wifi_only": true]
    )
)

// Allow any network connection, scoped to all dispatchers
config.addBarrier(
    Barriers.connectivity(defaultScopes: [.all])
)
```



#### Batching barrier

Configuration options:

* `batch_size`: Number of queued events required before opening the barrier.




```kotlin
// Batch 10 events before dispatching, scoped to all dispatchers
config.addBarrier(
    Barriers.batching(
        defaultScopes = listOf(BarrierScope.ALL),
        configuration = mapOf("batch_size" to 10)
    )
)

// Use default batch size, scoped to the Collect dispatcher
config.addBarrier(Barriers.batching())
```


```swift
// Batch 10 events before dispatching, scoped to all dispatchers
config.addBarrier(
    Barriers.batching(
        defaultScopes: [.all],
        configuration: ["batch_size": 10]
    )
)

// Use default batch size, scoped to the Collect dispatcher
config.addBarrier(Barriers.batching())
```



### JSON configuration

Barrier configuration is handled through remote settings or local JSON files. The barrier receives its configuration when created by the factory.

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

Barriers automatically receive `updateConfiguration()` calls when settings change.

## Create custom barriers

### Configurable barrier

Create a barrier that can be configured through remote or local settings:




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



### Register a barrier

Register your custom barrier during SDK initialization:




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



### Runtime barrier management

If your module implementation needs to register barriers at runtime, use the `BarrierRegistrar`:

```swift
// Get the barrier registrar from TealiumContext
let barrierRegistrar = context.barrierRegistrar

// Create and register a custom barrier
let customBarrier = CustomTimerBarrier(interval: 30.0)
barrierRegistrar.registerScopedBarrier(
    customBarrier,
    scopes: [.dispatcher(id: "my_dispatcher")]
)

// Unregister when no longer needed
barrierRegistrar.unregisterScopedBarrier(customBarrier)
```

## API reference

For detailed class and method signatures, see the API reference documentation:

* [Barriers (Swift)](https://docs.tealium.com/tealium-prism-swift/Barriers.html)
* [Barrier (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Barrier.html)
* [ConfigurableBarrier (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/ConfigurableBarrier.html)
* [Barriers (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)
