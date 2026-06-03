---
title: watchOS
description: Learn to install Tealium for watchOS.
url: https://docs.tealium.com/platforms/ios-objective-c/watchos/
---## Requirements

* Xcode 7&#43;
* iOS 8.1&#43;
* watchOS 2.0&#43;
* [Tealium for iOS](/platforms/ios-swift/) installed in the host app
* 400KB available space in `.ipa `file size (this accounts for the `tealium-ios` library needed in the host app)
* [Bitcode compliant](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) framework

## Sample Apps

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, it is recommended to download the sample apps:

- [Objective-C WatchOS sample app](https://github.com/Tealium/tealium-ios/tree/master/Samples/WatchOS_Catalog%2BTealium_ObjC)
- [Swift WatchOS sample app](https://github.com/Tealium/tealium-ios/tree/master/Samples/WatchOS_Sample_Swift)

To abstract the Tealium implementation from the rest of your app, we recommend the use of the [sample helper class](https://github.com/Tealium/tealium-ios/blob/master/Samples/WatchOS_Catalog%2BTealium_ObjC/WatchKit%20Catalog/Tealium/TealiumHelper.m). This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single header/method file.


## Install

Install Tealium for watchOS as an extension application where `TealiumIOS.framework` has been implemented in the host application. 


1. Add `TealiumWATCHOSExtension.framework` to your project&#39;s watchOS Extension target, and copy the framework to the project in the resulting dialog box.

2. In the target&#39;s **General: Embedded Binaries** section, add the framework:  
    ```perl
    TealiumWATCHOSExtension.framework
    ```  
For Swift projects, add `&lt;TealiumWATCHOSExtension/TEALWKExtension.h&gt;` to your bridging header file.  

3. Make sure all paths are as expected under **Projects: Target: Build Settings**. 


## Initialize

Once Tealium for watchOS is added to your project you are ready to start coding.

In the Application Delegate, or within a helper class setup method, add the following code to initialize the Tealium instance: 



```swift
// Get Tealium instance
let config = TEALWKExtensionConfiguration.configuration()
guard let tealium = TEALWKExtension.newInstanceForKey(&#34;[INSTANCE]&#34;) else {
    // Any additional failure response here
    return
}
```


```objc
// Import area
#import &lt;TealiumWATCHOSExtension/TealiumWATCHOS.h&gt;

// Within a setup method
TEALWKExtensionConfiguration *config = [TEALWKExtensionConfiguration configuration];
config.logLevel = TEALLogLevelDev;
[TEALWKExtension newInstanceForKey:@&#34;[INSTANCE]&#34; configuration:config]; 
```




## Track Views

Track screen views by calling [`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) with two parameters: the name of the screen and (optionally) contextual view data.

In any UIViewController&#39;s [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) method, use this code:




```swift
TEALWKExtension.instanceForKey(&#34;[hostTealiumInstanceKey]&#34;)?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [String:String]())
```


```objc
[[TEALWKExtension instanceForKey:@&#34;[INSTANCE]&#34;] trackViewWithTitle:NSStringFromClass([self class]) dataSources:@{}];
```



## Track Events

Track non-view activity by calling [`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) with two parameters: an event name and (optionally) contextual event data. 

In any method that triggers or responds to an event trigger, use this code: 



```swift
TEALWKExtension.instanceForKey(&#34;[INSTANCE]&#34;)?.trackEventwWithTitle(&#34;EVENT_NAME&#34;), dataSources: [String:String]())
```


```objc
[[Tealium instanceForKey:@&#34;[INSTANCE]&#34;] trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:@{@&#34;optionalKey&#34;:@&#34;optionalValue&#34;}];
```


