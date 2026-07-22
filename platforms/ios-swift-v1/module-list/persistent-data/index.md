---
title: PersistentData Module
description: Allows data variables to be stored on disk, and automatically adds them to each dispatch/tracking call.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/persistent-data/
---
## Usage

The PersistentData module stores variables on disk and automatically includes them in each tracking call. Usage of this module is recommended.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the PersistentData module with CocoaPods or Carthage.

### CocoaPods

To install the PersistentData module with CocoaPods, add the following to your Podfile:

```ruby
pod 'tealium-swift/TealiumPersistentData'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.



### Carthage

To install the PersistentData module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:

      ```ruby
      TealiumPersistentData.framework
      ```  
3. Add the following import statement to your helper file:  

      ```swift  
      import TealiumPersistentData
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## API Reference

See the [`TealiumPersistentData`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-persistent-data/) class in the iOS (Swift) API.
