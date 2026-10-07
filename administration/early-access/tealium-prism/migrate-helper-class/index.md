---
title: Migrate your helper class from the legacy SDK to Tealium Prism
description: Change the TealiumHelper class in your iOS or Android app to route events through Tealium Prism instead of Tealium for Swift or Tealium for Android (Kotlin).
url: https://docs.tealium.com/administration/early-access/tealium-prism/migrate-helper-class/
---
## Who this is for

You have an app on Tealium for Swift 2.x or Tealium for Android (Kotlin) 1.x, and a `TealiumHelper` class that wraps the SDK. This page shows the Prism call that replaces each legacy call. It does not cover moving stored data between the SDKs.

## Before you start

### Requirements

* Prism requires iOS 13 or Android API 23.
* Prism is Swift and Kotlin only. Java apps call the Kotlin API. Objective-C is not supported.

### Stored data

Stored data does not move. After the upgrade the user gets a new visitor ID, an empty persistent data layer and reset lifecycle counters. Keep the same account and profile. A data migration is planned for a later release.

### Dispatchers and modules

Prism does not include the Tag Management (webview) dispatcher, remote commands, the built-in consent manager, timed events, or the following modules:
  * Ad Identifier
  * Attribution
  * AutoTracking
  * Crash Reporter
  * Hosted Data Layer
  * In-App Purchase
  * Install Referrer
  * Location
  * Media
  * Visitor Service

### Dependencies

Update your dependencies before importing Prism:

* **iOS**  
Replace `TealiumSwift` with `TealiumPrism` (CocoaPods) or `TealiumPrismCore` and `TealiumPrismLifecycle` (Swift Package Manager).
* **Android**  
Replace `com.tealium:kotlin-core` with the `com.tealium.prism:prism-bom` BOM and `prism-core`, `prism-lifecycle`.

## Initialize

Legacy has two lists, collectors and dispatchers. Prism has one list of modules, plus a local settings file, a remote settings URL, and a block of programmatic settings.



```swift
// Legacy
let config = TealiumConfig(account: "ACCOUNT", profile: "PROFILE",
                           environment: "prod", dataSource: "DATASOURCE")
config.collectors = [Collectors.AppData, Collectors.Lifecycle]
config.dispatchers = [Dispatchers.Collect, Dispatchers.TagManagement]
tealium = Tealium(config: config) { _ in }

// Prism
let config = TealiumConfig(
    account: "ACCOUNT", profile: "PROFILE", environment: "prod",
    dataSource: "DATASOURCE",
    modules: [Modules.appData(), Modules.lifecycle(), Modules.collect()],
    settingsFile: "TealiumSettings",
    settingsUrl: "https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/prod/mobile_settings.json",
    forcingSettings: { $0.setMinLogLevel(.info) })
tealium = Tealium.create(config: config) { result in
    // Result<Tealium, Error>
}
```


```kotlin
// Legacy
val config = TealiumConfig(application, "ACCOUNT", "PROFILE", Environment.PROD,
    dataSourceId = "DATASOURCE",
    collectors = mutableSetOf(Collectors.App, Collectors.Device),
    dispatchers = mutableSetOf(Dispatchers.Collect, Dispatchers.TagManagement),
    modules = mutableSetOf(Modules.Lifecycle))
Tealium.create("main", config) { }

// Prism
val config = TealiumConfig.Builder(application, "ACCOUNT", "PROFILE", Environment.PROD,
        listOf(Modules.appData(), Modules.deviceData(), Modules.lifecycle(), Modules.collect()))
    .setDataSource("DATASOURCE")
    .setSettingsFile("tealium-settings.json")
    .setSettingsUrl("https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/prod/mobile_settings.json")
    .configureCoreSettings { it.setLogLevel(LogLevel.INFO) }
    .build()
tealium = Tealium.create(config) { result -> /* TealiumResult<Tealium> */ }
```



Prism keys instances by `ACCOUNT-PROFILE`. `Tealium["main"]` becomes the asynchronous `Tealium.get("ACCOUNT-PROFILE") { }` on Android and `TealiumInstanceManager.get(_:completion:)` on iOS. Most helpers keep their own reference.

## Track an event or a view

Prism has one `track` method. The view or event type is a parameter, and data is a `DataObject`.



```swift
// Legacy
tealium.track(TealiumEvent("purchase", dataLayer: ["order_id": "123"]))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", data: ["order_id": "123"])
tealium.track("home", type: .view)
```
<!-- TODO verify: does DataObject conform to ExpressibleByDictionaryLiteral, or must the sample use a DataObject builder? Signature confirmed: track(_ name: String, type: DispatchType = .event, data: DataObject? = nil). -->


