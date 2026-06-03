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

Learn more about [consent management](/platforms/getting-started-mobile/consent-management/) and consent policies.

## Consent

### Set Policy

Set the consent policy during initialization to one of the following:

* `.gdpr`
* `.ccpa`

The consent management module is included with the core library and is not active until a consent policy is set.

Only one policy may be enforced on a device at any given time.

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

Set the expiration time for the consent selections using the [`consentExpiry`](/platforms/ios-swift/api/tealium-config/#consentexpiry) property.

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

To trigger a callback once the consent has expired, define your callback on the [`TealiumConfig`](/platforms/ios-swift/api/tealium-config/) object:

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
		config.consentExpiry = (90, .days)
		config.onConsentExpiration = {
       	print(&#34;Consent expired&#34;)
       }
    //...
	}
}
```
Alternatively, define your callback on the [`TealiumConsentManager`](/platforms/ios-swift/api/tealium-consent-manager/) object:

```swift
tealium = Tealium(config: config) { [weak self] _ in
	self?.tealium?.consentManager?.onConsentExpiration = {
		print(&#34;Consent expired&#34;)
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

To set partial consent, specify a subset of consent categories. This implicitly sets [`userConsentStatus`](/platforms/ios-swift/api/tealium-consent-manager/#userconsentstatus) to `.consented`.   
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

If your organization&#39;s consent requirements are not covered by our standard GDPR and CCPA policies, create a custom consent policy.

1. Implement the `ConsentPolicy` protocol.   
```swift
class SomeCustomConsentPolicy: ConsentPolicy {
      // implement methods...
}
```

2. Set the [`consentPolicy`](/platforms/ios-swift/api/tealium-config/#consentpolicy) property on the `TealiumConfig` object to your new custom policy by using the `TealiumConsentPolicy.custom` enum with an associated type.   
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
| `shouldUpdateConsentCookie` | `Bool` |Sets whether or not to update a cookie in the TagManagement module&#39;s webview |
| `trackAction` | `TealiumConsentTrackAction`| The tracking action based on the consent status (allowed, forbidden, queued) |
| `updateConsentCookieEventName` | `String` | Sets the event name to use when `shouldUpdateConsentCookie` is set to true |

The following is a full example of a custom consent policy:  

```swift
class MyCustomConsentPolicy: ConsentPolicy {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var name: String = &#34;my custom policy&#34;

    var defaultConsentExpiry: (time: Int, unit: TimeUnit) = (90, .days)

    var shouldUpdateConsentCookie: Bool = false

    var updateConsentCookieEventName: String = &#34;custom_consent_update&#34;

    var consentPolicyStatusInfo: [String : Any]? {
        [&#34;custom_consent_status&#34;: preferences.consentStatus.rawValue,
         &#34;custom_consent_categories&#34;: preferences.consentCategories?.map({ $0.rawValue }),
         &#34;custom_policy_key&#34;: name]
    }

    var trackAction: TealiumConsentTrackAction  = .trackingAllowed

    var consentTrackingEventName: String = &#34;custom_consent_update&#34;

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
        &#34;customGDPRPolicy&#34;
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
        [&#34;custom_consent_status&#34;: preferences.consentStatus.rawValue,
         &#34;custom_consent_categories&#34;: preferences.consentCategories?.map({ $0.rawValue }),
         &#34;custom_policy_key&#34;: &#34;customGDPRPolicy&#34;]
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
            return &#34;user_consented&#34;
        case .notConsented:
            return &#34;user_not_consented&#34;
        case .unknown:
            return &#34;user_consent_unknown&#34;
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
        return [&#34;my_consent_status&#34;: status]
    }

}
```


## Use Cases

### Full Consent

The following example shows how to give your users the option to consent or decline the consent policy.  Once the user has consented or declined, the rules for your selected consent policy takes effect. Learn more about [consent policies](/platforms/getting-started-mobile/consent-management/#consent-policies).

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager?.userConsentStatus = status
}
```

Define and call the method in your Tealium Helper class when your app user consents to or declines tracking. If the user consents to tracking, the consent manager automatically includes them in all tracking categories.

![](/images/platforms/ios-swift/simple-consent)

### Partial Consent by Category (GDPR)

In category-based consent, the user must explicitly select each category from the full list of categories.

The following helper method calls methods from the [`TealiumConsentManager`](/platforms/ios-swift/api/tealium-consent-manager/) API:  
```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict[&#34;consentCategories&#34;] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict[&#34;consentStatus&#34;] as? String {
            let tealiumConsentStatus = (status == &#34;consented&#34;) ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

To update a list of categories:  
```swift
func setUserConsentPreferences(_ categories: [String]){
	let settingsDict: [String: Any] = [&#34;consentStatus&#34;: &#34;consented&#34;, &#34;consentCategories&#34;: categories]
	updateConsentPreferences(settingsDict)
}
```

#### Category Groups (GDPR)

In a category-based consent model, tracking categories are grouped into a smaller number of higher-level categories, defined by the customer.

For example, you may choose to group the Tealium consent categories `&#34;big_data&#34;`, `&#34;analytics&#34;`, and `&#34;monitoring&#34;` under a single category called `&#34;performance&#34;`. This may be easier for the user than selecting from the full list of categories. You may choose to represent this in a slider interface, ranging from least-permissive to most-permissive (all categories).

```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict[&#34;consentCategories&#34;] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict[&#34;consentStatus&#34;] as? String {
            let tealiumConsentStatus = (status == &#34;consented&#34;) ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

The following helper function defines groups of categories and sets the users consent preferences:  

```swift
func setUserConsentPreferences(){
	let consentGroups = [&#34;Off&#34; : [],
	        &#34;Performance&#34;: [&#34;analytics&#34;, &#34;monitoring&#34;, &#34;big_data&#34;, &#34;mobile&#34;, &#34;crm&#34;],
	        &#34;Marketing&#34;: [&#34;analytics&#34;, &#34;monitoring&#34;, &#34;big_data&#34;, &#34;mobile&#34;, &#34;crm&#34;, &#34;affiliates&#34;, &#34;email&#34;, &#34;search&#34;, &#34;engagement&#34;, &#34;cdp&#34;],
	        &#34;Personalized Advertising&#34;: [&#34;analytics&#34;, &#34;monitoring&#34;, &#34;big_data&#34;, &#34;mobile&#34;, &#34;crm&#34;, &#34;affiliates&#34;, &#34;email&#34;, &#34;search&#34;, &#34;engagement&#34;, &#34;cdp&#34;, &#34;display_ads&#34;, &#34;personalization&#34;, &#34;social&#34;, &#34;cookiematch&#34;, &#34;misc&#34;]]

	let userSelection = &#34;Marketing&#34;

	if let userList = consentGroups[userSelection] {
	  let settingsDict: [String: Any] = [&#34;consentStatus&#34;: &#34;consented&#34;, &#34;consentCategories&#34;: userList]

	  updateConsentPreferences(settingsDict)
	}
}
```

![](/images/platforms/ios-swift/grouped-gif.gif)

## Sample App

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Tealium for Swift [consent manager sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo).

![](/images/platforms/ios-swift/category-based)

