---
title: Visitor ID Manager module
description: Create, store, and switch the anonymous visitor ID in mobile apps with the Visitor ID Manager module.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/visitor-id-manager/
---
The Visitor ID Manager module is a collector that owns the anonymous visitor ID for a device. The module creates and stores the visitor ID, adds it to every tracking event, and switches it when the user identity in the data layer changes. The module is enabled by default and added automatically, so it works without configuration.

To read and manage the visitor ID in your app, use `tealium.visitorId`, which returns a `VisitorIdManager`.

## Collected data

| Data point | Key | Description |
| :--- | :--- | :--- |
| Visitor ID | `tealium_visitor_id` | The anonymous visitor ID for the device. |

## Configuration

| Setting | JSON key | Description | Default value |
| :--- | :--- | :--- | :--- |
| Visitor identity key | `visitor_identity_key` | The data layer key that holds the identity of the current user, such as an email address or user ID. Set this key to turn on [visitor switching](#visitor-switching). | None (visitor switching is off) |

The module also supports the common `enabled`, `order`, and `rules` module settings. For more information about rules, see [Rules](https://docs.tealium.com/rules/).

Configure the module using JSON settings files, programmatically, or a combination of both.

### JSON settings

To use a local settings file, pass the filename to `settingsFile` in `TealiumConfig`. To use remote settings, pass a URL to `settingsUrl`. When you use both, the SDK merges them and remote settings take priority.

```json
{
    "modules": {
        "VisitorId": {
            "module_type": "VisitorId",
            "enabled": true,
            "order": 1,
            "rules": {
                "operator": "and",
                "children": [
                    "rule_id_from_settings"
                ]
            },
            "configuration": {
                "visitor_identity_key": "email"
            }
        }
    }
}
```

### Programmatic settings

The SDK adds the module with its default settings. To change the module order, enforce settings, or initialize the module only from local or remote settings, add the module to the `modules` list in `TealiumConfig`.


<blockquote>
Programmatic settings always take precedence over local and remote settings. Only enforce values that must never change remotely.
</blockquote>


To enforce settings, pass a builder closure:



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.visitorId { builder ->
        builder.setVisitorIdentityKey("email")
    })
).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [
                               Modules.visitorId(forcingSettings: { builder in
                                   builder.setVisitorIdentityKey("email")
                               }),
                               // other modules...
                           ])
```



To initialize the module only when local or remote settings include it:



```kotlin
listOf(Modules.visitorId { null })
```


```swift
modules: [
    Modules.visitorId(forcingSettings: nil),
    // other modules...
]
```



### Disable the module

To disable the module, set `enabled` to `false` in its settings or call `setEnabled(false)` on its builder. While the module is disabled:

* Tracking events do not include `tealium_visitor_id`.
* Every `tealium.visitorId` method returns a failure.
* Visitor switching stops, and the SDK ignores identity changes in the data layer.
* The Collect module still sends events, and batches events without a visitor ID together.
* The [Context API module](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/) cannot fetch engine responses.

## Visitor switching

Visitor switching links visitor IDs to the identities you write to the data layer, so the SDK recognizes the same person across logins on the same device. The SDK has no concept of login or logout. It watches the data layer key set in `visitor_identity_key`:

* If you write a new identity and no other identity owns the current visitor ID, the SDK links the identity to the current visitor ID.
* If you write a known identity, the SDK restores the visitor ID previously linked to it.
* If you write a different, unknown identity, the SDK generates a new visitor ID and links it to that identity.
* If you remove the key or the key expires, the visitor ID stays the same and the SDK marks the identity as absent.

## Read the visitor ID

To read the visitor ID once, call `current()`. To receive the current visitor ID and every later change, subscribe to `tealium.visitorId`. The SDK emits a new value after `regenerate()`, `eraseLocalHistory()`, or a visitor switch.



```kotlin
// Read the visitor ID once
tealium.visitorId.current().subscribe { result ->
    val visitorId = result.getOrNull()
}

// Receive the current visitor ID and every later change
val subscription = tealium.visitorId.subscribe { result ->
    val visitorId = result.getOrNull()
}
```


```swift
// Read the visitor ID once
tealium.visitorId.current().subscribe { result in
    // Handle the result
}

// Receive the current visitor ID and every later change
tealium.visitorId.subscribe { result in
    switch result {
    case .success(let visitorId):
        print("Visitor ID: \(visitorId)")
    case .failure(.tealiumError(let error)):
        // The Tealium instance failed to initialize or shut down. This is the last emission.
        print("Visitor ID no longer available: \(error)")
    case .failure(let error):
        // The module is disabled. Values resume if the module is enabled again.
        print("Failed to resolve visitor ID: \(error)")
    }
}.addTo(disposable)
```



While the module is disabled, subscribers receive a failure, then receive values again if the module is enabled again. If the Tealium instance fails to initialize or shuts down, subscribers receive one final failure and the subscription ends.

## Reset the visitor ID

To generate a new anonymous visitor ID, call `regenerate()`. The result depends on whether an identity is in the data layer at the time of the call:

* If an identity is present, the identity takes ownership of the new visitor ID.
* If no identity is present, the new visitor ID is unowned. The next new identity written to the data layer adopts it, and a returning identity restores its previous visitor ID.

Calling `regenerate()` is optional. Use it in the following cases:

* **After logout**: Remove the identity key from the data layer, then call `regenerate()`. The departing identity keeps its visitor ID, and the device continues anonymously with a new one. If you call `regenerate()` before you remove the key, the SDK links the identity to the new visitor ID.
* **Before login**: Call `regenerate()` before you write a new identity to the data layer, so the new identity cannot adopt the visitor ID the device had before. The SDK processes both calls in order.



```kotlin
tealium.visitorId.regenerate().subscribe { result ->
    val newVisitorId = result.getOrNull()
}
```


```swift
tealium.visitorId.regenerate().subscribe { result in
    // Handle the result
}
```



## Erase local history

To handle a data deletion request on the device, call `eraseLocalHistory()`. This method erases every stored link between identities and visitor IDs, then generates a new anonymous visitor ID.

If an identity is in the data layer at the time of the call, the SDK links that identity to the new visitor ID. To erase without leaving any link, remove the identity from the data layer first.


<blockquote>
`eraseLocalHistory()` affects only the device. It does not remove the identity from the data layer or change server-side visitor profiles. Handle those separately.
</blockquote>




```kotlin
tealium.visitorId.eraseLocalHistory().subscribe { result ->
    val newVisitorId = result.getOrNull()
}
```


```swift
tealium.visitorId.eraseLocalHistory().subscribe { result in
    // Handle the result
}
```



If `regenerate()` or `eraseLocalHistory()` cannot store its changes, the method returns a failure. The SDK still uses the new visitor ID until the app relaunches. On the next launch, the SDK restores the previous visitor ID and all stored links.

## Set the first visitor ID

To migrate a visitor ID from a previous SDK, set an existing visitor ID in `TealiumConfig`. The SDK uses it only on first launch, before it stores any visitor ID.



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.collect())
)
    .setExistingVisitorId("EXISTING_VISITOR_ID")
    .build()
```


```swift
var config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [Modules.collect()])
config.existingVisitorId = "EXISTING_VISITOR_ID"
```



## API reference

For detailed class and method signatures, see the API reference documentation:

* [VisitorIdManager (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/VisitorIdManager.html)
* [VisitorIdManager (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-visitor-id-manager/index.html)
