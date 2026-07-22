---
title: Collect Module
description: Dispatches tracking calls to Tealium Customer Data Hub server-side products.
url: https://docs.tealium.com/platforms/ios-swift/module-list/collect/
---
## Usage

The Collect module dispatches tracking calls to Tealium Customer Data Hub. Usage of this module is strongly recommended if you are using Customer Data Hub server-side.

As an alternative, if you are using the Tag Management module, you may instead use the Collect tag with Tealium iQ. This may give greater control over the data and events dispatched to the Customer Data Hub, as you may then use load rules and extensions to manipulate the data prior to dispatch. If you are using the Collect tag with Tealium iQ, ensure that the Collect module is disabled to avoid duplicate tracking requests.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the Collect module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `"Up to next major"` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `Collect` module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

Learn more about the [Swift Package Manager installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended).

### CocoaPods

To install the Collect module with CocoaPods, add the following pod to your Podfile:  
```perl
pod 'tealium-swift/Collect'
```

Learn more about the [CocoaPods installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods).


### Carthage

To install the Collect module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumCollect.framework
      ```

[Learn more](https://docs.tealium.com/platforms/ios-swift/install/#carthage) about Carthage installation for iOS.

## Initialize

To initialize the module, verify that it's specified on the `TealiumConfig` `dispatchers` property:

`config.dispatchers = [Dispatchers.Collect]`

## Data Layer

The following variables are transmitted with each tracking call while the module is enabled:

| Variable         | Description                                                        | Example  |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | Static string to indicate which module the tracking call came from | `"collect"`       |
