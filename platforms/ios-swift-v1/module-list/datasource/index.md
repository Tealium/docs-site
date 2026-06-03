---
title: DataSource Module
description: Adds the data source variable to each dispatch.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/datasource/
---
## Usage

If you are using Swift 1.8.0&#43;, this module is already included in the Core and you do not need to install it. For prior version, follow this guide to install the module. 

The DataSource Module adds the data source variable to each dispatch.

Usage of this module is recommended if you are using the Tealium Customer Data Hub. Generate a data source key with the Customer Data Hub user interface. If you are using Tag Management only, it currently doesn&#39;t have any effect, apart from adding a new variable to each dispatch. [Learn more]() about Data Sources.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the DataSource module with CocoaPods or Carthage.

### CocoaPods

To install the DataSource module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod &#39;tealium-swift/TealiumDataSource&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.



### Carthage

To install the DataSource module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumDataSource.framework
      ```
3. To allow the datasource parameter to be set on the `TealiumConfig` class instance, add the following required import statement to your project:   
      ```swift
      import TealiumDataSource
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.


## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable           | Type | Description                                          | Example  |
|--------------------|-------|---------------------------------------------------|---------------|
| `tealium_datasource` | `String` | Specifies the data source name. Added to every dispatch. | `&#34;abc123&#34;`      |

## API Reference
No public API methods available. The Data Source variable is set by the TealiumConfig object (see [Swift Class: TealiumConfig](/platforms/ios-swift-v1/api/tealium-config/))


## Release Notes

Build 1

* Initial release
