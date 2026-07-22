---
title: Logger Module
description: Enables logging of debug information to the LLDB console.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/logger/
---
## Usage

The Logger module enables logging of debug information to the LLDB console.

Usage of this module is recommended. If you do not enable it, then there is no logging from the Tealium library.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the Logger module with CocoaPods or Carthage.

### CocoaPods

To install the Logger module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumLogger'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the Logger module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumLogger.framework
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
No new variables are introduced by this module.

## API Reference
There are no public API methods for this module. Control the module by using the settings available in the `TealiumConfig` object.

## Log Levels

The following log levels are available:

| Log Level | Description                                                                         | Enum value                    |
|-----------|-------------------------------------------------------------------------------------|-------------------------------|
| `None`      | Logging disabled.                                                                | `TealiumLogLevelValue.none`    |
| `Errors`    | Only errors are reported.                                                        | `TealiumLogLevelValue.errors`   |
| `Warnings`  | Only errors and warnings are reported.                                           | `TealiumLogLevelValue.warnings` |
| `Verbose`   | All log output are reported, including an entry for each tracking call/dispatch. | `TealiumLogLevelValue.verbose`  |
