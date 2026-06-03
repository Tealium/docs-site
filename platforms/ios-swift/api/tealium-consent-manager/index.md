---
title: TealiumConsentManager
description: Provides methods for Tealium consent management.
url: https://docs.tealium.com/platforms/ios-swift/api/tealium-consent-manager/
---
## Class: `TealiumConsentManager`

The following summarizes the commonly used methods of the iOS (Swift) `TealiumConsentManager` class.

| Method/Property | Description |
| ----- | ------ |
| [`onConsentExpiration`](#onconsentexpiration) | Callback to execute once consent selections expire |
| [`resetUserConsentPreferences()`](#resetuserconsentpreferences) | Clears all currently stored consent preferences in memory and in persistent storage |
| [`userConsentStatus`](#userconsentstatus) | Gets or sets the user&#39;s consent status |
| [`userConsentCategories`](#userconsentcategories) | Gets or sets the user&#39;s consent categories |

### `onConsentExpiration`

Callback to execute once consent selections expire.

```swift
config.onConsentExpiration = {
   // display consent modal
}
```

### `userConsentStatus`

Gets or sets the current consent status.

```swift
let categories = tealium.consentManager?.userConsentStatus
tealium.consentManager?.userConsentStatus = .consented
```

| Parameter Type | Description |
| --- | --- |
| `TealiumConsentStatus` | Current consent status |

### `resetUserConsentPreferences()`

Clears all currently stored consent preferences in memory and in persistent storage. Reverts to `&#34;unknown&#34;` consent state, with no categories.

```swift
resetUserConsentPreferences()
```

### `userConsentCategories`

Gets or sets all current consent categories.

```swift
let categories = tealium.consentManager?.userConsentCategories
tealium.consentManager?.userConsentCategories = [.cdp]
```

| Parameter Type | Description |
| --- | --- |
| `TealiumConsentCategories` | Current Tealium consent categories |
