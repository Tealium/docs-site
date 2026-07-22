---
title: FileStorage Module
description: Provides persistent data storage, backed by the FileManager/NSKeyedArchiver APIs.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/file-storage/
---
## Usage


<blockquote>
If you are using Swift 1.8.0+, this module is already included in the Core and you do not need to install it. For prior version, follow this guide to install the module.
</blockquote>


The FileStorage module provides persistent data storage, backed by the `FileManager`/`NSKeyedArchiver` APIs. This module must be used in conjunction with the Swift Module: [PersistentData](https://docs.tealium.com/platforms/ios-swift-v1/module-list/persistent-data/).

If you are using the Persistent Data module (Recommended), you must also use either the File Storage or Defaults Storage module to make the data persist across app launches. Whether you choose Defaults Storage over File Storage is personal choice. If both FileStorage and DefaultsStorage are included and enabled, FileStorage takes precedence and DefaultsStorage effectively becomes inactive.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the FileStorage module with CocoaPods or Carthage.

### CocoaPods

To install the FileStorage module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumFileStorage'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. It also bundles the PersistentData module. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the FileStorage module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumFileStorage.framework
      ```
3. To access the PersistentData API on the `Tealium` instance, add the following required import statement to your project:   
      ```swift
      import TealiumFileStorage
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. It also bundles the PersistentData module. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.


## Data Layer
No additional variables are introduced by this module.

## API Reference
There are no public API methods for this module. Successes and failures may be monitored through the Delegate module.

## Release Notes

Build 1.4.0

* Fixed bug that caused data not to be persisted to disk due to permissions error
