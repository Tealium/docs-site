---
title: Consent management
description: Learn to implement consent management for Android Kotlin.
url: https://docs.tealium.com/platforms/android-kotlin/consent-management/
---
## Usage

The consent management module is recommended and automatically enabled upon initialization. It is supported on Android mobile and Android TV.

Initialize the consent manager policy inside [`TealiumConfig`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy). Then manage user consent using the Tealium instance at [`tealium.consentManager`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#consentmanager).

Learn more about [consent management](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) and consent policies.

## Consent

### Set Policy

Set the consent policy during initialization to one of the following:

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`


<blockquote>
Only one policy may be enforced on a device at any given time.
</blockquote>


```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
}
```

### Consent Expiration

Set the expiration time for the consent selections using the [`consentExpiry`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#consentexpiry) property.


The following example sets the consent manager policy to GDPR and the expiration time to 90 days:  

```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
  consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
}
```

To trigger a callback once the consent has expired, use the [`onUserConsentPreferencesUpdated()`](https://docs.tealium.com/platforms/android-kotlin/api/consent-manager/#onuserconsentpreferencesupdated) method to check when the `ConsentStatus` is `UNKNOWN`:

```java
Tealium.create(BuildConfig.TEALIUM_INSTANCE, config) {
    events.subscribe(object : UserConsentPreferencesUpdatedListener {
        override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences,
                                                     policy: ConsentManagementPolicy) {
            if (userConsentPreferences.consentStatus == ConsentStatus.UNKNOWN) {
                Logger.dev(BuildConfig.TAG, "Re-prompt for consent")
            }
        }
    })
}
```

### Set Full Consent

To set full consent:

```java
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED
```


<blockquote>
Setting full consent implicitly sets the consent categories to the full list of available [`ConsentCategory`](https://docs.tealium.com/platforms/android-kotlin/api/consent-category/#class-consentcategory) types.
</blockquote>


### Set Partial Consent by Category

To set partial consent, specify a subset of consent categories. This implicitly sets [`userConsentStatus`](https://docs.tealium.com/platforms/android-kotlin/api/consent-manager/#userconsentstatus) to `CONSENTED`.

```java
tealium.consentManager.userConsentCategories = setOf(ConsentCategory.ANALYTICS, ConsentCategory.EMAIL)
```

### Set Declined Consent

To decline consent set the consent status:  
```java
tealium.consentManager.userConsentStatus = ConsentStatus.NOT_CONSENTED
```

Alternatively, set the consent categories to `null`.

## Custom Consent

If your organization's consent requirements are not covered by our standard [Opt-in](https://docs.tealium.com/glossary/#opt-in-model-consent) and [Opt-out](https://docs.tealium.com/glossary/#opt-out-model-consent) consent management policies, create a custom consent policy.

1. Implement the `ConsentManagementPolicy` interface.      
      ```java
      val customPolicy = object: ConsentManagementPolicy {
            //implement methods...
      }
      ```
2. Pass the `ConsentManagementPolicy` implementation to the `ConsentPolicy.CUSTOM` enum using the `setCustomPolicy()` method.      
      ```java
      ConsentPolicy.CUSTOM.setCustomPolicy(customPolicy)
      ```
3. Pass the `ConsentPolicy.CUSTOM` option on your `TealiumConfig` object through the [`consentManagerPolicy`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy) property.   
      ```java
      config.consentManagerPolicy = ConsentPolicy.CUSTOM
      ```

Your custom `ConsentManagementPolicy` implementation may delegate existing consent management methods and properties to the provided `superPolicy`, which overrides the `policy` key with its own name on each event.

```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
        ) : ConsentManagementPolicy by superPolicy {
    override val name: String = "custom_policy"

    override fun policyStatusInfo(): Map<String, Any> {
        return superPolicy.policyStatusInfo().toMutableMap().apply {
            put(ConsentManagerConstants.CONSENT_POLICY, name)
        }
    }
}

val customPolicy = CustomPolicy(ConsentPolicy.GDPR.create(
    UserConsentPreferences(ConsentStatus.UNKNOWN, null)))
```

After the custom consent policy is implemented, override the following properties and methods available on the `ConsentManagementPolicy` as needed:

| Property / Method | Type | Description |
| ----- | ------ | ----- |
| `name` | `String` | Name of the `ConsentManagementPolicy`|
| `userConsentPreferences` | `UserConsentPreferences` | The current `UserConsentPreferences` that are automatically updated by the `ConsentManager` when the preferences change|
| `consentLoggingEnabled` | `Boolean` | Sets whether or not logging of consent changes are required |
| `consentLoggingEventName` | `String` | Sets the event name (key: `tealium_event`) to use when logging a change in consent |
| `defaultConsentExpiry`] |`ConsentExpiry` | Sets the default expiry time for the `ConsentManagementPolicy` |
| `cookieUpdateRequired`| `Boolean` | Sets whether or not to update a cookie in the TagManagement module's webview|
| `cookieUpdateEventName` |  `String` | Sets the event name to use when `cookieUpdateRequired` is set to `true`|
| `policyStatusInfo()` |`Map<String, Any>` | Returns a map of key-value data to be added to the payload of each dispatch |
| `shouldQueue()` | `Boolean` | Returns whether or not to queue dispatches according to the `ConsentPolicy` rules|
| `shouldDrop()`| `Boolean` | Returns whether or not to drop dispatches according to the `ConsentPolicy` rules|

### Examples

The following example re-maps the policy data keys to avoid Tealium EventStream fixed consent values:   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    return superPolicy.policyStatusInfo().toMutableMap().apply {
        get(ConsentManagerConstants.CONSENT_STATUS)?.let { status ->
            remove(ConsentManagerConstants.CONSENT_STATUS)
            put("custom_consent_status", status)
        }
        get(ConsentManagerConstants.CONSENT_CATEGORIES)?.let { categories ->
            remove(ConsentManagerConstants.CONSENT_CATEGORIES)
            put("custom_consent_categories", categories)
        }
    }
}
```

The following example customizes the consent logging event name that is sent:   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    override val consentLoggingEventName: String
        get() {
            return when(userConsentPreferences.consentStatus) {
                ConsentStatus.CONSENTED -> "user_consented"
                ConsentStatus.NOT_CONSENTED -> "user_not_consented"
                ConsentStatus.UNKNOWN -> "user_consent_unknown"
            }
        }
}
```

The following example returns third-party consent values, where `thirdPartyConsentProvider` is a reference to another consent provider:   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy,
        val thirdPartyConsentLibrary: OtherConsentProvider
) : ConsentManagementPolicy by superPolicy {
    override fun policyStatusInfo(): Map<String, Any> {
        val status = thirdPartyConsentLibrary
                .getConsent(userConsentPreferences.consentStatus == ConsentStatus.CONSENTED)
        return mapOf("my_consent_status" to status)
    }
}
```
