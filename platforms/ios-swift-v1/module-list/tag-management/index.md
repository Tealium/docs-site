---
title: TagManagement Module
description: A client-side implementation of the Universal Tag (utag.js) which uses a non-rendered WKWebView instance to execute JavaScript.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/tag-management/
---
## Usage

The TagManagement module is a client-side implementation of the Universal Tag (`utag.js`) which uses a non-rendered `WKWebView` instance to execute JavaScript. This module is required in apps that make use of Tealium iQ Tag Management. It is automatically included in Carthage and CocoaPods framework builds.

## Supported Platforms

* iOS


## Requirements

* WebKit (WKWebView)

## Install

Install the TagManagement module with CocoaPods or Carthage.

### CocoaPods

To install the TagManagement module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod &#39;tealium-swift/TealiumTagManagement&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the TagManagement module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumTagManagement.framework
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call:

| Variable         | Type | Description                                                        | Example  |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | Static string to indicate which module the tracking call came from | `&#34;tagmanagement&#34;` |

## Public API
The WKWebView protocols are accessible by adding another object conforming the `WKWebView` delegate to the module&#39;s multicast delegate:

```swift
tealium.tagManagement()?.delegates.add(MY_OBJECT)
```

## About WKWebView

Prior to version 1.7.0, this module used `UIWebView` which is now deprecated in favor of `WKWebView`. The OS requires that `WKWebView` always be attached to a `UIView`, even if it is not rendered. If it is not attached to a UIView, the OS severely throttles the performance and the JavaScript executes suboptimally. **To accommodate this the Tag Management module attempts to attach the non-rendered WKWebView to the root UIView of your app.**

If your app has a complex view hierarchy and the module cannot detect the `rootViewController`, initialize [TealiumConfig](/platforms/ios-swift-v1/api/tealium-config/) with a view to attach to in `viewDidLoad`, `viewWillAppear:`, or `viewDidAppear:`.

Release 1.7.1 significantly improves the auto-detection of views and removes the need to specify a view in most scenarios. But you must test this in your app to verify that tracking calls are sent correctly. See [Release Notes](/platforms/ios-swift-v1/release-notes/) for full details.

If your app jumps to a `UIViewController` upon receiving a push notification, and has a different view hierarchy than when Tealium was initialized, you must update the current `UIView` using the following API method.

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    // this view does not have a navigation controller
    if self.navigationController == nil {
          // update the current root UIView on the Tealium instance
        tealium?.updateRootView(self.view)
    }
    // Do any additional setup after loading the view.
}
```

See the sample app [Swift-WKWebView](https://github.com/Tealium/tealium-swift/tree/master/samples/Swift-WKWebView) for a full example.

`WKWebView` and `UIWebView` use different methods to store cookies (`WKHTTPCookieStore` and `HTTPCookieStorage` respectively), so the module automatically synchronizes cookies the first time that WKWebView is launched. The cookies in `HTTPCookieStorage` are not deleted, but eventually expire on their own.

The [`shouldAddCookieObserver`](/platforms/ios-swift-v1/api/tealium-config/#shouldaddcookieobserver) method lets you use your own cookie observer during cookie synchronization, which requires a cookie observer to retrieve cookies on the main thread after setting them. This issue is caused by bugs in `WKWebView`, which prevents your own observer from being called.   
