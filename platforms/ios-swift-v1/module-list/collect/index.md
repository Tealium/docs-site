---
title: Collect Module
description: Dispatches tracking calls to Tealium Customer Data Hub.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/collect/
---
## Usage
The Collect module dispatches tracking calls to Tealium Customer Data Hub. Usage of this module is strongly recommended if you are using Customer Data Hub.

As an alternative, if you are using the Tag Management module, you may instead use the Collect tag with Tealium iQ. This may give greater control over the data and events dispatched to the Customer Data Hub, as you may then use load rules and extensions to manipulate the data prior to dispatch. If you are using the Collect tag with Tealium iQ, ensure that the Collect module is disabled to avoid duplicate tracking requests.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the Collect module with CocoaPods or Carthage.

### CocoaPods

To install the Collect module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumCollect'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the Collect module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumCollect.framework
    ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable         | Description                                                        | Example  |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | Static string to indicate which module the tracking call came from | `"collect"`       |