```kotlin
// Legacy
tealium.track(TealiumEvent("purchase", mapOf("order_id" to "123")))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", DataObject.create { put("order_id", "123") })
tealium.track("home", DispatchType.View, DataObject.EMPTY_OBJECT)
```



## Data layer

`add` becomes `put`, `delete` becomes `remove`, and reads are asynchronous. Expiry names are unchanged, except that Swift `.afterCustom` is gone. Use `.after(Date)` instead.



```swift
// Legacy
tealium.dataLayer.add(key: "user_tier", value: "gold", expiry: .forever)
tealium.dataLayer.delete(for: "user_tier")
let tier = tealium.dataLayer.all["user_tier"]

// Prism
tealium.dataLayer.put(key: "user_tier", value: "gold", expiry: .forever)
tealium.dataLayer.remove(key: "user_tier")
tealium.dataLayer.get(key: "user_tier", as: String.self).subscribe { result in
    // Result<String?, ModuleError<Error>>
}
```


```kotlin
// Legacy
tealium.dataLayer.putString("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
val tier = tealium.dataLayer.getString("user_tier")

// Prism
tealium.dataLayer.put("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
tealium.dataLayer.getString("user_tier").subscribe { result -> /* TealiumResult<String?> */ }
```



To write multiple values in one transaction, use `dataLayer.transactionally { }` on both platforms.

## Consent

Prism has no consent status or categories of its own. Your consent management platform (CMP) is the source of truth. You implement a small adapter that publishes the user's decision as a set of purposes, and map each purpose to the dispatchers it releases.



```swift
// Legacy
config.consentPolicy = .gdpr
tealium.consentManager?.userConsentStatus = .consented
tealium.consentManager?.userConsentCategories = [.analytics]

// Prism
final class MyCMPAdapter: CMPAdapter {
    let id = "my_cmp"
    let allPurposes: Set<String>? = ["analytics", "marketing"]
    let consentDecision: Observable<ConsentDecision?>   // emit on every user decision
    // TODO verify: how a customer constructs the Observable (Subject type name).
}
config.enableConsentIntegration(with: MyCMPAdapter(), forcingConfiguration: {
    $0.addPurpose("analytics", dispatcherIds: ["Collect"])
})
```


```kotlin
// Legacy
config.consentManagerPolicy = ConsentPolicy.GDPR
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED

// Prism
class MyCmpAdapter : CmpAdapter {
    override val id = "my_cmp"
    override val allPurposes: Set<String>? = setOf("analytics", "marketing")
    override val consentDecision: Observable<ConsentDecision?> = TODO()
}
TealiumConfig.Builder(https://docs.tealium.com/* ... */)
    .enableConsentIntegration(MyCmpAdapter()) { it.addPurpose("analytics", listOf("Collect")) }
```



<!-- TODO verify: ConsentDecision.DecisionType case names. Also verify addPurpose parameter types on Kotlin ConsentConfigurationBuilder. Consent surface is the least stable API at 0.6.0 (MT-2080 replay fix open). -->

## Visitor ID



```swift
// Legacy
let id = tealium.visitorId
tealium.resetVisitorId()
config.visitorIdentityKey = "customer_id"

// Prism
tealium.resetVisitorId()          // returns the new ID in a result
tealium.clearStoredVisitorIds()
// identity switching: forcingSettings: { $0.setVisitorIdentityKey("customer_id") }
```


```kotlin
// Legacy
val id = tealium.visitorId
tealium.resetVisitorId()
config.visitorIdentityKey = "customer_id"

// Prism
tealium.resetVisitorId()          // SingleResult<String>
tealium.clearStoredVisitorIds()
// identity switching: .configureCoreSettings { it.setVisitorIdentityKey("customer_id") }
```



Prism 0.6.0 has no method to read the current visitor ID. The ID is sent on every event as `tealium_visitor_id`.

## Remote commands become dispatchers

In Prism, each vendor is a dispatcher module with the same role and lifecycle as Collect: native, queued on disk, gated by consent and barriers, configured from the settings file. Use a published dispatcher where one exists (Firebase for iOS today), or write one.



```swift
// Legacy
let firebase = RemoteCommand(commandId: "firebase", description: "Firebase", type: .webview) { response in
    // call the Firebase SDK with response.payload
}
config.addRemoteCommand(firebase)

// Prism: implement Dispatcher, register its ModuleFactory in `modules`
final class MyDispatcher: Dispatcher {
    let id = "my_vendor"
    let version = "1.0.0"
    func dispatch(_ data: [Dispatch], completion: @escaping ([Dispatch]) -> Void) -> any Disposable {
        // send each dispatch payload to the vendor SDK; complete with the dispatches that succeeded
    }
    func updateConfiguration(_ configuration: DataObject) -> Self? { self }
    func shutdown() {}
}
```


