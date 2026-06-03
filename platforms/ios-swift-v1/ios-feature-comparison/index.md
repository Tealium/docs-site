---
title: Feature comparison
description: Detailed list of feature comparison between iOS Objective-C and iOS Swift libraries.
url: https://docs.tealium.com/platforms/ios-swift-v1/ios-feature-comparison/
---This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](/platforms/ios-swift/).

The Tealium library for Swift is fully compatible with apps running pure Swift, Objective-C, or any combination of the two. Since it is the newest and most up-to-date library, we strongly recommend implementing the Swift library if possible.

The Objective-C library is still fully supported, but the Swift library generally updates faster and has the newest features. Additionally, Swift has the widest compatibility of all Tealium libraries, including support for server-side Swift environments.

Check the comparison table below to figure out which is most suitable for your needs.

## Memory Footprint &amp; Performance

All SDKs have some performance and memory impacts on your app. This varies between apps, and may be difficult to measure the exact footprint of a specific SDK.

We have measured the Tealium Swift SDK against a baseline of a standard blank iOS Single View app. These figures may vary for your specific implementation, so they only serve as a rough indicator.  All figures obtained using XCode Allocations Instrument.

**Compiled App Archive (`.ipa` file)**  

* 3&#43; MB (includes all modules)

**Runtime Memory Usage**  

* 2 - 2.5&#43; MB (Collect module and supporting modules)
* 7 - 10&#43; MB (Tag Management module, Collect module, and supporting modules)

**Startup Time**   

* ≈0.05 seconds (approximate time from initialization to completion callback firing)

## Swift Versions
* 4.0&#43; (Xcode 9.0&#43;)

## Operating Systems
* iOS 9.0&#43;
* tvOS 9.2&#43;
* macOS 10.11&#43;
* WatchOS 3.0&#43;

## Tealium Products
* Tealium iQ Tag Management
* Tealium EventStream
* Tealium AudienceStream
* Tealium DataAccess

## tealium-swift vs. tealium-ios
The Swift library was built from scratch on a completely new codebase to the [Objective-C library](https://github.com/Tealium/tealium-ios), and there are some subtle differences between the two libraries in terms of the current feature set. Below, we have compared the different features of both libraries. If you have requests for new features, feel free to open an issue on our GitHub page, or contact your account manager.


| Feature| TealiumIOS (Objective-C) | Tealium-Swift | Description | Notes |
|--------| ------------------------ | ------------- | ----------  | ----- |
| Instance Manager/Multiton                     | ✔                                | ✔                | Enables support for multiple Tealium instances (profiles) running in the same app.                 | May be added to Swift in a future release. Not a widely-used feature of the Objective-C library. Most customers do not need this feature.                                                                                                            |
| UI Auto Tracking                        |                                 | ✔                | Automatically tracks UIViews and Events                                                            | Available as an optional module, but not recommended due to additional performance overheads                                                                                                                                                                                                |
| Lifecycle Tracking                   | ✔                                | ✔                | Tracks App lifecycle events.                                                                       |                                                                                                                                                                                                                                                      |
| Tag Management                       | ✔                                | ✔                | Allows use of Tealium iQ through a non-rendered web view                                           |                                                                                                                                                                                                                                                      |
| Tealium Collect                      | ✔                                | ✔                | Sends data to Tealium Customer Data Hub using a native HTTPS request                                           |                                                                                                                                                                                                                                                      |
| Offline functionality/queuing        | ✔                                | ✔                | Automatically queues events if the device is online, and transmits when the device is online again |  |
| Remote Mobile Publish Settings (MPS) | ✔                               |  ✔               | Allows remote configuration of certain library settings                                            | Support added in version 1.9.0                                                                                                   |
| Volatile Data                        | ✔                                | ✔                | Stores data for the current session (until app is terminated)                                      |                                                                                                                                                                                                                                                      |
| Persistent Data                      | ✔                                | ✔                | Stores data between app launches                                                                   |                                                                                                                                                                                                                                                      |
| Remote Commands                      | ✔                                | ✔                | Allows triggering of specified native code blocks from Tealium iQ                                  |                                                                                                                                                                                                                                                      |
| Apple Search Ads Support             |                                 | ✔                | Adds support for the Apple Search Ads API to collect attribution data automatically                | Not planning to port to Objective-C                                                                                                                                                                                                                  |
| Optimizely Experiment Tracking       | ✔                                |                | Tracks Optimizely experiment data automatically                                                    | May port to Swift in future.                                                                                                                                                                                          |
| iOS Support                          | ✔                                | ✔                |                                                                                                   |                                                                                                                                                                                                                                                      |
| watchOS Support                      | ✔                                | ✔               |                                                                                                   |                                                                                                                                                                                                                                                      |
| tvOS Support                         | ✔                                | ✔                |                                                                                                   |                                                                                                                                                                                                                                                      |
| macOS Support                        |                                 | ✔                |                                                                                                   |                                                                                                                                                                                                                                                      |
| CocoaPods Support                    | ✔                                | ✔               | Support for the CocoaPods dependency manager                                                       |                                                                                                                                                                                                                                                      |
| Carthage Support                     | ✔                                | ✔                | Support for the Carthage dependency manager                                                        |                                                                                                                                                                                                                                                      |
| Swift Package Manager (SPM) Support                     |                                 | ✔                | Support for the Swift Package Manager dependency manager                                                        |                                                                                                                                                                                                                                                      |
| Source Code Available                |                                 | ✔                | May assist with debugging                                                                          |  
| Consent Manager                | ✔                                | ✔                | Assists with GDPR/privacy compliance                                                                          |
| Tealium Visitor Service API                | ✔                                |     ✔             | Provides callbacks for changes to a user&#39;s AudienceStream visitor profile
