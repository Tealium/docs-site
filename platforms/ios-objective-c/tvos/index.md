---
title: tvOS
description: Learn to install Tealium for tvOS.
url: https://docs.tealium.com/platforms/ios-objective-c/tvos/
---

<blockquote>
tvOS is no longer supported. The Tealium [iOS (Swift)](https://docs.tealium.com/platforms/ios-swift/) library is recommended.
</blockquote>



## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Xcode 7+
* tvOS 9.0+
* 100KB available space in `.ipa` file size
* [Bitcode compliant](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) framework 

## Sample Apps

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, it is recommended to download the [tvOS sample apps](https://github.com/Tealium/tealium-tvos/tree/master/Samples).

To abstract the Tealium implementation from the rest of your app, we recommend the use of the [sample helper class](https://github.com/Tealium/tealium-tvos/blob/master/Samples/tvOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift). This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single header/method file.


## Install

Install and manage Tealium dependencies for tvOS with CocoaPods. 

1. Add the following dependency to your Podfile:
    ```perl
    pod 'TealiumTVOS'
    ```

2. Download and install [Tealium for tvOS](https://github.com/Tealium/tealium-tvos).
    
<blockquote>
We recommend cloning the library (instead of downloading) to make it easier to update to future releases.
</blockquote>
  

3. Add `TealiumTVOS.framework` to your project's tvOS Extension target, and copy the framework to the project in the resulting dialog box.

4. In the target's **General: Embedded Binaries** section, add the framework:    
    ```perl
    TealiumTVOS.framework
    ```

## Initialize

In the Application Delegate, or within a helper class setup method, invoke a Tealium instance with the following code:



```swift
let config = TEALConfiguration.init(account: "ACCOUNT",
                      profile: "PROFILE",
                      environment: "ENV",
                      datasource: "DATASOURCE")

guard let tealium = Tealium.newInstanceForKey("uniqueInstanceKey", configuration: config) else {
    // Any additional failure response here
    return
}
```


```objc
TEALConfiguration *configuration = [TEALConfiguration
                      configurationWithAccount:@"ACCOUNT"
                      profile:@"PROFILE"
                      environment:@"ENV",
                      datasource:@"DATASOURCE"];

Tealium *tealiumInstance1 = [Tealium newInstanceForKey:@"INSTANCE" configuration:configuration]; 
```



| Parameter | Description | Example |
|-----------|-------------|  ---- |
| `account`   | Tealium account name |`"companyXYZ"` |
| `profile`   | Tealium profile name | `"main"` |
| `environment` | Tealium environment name  | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` | (Optional) data source key  | `"abc123"`|
| `instance` | Unique Tealium instance identifier  (multiple instances are supported) | `"tealium_main"` |

## Track Views

Track screen views by calling [`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) with two parameters: the name of the screen and (optionally) contextual view data.

In any UIViewController's [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) method: 



```swift
Tealium.instanceForKey("uniqueInstanceKey")?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [:])
```


```objc
[[Tealium instanceForKey:@"INSTANCE"] trackViewWithTitle:NSStringFromClass([self class]) dataSources:nil];
```




<blockquote>
The screen name is populated in the event data as `screen_title`.
</blockquote>


## Track Events

Track non-view events by calling [`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) with two parameters: an event name and (optionally) contextual event data. 



```swift
Tealium.instanceForKey("INSTANCE")?.trackEventWithTitle("EVENT_NAME", dataSources: [:])
```


```objc
[[Tealium instanceForKey:@"INSTANCE"] trackEventWithTitle:@"EVENT_NAME" dataSources:nil];
```




<blockquote>
The event name is populated in the event data as `tealium_event`.
</blockquote>



## API Reference

See the [TealiumTVOS Reference API](http://tealium.github.io/tealium-tvos/) for a complete list of classes and methods.