```kotlin
// Legacy
tealium.remoteCommands?.add(FirebaseRemoteCommand(application))

// Prism: extend CommandDispatcher with named commands, register its ModuleFactory in `modules`
val commands = listOf(Command.synchronous("log_event") { payload -> /* vendor SDK call */ })
```



<!-- TODO verify: Firebase dispatcher factory name for the iOS module (separate repo tealium-prism-ios-firebase-dispatcher). Also verify full CommandDispatcher constructor for Kotlin (id, version, commands, logger, logCategory, scheduler) and the ModuleFactory boilerplate. Link to the Modules page once merged. -->

## Logging



```swift
// Legacy
config.logLevel = .info            // info, debug, error, fault, silent

// Prism
forcingSettings: { $0.setMinLogLevel(.debug) }   // trace, debug, info, warn, error, silent
config.loggerType = .custom(myLogHandler)        // optional
```


```kotlin
// Legacy
config.logLevel = LogLevel.DEV     // DEV, QA, PROD, SILENT

// Prism
.configureCoreSettings { it.setLogLevel(LogLevel.DEBUG) }  // TRACE, DEBUG, INFO, WARN, ERROR, SILENT
.setLogHandler(myLogHandler)                                // optional
```



The level can also be set remotely with the `log_level` key under `core` in `mobile_settings.json`, and a programmatic value takes precedence.

## Teardown



```swift
// Legacy
tealium.disable()

// Prism
tealium.shutdown()   // later calls fail with TealiumError.instanceShutdown
```


```kotlin
// Legacy
Tealium.destroy("main")

// Prism
tealium.shutdown()   // or Tealium.shutdown("ACCOUNT-PROFILE")
```



Before calling `shutdown()`, dispose any subscriptions you hold.

## Behavior differences

| Area | Legacy | Prism |
|---|---|---|
| Queueing | One queue. Batching and offline are handled per config flag. | One SQLite queue per dispatcher. Every event is written before send and removed after a confirmed send. Barriers (connectivity, batching) release the queue. `flushEventQueue()` forces it. |
| Consent | SDK stores status and categories. Events queue until consented. | SDK stores nothing. Your CMP adapter publishes purposes. Each purpose releases named dispatchers. Held events refire for the dispatchers you list. |
| Settings | Programmatic config plus `mobile.json` from Tealium iQ | Local file < remote URL (cached for offline) < programmatic. Programmatic values can never be overridden remotely. A module only starts when settings exist for it. |
| Tag logic | utag.js in a webview | Transformers on device: set values, lowercase, persist, JavaScript in an isolated runtime. No webview. |
| Threading and results | Mixed. Some sync reads. Fire and forget. | All public calls are safe from any thread and run on one SDK queue. Every write or read returns a `SingleResult` or `Single`. Subscribe to see errors, or ignore it. Completions run on the SDK queue, not yours. |
| Stored data | Persists across SDK upgrades | Not carried over from legacy at 0.6.0 |

## Checklist

1. Bump the deployment target to iOS 13 or API 23.
1. Swap the dependency and the `import`.
1. Replace the two collector and dispatcher lists with one `modules` list. Drop Tag Management and Remote Commands.
1. Add `settingsFile` or `settingsUrl`. Move per-module options into the settings file or `forcingSettings` / `configureCoreSettings`.
1. Replace `Tealium(config:)` or `Tealium.create(name, config)` with `Tealium.create(config)`.
1. Replace `TealiumEvent` / `TealiumView` with `track(name, type:, data:)`.
1. Rename `add` to `put` and `delete` to `remove`.
1. Make reads asynchronous.
1. Replace the consent manager with a CMP adapter and purpose mapping.
1. Replace each remote command with a dispatcher module.
1. Move log level into settings.
1. Replace `disable()` and `destroy()` with `shutdown()`.
1. Test on a fresh install and on an upgrade from the legacy app.
1. Expect a new visitor ID on upgrade.

## Where to get help

For questions about the migration timeline, [contact support](https://docs.tealium.com/support/). Report SDK defects on [tealium-prism-swift](https://github.com/tealium/tealium-prism-swift/issues) and [tealium-prism-kotlin](https://github.com/tealium/tealium-prism-kotlin/issues).
