---
title: AppData Module
description: Gathers important information about the app bundle.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/appdata/
---
## Usage
The AppData module gathers important information about the app bundle. Usage of this module is recommended, but not mandatory. If you choose to exclude it, the data layer variables are not included in tracking calls.

The following platforms are supported:

* iOS
* macOS
* watchOS
* tvOS

## Install

Install the AppData module with CocoaPods or Carthage.

### CocoaPods

To install the AppData module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod &#39;tealium-swift/TealiumAppData&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the AppData module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumAppData.framework
    ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable         | Description                              | Example                         |
|----------------------|--------------------------------------|---------------------------------|
| `app_build`           | Minor build version of the app| `&#34;2213&#34;`                                 |
| `app_name`            | Name of the app (usually same as App Store name)| `&#34;Digital Velocity&#34;`   |
| `app_rdns`            | Fully-qualified name of the app bundle| `&#34;com.tealium.digitalvelocity&#34;`          |
| `app_uuid`            | Random uuid. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled.  | `123e4567-e89b-12d3-a456-&#34;426655440000&#34;` |
| `app_version`         | Version of the app bundle                                                                                                                                   | `&#34;1.0&#34;`                                  |
| `tealium_visitor_id`         | Persistent Tealium visitor ID                                                                                                                               | `&#34;123e4567e89b12d3a456426655440000&#34;`     |
