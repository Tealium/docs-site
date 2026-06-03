---
title: Install
description: Learn to install the Tealium SDK for iOS (Objective-C).
url: https://docs.tealium.com/platforms/ios-objective-c/install/
---
This section covers the previous iOS library, Objective-C. [Swift](/platforms/ios-swift/) is the preferred programming language for macOS, iOS, watchOS, tvOS and beyond. Swift code co-exists along side your existing Objective-C files in the same project, with full access to your Objective-C API, making it easy to adopt.

## Requirements

* Xcode 7.0&#43;
* iOS 8.1&#43;
* [Tealium iQ Mobile Profile]()
* [Tealium Customer Data Hub account]()

## Sample Apps

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, explore the Tealium for iOS [sample apps](https://github.com/Tealium/tealium-ios/tree/master/Samples).

To abstract the Tealium implementation from the rest of your app, we recommend the use of a `TealiumHelper` class. This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single `ViewController` or header/method file.

- [TealiumHelper for Objective-C](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_ObjC/UIKitCatalog/TealiumHelper.m)
- [TealiumHelper for Swift](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift)

See the [TealiumIOS API](https://tealium.github.io/tealium-ios/) for a complete listing of Tealium classes and methods for iOS.

## Install

Install the Tealium SDK for iOS (Objective-C) with CocoaPods, Carthage, or manually.

### CocoaPods

To install Tealium for iOS (Objective-C) for your app with CocoaPods (Recommended):

1. Add the following dependency to your Podfile:
      ```perl
      pod &#34;TealiumIOS&#34;
      ```

2. Save the file and run the following in your project directory:

      ```perl
      pod install --repo-update
      ```

3. Use the created `.xcworkspace` file to continue building your app. If you do not use the `.xcworkspace` file, you are not able to build the app correctly.

### Carthage

To install Tealium for iOS (Objective-C) for your app with Carthage:

1.  Add the following to your Cartfile:  
      ```perl
      github &#34;tealium/tealium-ios&#34;
      ```

2. To download and extract the frameworks, run the following command:  
      ```perl
      carthage update --platform ios --use-xcframeworks
      ```
      Be sure to use the `--use-xcframeworks` flag, or the build will fail. This requires [Carthage 0.38.0](https://github.com/Carthage/Carthage/releases/tag/0.38.0).

3. For the required frameworks to be copied automatically at build-time, verify sure that Carthage is [properly integrated](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) into your Xcode project. 

### Manual

To install Tealium for iOS (Objective-C) for your app manually:

1.  Add `TealiumIOS.xcframework` to your project.

2.  Copy framework to project in the resulting dialog box.

3.  In the Target go to **General &gt; Frameworks, Libraries &amp; Embedded Content** and add `TealiumIOS.xcframework` with the &#34;Embed &amp; Sign&#34; option selected.
For Swift projects go to the **Build Settings &gt; Swift Compiler &gt; Objective-C Bridging Header** option and include the file `TealiumIOSBridgingHeader.h`. 


## Initialize

In the Application Delegate or within a helper class setup method use the following initialization code:  



```swift
// set your account, profile, and environment
let tealConfig = TEALConfiguration.init(account: &#34;ACCOUNT&#34;,
                                        profile: &#34;PROFILE&#34;,
                                    environment: &#34;ENVIRONMENT&#34;,
                                     datasource: &#34;DATASOURCE&#34;)

// Initialize with a unique key for this instance
guard let tealium = Tealium.newInstanceForKey(&#34;INSTANCE&#34;, configuration: tealConfig) else {
     // Any additional failure response here           
     return
}
```



```obj-c
// import area
@import TealiumIOS;

// Set your account, profile, and environment
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34;
                          profile:@&#34;PROFILE&#34;
                          environment:@&#34;ENVIRONMENT&#34;
                          datasource:@&#34;DATASOURCE&#34;];

// Initialize with a unique key for this instance
Tealium *tealium = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:tealConfig]; 
```



The log level is set by default from the publish settings from your iQ account. To override this setting set the `logLevel` property in the TEALConfiguration instance:



```swift
// Set the log verbosity to errors only
tealConfig.logLevel = .prod
```



```obj-c
// Set the log verbosity to maximum
[tealConfig setLogLevel: TEALLogLevelDev];
```



The Tealium instance must be configured with the following parameters before it begins tracking:

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name | `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealium profile name  | `&#34;main&#34;`  |
| `environment` | `String` |Tealium environment name  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` | `String` |(Optional) data source key | `&#34;abc123&#34;` |
| `instance` | `String` |Unique name for your instance (multiple instances are supported)  | `&#34;tealium_main&#34;` |
