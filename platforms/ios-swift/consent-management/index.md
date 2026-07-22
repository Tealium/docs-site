---
title: Consent management
description: Learn how to implement consent management for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift/consent-management/
---
## Usage

The consent manager module provides a simple API to help manage tracking consent at a granular level. It is supported on all Apple platforms (iOS, iPadOS, tvOS, watchOS, macOS, macOS Catalyst).

Version 2.x of the Tealium Swift library introduces important changes to the consent manager module:

* Consent manager disabled by default (see [Full Consent](#full-consent) to enable)
* Consent manager incorporated into the `TealiumCore` module
* CCPA support introduced
* Consent expiration options

Learn more about [consent management](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) and consent policies.

## Consent

### Set Policy

Set the consent policy during initialization to one of the following:

* `.gdpr`
* `.ccpa`

The consent management module is included with the core library and is not active until a consent policy is set.


<blockquote>
Only one policy may be enforced on a device at any given time.
</blockquote>


To set the GDPR policy:  

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
    //...
	}
}
```

To set consent logging events, which are generated whenever the consent status changes:  
```swift
config.consentLoggingEnabled = true
```

### Consent Expiration

Set the expiration time for the consent selections using the [`consentExpiry`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#consentexpiry) property.

The following example sets the consent manager policy to GDPR and the expiration time to 90 days:

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
		config.consentExpiry = (90, .days)
    //...
	}
}
```

To trigger a callback once the consent has expired, define your callback on the [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/) object:

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
		config.consentExpiry = (90, .days)
		config.onConsentExpiration = {
       	print("Consent expired")
       }
    //...
	}
}
```
Alternatively, define your callback on the [`TealiumConsentManager`](https://docs.tealium.com/platforms/ios-swift/api/tealium-consent-manager/) object:

```swift
tealium = Tealium(config: config) { [weak self] _ in
	self?.tealium?.consentManager?.onConsentExpiration = {
		print("Consent expired")
	}
}
```

### Set Full Consent

To set full consent:  
```swift
func grantFullConsent() {
	self.tealium?.consentManager?.userConsentStatus = .consented
}
```

### Set Partial Consent by Category

To set partial consent, specify a subset of consent categories. This implicitly sets [`userConsentStatus`](https://docs.tealium.com/platforms/ios-swift/api/tealium-consent-manager/#userconsentstatus) to `.consented`.   
```swift
func grantPartialConsent(categories: [TealiumConsentCategories]) {
	self.tealium?.consentManager?.userConsentCategories = categories
}
```

Example usage: `grantPartialConsent([.analytics, .cdp])` (see parameter categories)

### Set Declined Consent

To decline consent set the consent status:  
```swift
func declineConsent() {
	self.tealium?.consentManager?.userConsentStatus = .notConsented
}
```

## Custom Consent

If your organization's consent requirements are not covered by our standard GDPR and CCPA policies, create a custom consent policy.

1. Implement the `ConsentPolicy` protocol.   
```swift
class SomeCustomConsentPolicy: ConsentPolicy {
      // implement methods...
}
```

2. Set the [`consentPolicy`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#consentpolicy) property on the `TealiumConfig` object to your new custom policy by using the `TealiumConsentPolicy.custom` enum with an associated type.   
```swift
config.consentPolicy = .custom(SomeCustomConsentPolicy.self)
```

After the custom consent policy is implemented, override the following properties available on the `ConsentPolicy` as needed:

| Property | Type | Description |
| ---- | ---- | ---- |
| `name` | `String` | Name of the `ConsentPolicy`|
| `consentPolicyStatusInfo` | `[String: Any]?`| Returns:`[String: Any]` of key-value data to be added to the payload of each `TealiumDispatch`|
| `consentTrackingEventName` | `String` | Sets the event name (key: `tealium_event`) to use when logging a change in consent |
| `defaultConsentExpiry` | `(time: Int, unit: TimeUnit)` | Sets the default expiry time for this `ConsentPolicy` |
| `preferences` | `UserConsentPreferences` | The current `UserConsentPreferences` that are automatically updated by the `ConsentManager` when the preferences change|
| `shouldLogConsentStatus` | `Bool` | Sets whether or not logging of consent changes are required |
| `shouldUpdateConsentCookie` | `Bool` |Sets whether or not to update a cookie in the TagManagement module's webview |
| `trackAction` | `TealiumConsentTrackAction`| The tracking action based on the consent status (allowed, forbidden, queued) |
| `updateConsentCookieEventName` | `String` | Sets the event name to use when `shouldUpdateConsentCookie` is set to true |

The following is a full example of a custom consent policy:  

```swift
class MyCustomConsentPolicy: ConsentPolicy {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var name: String = "my custom policy"

