---
title: ConsentManager
description: Reference guide for ConsentManager class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/consent-manager/
---
## Class: `ConsentManager`

The following summarizes the commonly used methods of the `ConsentManager` class for Kotlin. See [consent management](/platforms/android-kotlin/consent-management/) for more details.

| Method | Description |
| ----- | ------ |
| [`isConsentLoggingEnabled`](#isconsentloggingenabled) | Gets/sets whether to log consent preference changes |
| [`policy`](#policy) | Gets the current policy that is in force (nullable) |
| [`reset()`](#reset) | Resets the Consent Status and Categories back to default values |
| [`userConsentCategories`](#userconsentcategories) | Gets/sets the currently consented set of `ConsentCategory`s |
| [`userConsentStatus`](#userconsentstatus) | Gets/sets the current user `ConsentStatus` |

### `isConsentLoggingEnabled`

Get or set whether to log changes to the user consent preferences. Initialized through the [TealiumConfig.consentManagerLoggingEnabled](/platforms/android-kotlin/api/tealium-config/#consentmanagerloggingenabled) option.

```java
tealium.consentManager.isConsentLoggingEnabled // for example: false
```

### `policy`

Returns the currently in-use `ConsentPolicy`. Initialized through the [TealiumConfig.consentManagerPolicy](/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy) option, and may be set to `null`.

```java
val policy = tealium.consentManager.policy // for example: ConsentPolicy.GDPR
```

### `reset()`

Returns the provided `userConsentStatus` and `userConsentCategories` back to their default values; `ConsentStatus.UNKNOWN` and `null` respectively.

```java
tealium.consentManager.reset()
```



### `userConsentCategories`

Set or get the current Consent Status as granted by the app user. Learn more about the [available options](/platforms/android-kotlin/api/consent-category/).

```java
tealium.consentManager.userConsentCategories = setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)

val categories = tealium.consentManager.userConsentCategories
// returns setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)
```

### `userConsentStatus`

Set or get the current consent status as granted by the app user. Available options are: `UNKOWN`, `CONSENTED` and `NOT_CONSENTED`

```java
tealium.consentManager.userConsentPreferences = ConsentStatus.CONSENTED

val status = tealium.consentManager.userConsentStatus // returns ConsentStatus.CONSENTED
```

## Interface: `UserConsentPreferencesUpdatedListener`

The `UserConsentPreferencesUpdatedListener` is a listener interface. Register to receive the latest version updates of `UserConsentPreferences` and `ConsentPolicy`.

| Method | Description |
| ----- | ------ |
| [`onUserConsentPreferencesUpdated()`](#onuserconsentpreferencesupdated) | Gets or sets whether to log consent preference changes |

### `onUserConsentPreferencesUpdated()`

Gets or sets whether to log consent preference changes. Implement the method on a class that implements the interface, or pass in an anonymous object after creating your `Tealium` instance.

```java
onUserConsentPreferencesUpdated(userConsentPreferences:policy:)
```

| Parameters   | Type     | Description     |
| ------------ | -------- | --------------- |
| `userConsentPreferences` | `UserConsentPreferences` | User consent preferences  |
| `policy` | `ConsentManagementPolicy` | Consent management policy |

Example:

```java
val tealium = Tealium.create(...) {
    events.subscribe(object : UserConsentPreferencesUpdatedListener {
        override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences,
            policy: ConsentManagementPolicy) {
            Logger.dev(BuildConfig.TAG, &#34;Consent preferences have been updated&#34;)

            }
        )}
    )
}
```
