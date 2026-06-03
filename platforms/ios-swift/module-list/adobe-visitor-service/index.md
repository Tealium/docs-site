---
title: AdobeVisitorService Module
description: Provides a central cross-device visitor ID for each user.
url: https://docs.tealium.com/platforms/ios-swift/module-list/adobe-visitor-service/
---
The Adobe Visitor Service module interfaces directly with Adobe’s REST API to retrieve and maintain the Experience Cloud ID (ECID) for visitors.

Learn more about the [AdobeVisitorService](/platforms/getting-started-mobile/adobe-visitor-service/) module.

## Requirements

* [Tealium for Swift](/platforms/ios-swift/) (2.0.0&#43;)
* Valid Adobe account and Adobe organization ID
* [TealiumAdobeVisitorAPI GitHub Repo](https://github.com/Tealium/tealium-swift-adobe-visitor-api)

## Sample App

To help to familiarize yourself with the Tealium library and best practice implementation, explore the [AdobeVisitorService module sample app](https://github.com/Tealium/tealium-swift-adobe-visitor-api/tree/main/VisitorAPIExample) for iOS.

## Install

The AdobeVisitorService module is configured when initializing the Tealium SDK, and does not have remote configuration capabilities.

The module acts as a `DispatchValidator`, preventing calls being sent without an Adobe organization ID. It attempts to retrieve an ECID from the Adobe API, but after 5 failed attempts, calls are permitted to continue without an ECID to avoid data loss. Sending data is prioritized over having a valid ECID.

Possible causes for no ECID being retrieved are:

* Invalid response, such as a response was received but did not contain a valid ECID.
* There was no response.
* The Adobe organization ID was invalid.

### Carthage

To install the AdobeService module with Carthage, add the following to your cartfile:

```bash
github &#34;tealium/tealium-swift-adobe-visitor-api&#34;
```

[Learn more](/platforms/ios-swift/install/#carthage) about Carthage installation for iOS.

### CocoaPods


To install the AdobeVisitor module with CocoaPods, add the following pod to your podfile:  
```perl
pod &#39;TealiumAdobeVisitorAPI&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).

### Swift Package Manager (Recommended)

Swift Package Manager is the recommended way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/Tealium/tealium-swift-adobe-visitor-api`.
1. Configure the version rules. The default, `&#34;Up to next major&#34;`, is recommended. If the current Tealium Swift library version does not appear in the list, reset your Swift package cache.
1. Select the `TealiumAdobeVisitorAPI` module from the list of modules to install. Add the module to each of your app targets in your Xcode project under **Frameworks and Libraries**.

Learn more about the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) installation for iOS.

```swift
import TealiumAdobeVisitorAPI

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;ENVIRONMENT&#34;)
config.collectors = [Collectors.AppData,
    Collectors.Connectivity,
    Collectors.Device,
    Collectors.Lifecycle,
    Collectors.AdobeVisitor]
config.dispatchers = [Dispatchers.Collect]
self.tealium = Tealium(config: config)
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

Learn more about the [Swift Package Manager installation for iOS](/platforms/ios-swift/install/#swift-package-manager-recommended).

To link a known visitor ID or set the authentication state, see [Set a known visitor ID and authentication state](/platforms/getting-started-mobile/adobe-visitor-service/#set-a-known-visitor-id-and-authentication-state).