    var defaultConsentExpiry: (time: Int, unit: TimeUnit) = (90, .days)

    var shouldUpdateConsentCookie: Bool = false

    var updateConsentCookieEventName: String = "custom_consent_update"

    var consentPolicyStatusInfo: [String : Any]? {
        ["custom_consent_status": preferences.consentStatus.rawValue,
         "custom_consent_categories": preferences.consentCategories?.map({ $0.rawValue }),
         "custom_policy_key": name]
    }

    var trackAction: TealiumConsentTrackAction  = .trackingAllowed

    var consentTrackingEventName: String = "custom_consent_update"

    var shouldLogConsentStatus: Bool = true

}
var tealium: Tealium?
let config = TealiumConfig(...)
config.consentPolicy = .custom(MyCustomConsentPolicy.self)
/// ... other configuration options
tealium = Tealium(config: config)
```

Create your custom policy that conforms to either the `GDPRConsentPolicyCreatable` or `CCPAConsentPolicyCreatable` protocol. After you create your custom policy and override what you want to override, set `config.consentPolicy` to `.custom(YourCustomPolicy.self)`.


### Examples

Using the existing GDPR implementation, but overriding the name of the policy (overrides the `policy` value in the tracking payload):   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var name: String {
        "customGDPRPolicy"
    }

}

config.consentPolicy = .custom(CustomGDPRConsentPolicy.self)
```

Remapping the policy data keys to avoid Tealium EventStream fixed consent values:   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentPolicyStatusInfo: [String : Any]? {
        ["custom_consent_status": preferences.consentStatus.rawValue,
         "custom_consent_categories": preferences.consentCategories?.map({ $0.rawValue }),
         "custom_policy_key": "customGDPRPolicy"]
    }

}
```

Customize the consent logging event name that is sent:   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentTrackingEventName: String {
        switch preferences.consentStatus {
        case .consented:
            return "user_consented"
        case .notConsented:
            return "user_not_consented"
        case .unknown:
            return "user_consent_unknown"
        }
    }

}
```

Return third-party consent values instead, if `thirdPartyConsentProvider` is a reference to another consent provider:   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    let thirdPartyConsentProvider = ThirdPartyProvider()
    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentPolicyStatusInfo: [String: Any]? {
        let status = thirdPartyConsentProvider.getConsent()
        return ["my_consent_status": status]
    }

}
```


## Use Cases

### Full Consent

The following example shows how to give your users the option to consent or decline the consent policy.  Once the user has consented or declined, the rules for your selected consent policy takes effect. Learn more about [consent policies](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/#consent-policies).

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager?.userConsentStatus = status
}
```

Define and call the method in your Tealium Helper class when your app user consents to or declines tracking. If the user consents to tracking, the consent manager automatically includes them in all tracking categories.

![](https://docs.tealium.com/images/platforms/ios-swift/simple-consent)

### Partial Consent by Category (GDPR)

In category-based consent, the user must explicitly select each category from the full list of categories.

The following helper method calls methods from the [`TealiumConsentManager`](https://docs.tealium.com/platforms/ios-swift/api/tealium-consent-manager/) API:  
```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict["consentStatus"] as? String {
            let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

To update a list of categories:  
```swift
func setUserConsentPreferences(_ categories: [String]){
	let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": categories]
	updateConsentPreferences(settingsDict)
}
```

#### Category Groups (GDPR)

In a category-based consent model, tracking categories are grouped into a smaller number of higher-level categories, defined by the customer.

For example, you may choose to group the Tealium consent categories `"big_data"`, `"analytics"`, and `"monitoring"` under a single category called `"performance"`. This may be easier for the user than selecting from the full list of categories. You may choose to represent this in a slider interface, ranging from least-permissive to most-permissive (all categories).

```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict["consentStatus"] as? String {
            let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

The following helper function defines groups of categories and sets the users consent preferences:  

```swift
func setUserConsentPreferences(){
	let consentGroups = ["Off" : [],
	        "Performance": ["analytics", "monitoring", "big_data", "mobile", "crm"],
	        "Marketing": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp"],
	        "Personalized Advertising": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp", "display_ads", "personalization", "social", "cookiematch", "misc"]]

	let userSelection = "Marketing"

	if let userList = consentGroups[userSelection] {
	  let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": userList]

	  updateConsentPreferences(settingsDict)
	}
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/grouped-gif.gif)

## Sample App

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Tealium for Swift [consent manager sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo).

![](https://docs.tealium.com/images/platforms/ios-swift/category-based)

