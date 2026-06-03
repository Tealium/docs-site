---
title: tvOS
description: Learn to install Tealium for tvOS.
url: https://docs.tealium.com/platforms/ios-objective-c/tvos/
---
tvOS is no longer supported. The Tealium [iOS (Swift)](/platforms/ios-swift/) library is recommended.


## Requirements

* [Tealium Customer Data Hub account]()
* Xcode 7&#43;
* tvOS 9.0&#43;
* 100KB available space in `.ipa` file size
* [Bitcode compliant](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) framework 

## Sample Apps

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, it is recommended to download the [tvOS sample apps](https://github.com/Tealium/tealium-tvos/tree/master/Samples).

To abstract the Tealium implementation from the rest of your app, we recommend the use of the [sample helper class](https://github.com/Tealium/tealium-tvos/blob/master/Samples/tvOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift). This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single header/method file.


## Install

Install and manage Tealium dependencies for tvOS with CocoaPods. 

1. Add the following dependency to your Podfile:
    ```perl
    pod &#39;TealiumTVOS&#39;
    ```

2. Download and install [Tealium for tvOS](https://github.com/Tealium/tealium-tvos).
    We recommend cloning the library (instead of downloading) to make it easier to update to future releases.  

3. Add `TealiumTVOS.framework` to your project&#39;s tvOS Extension target, and copy the framework to the project in the resulting dialog box.

4. In the target&#39;s **General: Embedded Binaries** section, add the framework:    
    ```perl
    TealiumTVOS.framework
    ```

## Initialize

In the Application Delegate, or within a helper class setup method, invoke a Tealium instance with the following code:



```swift
let config = TEALConfiguration.init(account: &#34;ACCOUNT&#34;,
                      profile: &#34;PROFILE&#34;,
                      environment: &#34;ENV&#34;,
                      datasource: &#34;DATASOURCE&#34;)

guard let tealium = Tealium.newInstanceForKey(&#34;uniqueInstanceKey&#34;, configuration: config) else {
    // Any additional failure response here
    return
}
```


```objc
TEALConfiguration *configuration = [TEALConfiguration
                      configurationWithAccount:@&#34;ACCOUNT&#34;
                      profile:@&#34;PROFILE&#34;
                      environment:@&#34;ENV&#34;,
                      datasource:@&#34;DATASOURCE&#34;];

Tealium *tealiumInstance1 = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:configuration]; 
```



| Parameter | Description | Example |
|-----------|-------------|  ---- |
| `account`   | Tealium account name |`&#34;companyXYZ&#34;` |
| `profile`   | Tealium profile name | `&#34;main&#34;` |
| `environment` | Tealium environment name  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` | (Optional) data source key  | `&#34;abc123&#34;`|
| `instance` | Unique Tealium instance identifier  (multiple instances are supported) | `&#34;tealium_main&#34;` |

## Track Views

Track screen views by calling [`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) with two parameters: the name of the screen and (optionally) contextual view data.

In any UIViewController&#39;s [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) method: 



```swift
Tealium.instanceForKey(&#34;uniqueInstanceKey&#34;)?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [:])
```


```objc
[[Tealium instanceForKey:@&#34;INSTANCE&#34;] trackViewWithTitle:NSStringFromClass([self class]) dataSources:nil];
```



The screen name is populated in the event data as `screen_title`.

## Track Events

Track non-view events by calling [`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) with two parameters: an event name and (optionally) contextual event data. 



```swift
Tealium.instanceForKey(&#34;INSTANCE&#34;)?.trackEventWithTitle(&#34;EVENT_NAME&#34;, dataSources: [:])
```


```objc
[[Tealium instanceForKey:@&#34;INSTANCE&#34;] trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:nil];
```



The event name is populated in the event data as `tealium_event`.


## API Reference

See the [TealiumTVOS Reference API](http://tealium.github.io/tealium-tvos/) for a complete list of classes and methods.
