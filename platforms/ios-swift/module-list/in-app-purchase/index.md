---
title: In-App Purchase Module
description: The In-App Purchase module adds automatic tracking of in-app purchases to your app.
url: https://docs.tealium.com/platforms/ios-swift/module-list/in-app-purchase/
---
## What is an in-app purchase?

An in-app purchase is additional content, services, or a subscription that you buy inside the app. Some examples of in-app purchases include:

* Upgrade to remove ads
* Game credits
* Virtual currency
* Extra game levels
* Unlock more features

Examples of purchases that are not considered in-app purchases include:

* Purchasing clothes or other items in an e-commerce app.
* Using Apple Pay to complete a purchase.

Learn more about [in-app purchases in the Apple developer portal](https://developer.apple.com/in-app-purchase/).

## Install

Install the In-App Purchase module with Swift Package Manager, CocoaPods, or Carthage.

### Swift Package Manager (Recommended)

Swift Package Manager is the recommended way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`.
1. Configure the version rules. The default, `&#34;Up to next major&#34;`, is recommended. If the current Tealium Swift library version does not appear in the list, reset your Swift package cache.
1. Select the `InAppPurchase` module from the list of modules to install. Add the module to each of your app targets in your Xcode project under **Frameworks and Libraries**.

Learn more about the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) installation for iOS.

### CocoaPods

To install the In-App Purchase module with CocoaPods, add the following pod to your Podfile:

```perl
pod &#39;tealium-swift/InAppPurchase&#39;
```
Learn more about the [CocoaPods](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods) installation for iOS.

### Carthage

Follw these steps to install the In-App Purchase module with Carthage:

1. Navigate to the **General** configuration pane for the target app in Xcode.
2. Add the following framework to the **Embedded Binaries** section:
      ```swift
      TealiumInAppPurchase.xcframework
      ```
3. To import the In-App Purchase library, add the following import statement to your project:
      ```swift
      import TealiumInAppPurchase
      ```

Learn more about the [Carthage](https://docs.tealium.com/platforms/ios-swift/install/#carthage) installation for iOS.

## Configure

To instantiate the In-App Purchase module, you must specify it in your `TealiumConfig` object when initializing the SDK:

```swift
import TealiumCore
import TealiumInAppPurchase

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           datasource: &#34;DATASOURCE&#34;)

config.collectors = [Collectors.InAppPurchase]
tealium = Tealium(config: config) { _ in }
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Data Layer

The In-App Purchase module sends the following attributes in the event:

| Variable             | Description                                                         | Example |
|:---------------------|:--------------------------------------------------------------------|:--|
| `purchase_order_id`  | The order ID of the purchase.                                       | &#34;1234567890&#34; |
| `purchase_timestamp` | The timestamp of the purchase in ISO 8601 format.                   | &#34;2022-01-17T14:42:28Z&#34; |
| `purchase_quantity`  | The total number of items purchased.                                | &#34;1&#34; |
| `purchase_skus`      | An array of the product IDs purchased.                              | [&#34;com.example.level1&#34;] |
| `autotracked`        | Set to `true` to indicate that the event was tracked automatically. | true |
| `tealium_event`      | The name of the event.                                              | &#34;in_app_purchase&#34; |
