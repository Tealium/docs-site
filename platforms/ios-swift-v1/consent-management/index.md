---
title: Consent management
description: Learn how to implement consent management for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift-v1/consent-management/
---
<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


## Usage

The consent management module provides a simple API to help manage tracking consent at a granular level. If you have included the CocoaPods dependency or Carthage framework, consent management is enabled by default, and no tracking calls are sent until you explicitly notify the API that the user has consented to tracking.

Usage of this module is recommended, as it is automatically included and enabled in Carthage and CocoaPods framework builds. The Foundation framework is an external dependency.

Supported platforms include: iOS, macOS, tvOS, and watchOS.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) about consent management.




## Sample App

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Tealium for Swift consent manager [sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo).


## Disable

To disable consent management, include it in the list of disabled modules on the [TealiumConfig](https://docs.tealium.com/platforms/ios-swift-v1/api/) object at initialization time.


## Data Layer

The following variables are transmitted with each tracking call while the module is enabled:

| Variable Name | Description | Example  |
| --- | --- | --- |
| `policy` | The policy under which consent was collected (default: `gdpr`) | `gdpr` |
| `consent_status` | The user's current consent status | [`consented`, `notConsented`] |
| `consent_categories` | An array of the user's selected consent categories | [`"analytics"`, `"cdp"`] |


## Examples

The following example code shows how to access the consent manager.

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                 profile: "PROFILE",
        	   	                 environment: "ENVIRONMENT",
           		                 datasource: "DATASOURCE")

		// sets the initial status to notConsented. All events sent will be deleted.
		// config.initialUserConsentStatus = .notConsented
		// sets the initial status to consented. All events transmitted immediately until consent status changed to .notConsented
		// config.initialUserConsentStatus = .consented

		// sets the initial status to unknown (default). All events queued until consent status changed
		config.initialUserConsentStatus = .unknown
		// if true, consent logging events will be generated whenever the consent status changes
		config.consentLoggingEnabled = false



		self.tealium = Tealium(config: config)

		// ...
	}


	// grants full consent (all categories)
	func grantFullConsent() {
		self.tealium?.consentManager()?.setUserConsentStatus(.consented)
	}

	/// Grants partial consent for specific categories
	/// Example usage: `grantPartialConsent([.analytics, .cdp])`
	/// - Parameter categories: `[TealiumConsentCategories]`.
	func grantPartialConsent(categories: [TealiumConsentCategories]) {
		self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: .consented, categories: categories)
	}

	// declines consent; all future events will be deleted.
	func declineConsent() {
		self.tealium?.consentManager()?.setUserConsentStatus(.notConsented)
	}

}
```

## Use Cases

### Simple Opt-in

This example shows you how to give your users a simple "Opt-in/Opt-out" option. If the user consents, they are automatically opted-in to all tracking categories. If they revoke their consent, no categories remain active, and no tracking calls are sent.

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager()?.setUserConsentStatus(status)
}
```

Define and call the following method in your Tealium Helper class when your app user consents to or declines tracking. If the user consents to tracking, the consent manager automatically opts them in to all tracking categories.

![](https://docs.tealium.com/images/platforms/ios-swift/simple-consent)

### Grouped Opt-in

This example shows a category-based consent model, where tracking categories are grouped into a smaller number of higher-level categories, defined by you.

For example, you may choose to group the Tealium consent categories `"big_data"`, `"analytics"`, and `"monitoring"` under a single category called `"performance"`. This may be easier for the user than selecting from the full list of categories. You may choose to represent this in a slider interface, ranging from least-permissive to most-permissive (all categories).

```swift
func updateConsentPreferences(_ dict: [String: Any]) {
    if let status = dict["consentStatus"] as? String {
        var tealiumConsentCategories = [TealiumConsentCategories]()
        let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
        }
        self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: tealiumConsentStatus, categories: tealiumConsentCategories)
    }
}

// example function to define groups of categories, and set the consent preferences in the consentManager API.
// call this function when the user saves their preferences
func setUserConsentPreferences(){
	// define a dictionary containing grouped categories
	let consentGroups = ["Off" : [],
	        "Performance": ["analytics", "monitoring", "big_data", "mobile", "crm"],
	        "Marketing": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp"],
	        "Personalized Advertising": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp", "display_ads", "personalization", "social", "cookiematch", "misc"]]

	// this is the user's selected preferences level. Is typically dynamic in a real app
	let userSelection = "Marketing"

	if let userList = consentGroups[userSelection] {
	  let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": userList]

	  updateConsentPreferences(settingsDict)
	}
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/grouped-gif.gif)

### Category-based Opt-in

This example shows a category-based consent model where the user must explicitly select each category from the full list of categories. The default state is `"Unknown"`, which queues hits until the user provides their consent. If the user consents to any category, events are de-queued, and the consented category data is appended to each tracking call.

```swift
// helper method to call Tealium consentManager API
func updateConsentPreferences(_ dict: [String: Any]) {
    if let status = dict["consentStatus"] as? String {
        var tealiumConsentCategories = [TealiumConsentCategories]()
        let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
        }
        self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: tealiumConsentStatus, categories: tealiumConsentCategories)
    }
}

// example function to take a list of categories and pass to the Tealium consentManager API
func setUserConsentPreferences(_ categories: [String]){

	let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": categories]
	updateConsentPreferences(settingsDict)
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/category-based)
