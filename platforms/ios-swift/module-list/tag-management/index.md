---
title: TagManagement Module
description: A client-side implementation of the Universal Tag (utag.js) which uses a non-rendered WKWebView instance to execute JavaScript.
url: https://docs.tealium.com/platforms/ios-swift/module-list/tag-management/
---
## Usage

The TagManagement module is a client-side implementation of the Universal Tag (`utag.js`) which uses a non-rendered `WKWebView` instance to execute JavaScript. This module is required in apps that make use of Tealium iQ Tag Management. It is automatically included in Carthage and CocoaPods framework builds.

## Supported Platforms

* iOS

## Requirements

* WebKit (WKWebView)

## Install

Install the TagManagement module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0&#43;, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `TagManagement` module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

### CocoaPods

To install the TagManagement module with CocoaPods, add the following pod to your Podfile:  
```perl
pod &#39;tealium-swift/TagManagement&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the TagManagement module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumTagManagement.framework
      ```
Learn more about the [Carthage installation for iOS](/platforms/ios-swift/install/#carthage).

## Initialize

To initialize the module, verify that it&#39;s specified on the `TealiumConfig` [`collectors`](/platforms/ios-swift/api/tealium-config/#collectors) property

`config.dispatchers = [Dispatchers.TagManagement]`

## Customizing the WebView Settings

### App Bound Domains

If your app uses the [WKAppBoundDomains](https://webkit.org/blog/10882/app-bound-domains/) feature to limit which domains webviews in your app can communicate with, you must pass a custom `WKWebViewConfiguration` and set its `limitsNavigationsToAppBoundDomains` property to `true`. Failing to do this will result in all tracking calls being dropped by the operating system. You must also include &#34;tags.tiqcdn.com&#34; in your `Info.plist`&#39;s `WKAppBoundDomains` list, as well as the domains for any tags you have set up in Tealium iQ (for example &#34;google-analytics.com&#34;). Be aware that a maximum of 10 domains can be configured for the entire app, so if you use multiple client-side tags, you may easily exceed this.

```
 let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)
 config.dispatchers = [Dispatchers.TagManagement]
 let wkWebViewConfiguration = WKWebViewConfiguration()
 wkWebViewConfiguration.limitsNavigationsToAppBoundDomains = true
 config.webviewConfig = wkWebViewConfiguration
 tealium = Tealium(config: config)
        
```

### Process Pool

If your app uses its own `WKWebView`, to avoid cookie synchronization issues, pass a singleton `WKProcessPool` instance to be used by the Tealium webview, or a custom `WkWebViewConfiguration` that&#39;s shared with other webviews in your app. 

Learn about [webviewProcessPool](/platforms/ios-swift/api/tealium-config/#webviewprocesspool) and [webViewConfig](/platforms/ios-swift/api/tealium-config/#webviewconfig).

## Data Layer
The following variables are transmitted with each tracking call:

| Variable         | Type | Description                                                        | Example  |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | Static string to indicate which module the tracking call came from | `&#34;tagmanagement&#34;` |


## About WKWebView

Prior to version 1.7.0, this module used `UIWebView` which is now deprecated in favor of `WKWebView`. The OS requires that `WKWebView` always be attached to a `UIView`, even if it is not rendered. If it is not attached to a UIView, the OS severely throttles the performance and the JavaScript executes suboptimally. **To accommodate this the Tag Management module attempts to attach the non-rendered WKWebView to the root UIView of your app.**

If your app has a complex view hierarchy and the module is not detecting the `rootViewController`, initialize [TealiumConfig](/platforms/ios-swift/api/tealium-config/) with a view to attach to in `viewDidLoad`, `viewWillAppear:`, or `viewDidAppear:`.

Release 1.7.1 significantly improves the auto-detection of views and removes the need to specify a view in most scenarios. But you must test this in your app to verify that tracking calls are sent correctly. See [Release Notes](/platforms/ios-swift/release-notes) for full details.

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

The [`shouldAddCookieObserver`](/platforms/ios-swift/api/tealium-config/#shouldaddcookieobserver) method lets you use your own cookie observer during cookie synchronization, which requires a cookie observer to retrieve cookies on the main thread after setting them. This issue is caused by bugs in `WKWebView`, which prevents your own observer from being called.   
