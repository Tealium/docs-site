---
title: TealiumConsentManager
description: Provides methods for Tealium consent management.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-consent-manager/
---
## Class: `TealiumConsentManager`

The following summarizes the commonly used methods of the iOS (Swift) `TealiumInstanceManager` class.

| Method | Description |
| ----- | ------ |
| `addConsentDelegate()` | Registers a specific class conforming to the `TealiumConsentDelegate` protocol |
| `getUserConsentCategories()` | Returns all current consent categories |
| `getUserConsentPreferences()` | Returns all current consent preferences|
| `getUserConsentStatus()` |Returns the current consent status |
| `removeAllConsentDelegates()` | Removes all consent delegates |
| `resetUserConsentPreferences()` | Clears all currently stored consent preferences in memory and in persistent storage |
| `setUserConsentCategories()` | Sets the user's consent categories |
| `setUserConsentStatus()` | Sets the user's consent status |
| `setUserConsentStatusWithCategories()` | Sets consent status and categories |

### `addConsentDelegate()`

Registers a specific class conforming to the `TealiumConsentDelegate` protocol.

```swift
addConsentDelegate(delegate)
```

| Parameters | Type  | Description |
| --- | --- | --- |
| `delegate` | `TealiumConsentManagerDelegate` | A class conforming to `TealiumConsentDelegate` |

### `getUserConsentCategories()`

Returns all current consent categories.

```swift
getUserConsentCategories()
```

| Return Type | Description |
| --- | --- |
| `TealiumConsentCategories` | Current Tealium consent categories |

### `getUserConsentPreferences()`

Returns all current consent preferences.

```swift
getUserConsentPreferences()
```

| Return Type | Description |
| --- | --- |
| `TealiumConsentUserPreferences` | All current consent preferences |


### `getUserConsentStatus()`

Returns the current consent status.

```swift
getUserConsentStatus()
```

| Return Type | Description |
| --- | --- |
| `TealiumConsentStatus` | Current consent status |


### `removeAllConsentDelegates()`

Removes all consent delegates. Retains the built-in delegate created by the `TealiumConsentManagerModule` class.

```swift
removeAllConsentDelegates()
```

### `resetUserConsentPreferences()`

Clears all currently stored consent preferences in memory and in persistent storage. Reverts to `"unknown"` consent state, with no categories.

```swift
resetUserConsentPreferences()
```


### `setUserConsentCategories()`

Sets the user's consent categories. Designed to be called from your consent management preferences screen in your app. Sets consent status to `.consented`.

```swift
setUserConsentCategories(categories)
```

| Parameter | Type Description | Example |
| --- | --- | --- |
| `categories` | An array of values from the TealiumConsentCategories enum | `[.analytics,.bigData]` |

The following example shows how to set the user consent categories to `[.analytics,.bigData]`:

```swift
tealium?.consentManager()?.setUserConsentCategories([.analytics,.bigData])
```


### `setUserConsentStatus()`

Sets the user's consent status. Designed to be called from your consent management preferences screen in your app when the user enables or disables tracking.

Sets the list of consented categories to include ALL available consent categories, if the status is `.consented`. Does not allow categories to be set selectively.

```swift
setUserConsentStatus(status)
```

| Parameters | Type |  Description | Example |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus` | The consent status to be set| [`.unknown`, `.consented`, `.notConsented`] |

The following example shows how to set the user consent status to `.consented`:

```swift
tealium?.consentManager()?.setUserConsentStatus(.consented)
```

The following define the different types of Tealium consent statuses from the `TealiumConsentStatus` enum.

**.unknown**  
The `unknown` status is the default setting for the consent manager. In this state, the consent manager queues events locally until an affirmative `consented`/`notConsented` status is provided.

**.consented**  
The `consented` status is set when the user has consented to tracking. In this state, the consent manager allow all tracking calls to continue as normal.

**.notConsented**  
The `notConsented` status is set when the user has declined tracking. In this state, the consent manager drops all tracking calls and halt further processing by the SDK.



### `setUserConsentStatusWithCategories()`

Sets consent status and categories.

```swift
setUserConsentStatusWithCategories(status, categories)
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus?` | The consent status to be set| [`.unknown`, `.consented`, `.notConsented`] |
| `categories` | `[TealiumConsentCategories]?` | The consented categories to be set | `[.analytics]` |

The following example shows how to set the user consent status to `.consented` and set the categories to `.analytics`:

```swift
tealium?.consentManager()?.setUserConsentStatusWithCategories(status: .consented, categories: [.analytics])
```
