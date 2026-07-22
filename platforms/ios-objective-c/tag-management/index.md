---
title: Tag Management
description: Learn how tag management is implemented as a non-rendered WKWebView instance to execute the Universal Tag (utag.js) JavaScript client-side.
url: https://docs.tealium.com/platforms/ios-objective-c/tag-management/
---
This tag management feature lets you integrate JavaScript based vendor tags into your app and manage them remotely using Tealium iQ, similarly to a website.

## How It Works

Once you have [created a mobile profile in Tealium iQ](https://docs.tealium.com/creating-a-mobile-profile/) with Tag Management enabled, when you initialize the Tealium instance in your app, a non-rendered web view is created to load a simple HTML file from Tealium  in which to load the Universal Tag `utag.js`. This web view is never rendered to the user.

* Versions 5.5.0 and newer, running iOS 11.0 and newer use [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview?language=objc).
* Versions 5.4.x and older, running iOS 10.0 and older use [UIWebView](https://developer.apple.com/documentation/uikit/uiwebview).


<blockquote>
If you are supporting iOS versions lower than iOS 11.0 and would still like to use WKWebView, then upgrade to version 5.5.0 or newer. The caveat is that your visitor_id and other cookies will be reset. This is because the [WKHTTPCookieStore](https://developer.apple.com/documentation/webkit/wkhttpcookiestore) is only supported in iOS 11.0
</blockquote>



### Sample

To better familiarize yourself with Tealium's `WKWebView`, explore the [WKWebView sample](https://github.com/Tealium/tealium-ios/tree/master/Samples/iOS_WKWebView%2BTealium_Objc).

### Usage

`WKWebView` is required to be attached to a `UIView`, even if it is not rendered. To accommodate this the Tealium SDK attempts to attach the non-rendered `WKWebView` to the `rootViewController.view`, the most common scenario when your window's `rootViewController` is a subclass of `UIViewController` or one of Apple's container view controllers (`UINavigationController` or `UITabBarController`).

If your app has a complex view hierarchy, set the `TEALConfiguration` instance with a view to attach to in `viewDidLoad`, `viewWillAppear:`, or `viewDidAppear:`.

```obj-c
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@"ACCOUNT"
                                              profile:@"PROFILE"
                                              environment:@"ENVIRONMENT"
                                              datasource:@"DATASOURCE"];
tealConfig.view = <UIVIEW>; // For example, self.view in a UIViewController subclass
// Initialize with a unique key for this instance
Tealium *tealium = [Tealium newInstanceForKey:@"INSTANCE" configuration:tealConfig]; 
```

| Parameters    | Type     | Description                                        | Example        |
|:--------------|:---------|:---------------------------------------------------|:---------------|
| `account`     | `String` | Tealium account name                               | `"companyXYZ"` |
| `profile`     | `String` | Tealium profile name                               | `"main" `      |
| `environment` | `String` | Tealium environment name                           | `"prod"`       |
| `datasource`  | `String` | (Optional) data source key (Set to `null` if none) | `"abc123"`     |


Upon receiving a push notification, if your app jumps to a `UIViewController` and has a different view hierarchy than when Tealium was initialized, you must remove the old instance of Tealium and create a new one with the view to attach to. The sample app shows an example of this in [`GreenViewController.m`](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/GreenViewController.m) and [TealiumHelper.m](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/TealiumHelper.m).


Although the Objective-C SDK is currently closed source, to provide more context, this following code snippet shows how the web view is created.

```obj-c
- (UIView *_Nullable)webViewContainer {
    if (!_webViewContainer) {
        UIWindow *window = [[UIApplication sharedApplication] keyWindow];
        UIViewController *rootViewController = window.rootViewController;
        UIViewController *topViewController;

        if ([rootViewController isKindOfClass:[UINavigationController class]]) {
            topViewController = [((UINavigationController *)rootViewController).viewControllers lastObject];
        } else if ([rootViewController isKindOfClass:[UITabBarController class]]) {
            topViewController = ((UITabBarController *)rootViewController).selectedViewController;
        } else {
            topViewController = rootViewController;
        }

        UIView *view = topViewController.viewIfLoaded;
        if (view) {
            self.webViewContainer = view;
        }
    }
    return _webViewContainer;
}
```

The view is only used once to initialize the `WKWebView`.

## `TealiumConfig`

### `WKProcessPool`

If you use a `WKWebView` webview in your app, create and retain a singleton `WKProcessPool` instance and set it prior to instantiating Tealium. This also prevents cookie synchronization issues if your app contains other webviews besides the Tealium Tag Management webview.

```obj-c
WKProcessPool *wkProcessPool = [[WKProcessPool alloc] init];
```

Example:   

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@"ACCOUNT" profile:@"PROFILE" environment:@"ENV"];
_configuration.wkProcessPool = MyApp.wkProcessPool;

self.tealium = [Tealium newInstanceForKey:@"INSTANCE_KEY" configuration:_configuration];
```

### `WKWebviewConfiguration`

Permits a custom `WKWebviewConfiguration` object to be passed, which is used by the Tealium Tag Management webview. If using this option instead of `webviewProcessPool` option, set the singleton `WKProcessPool` through the customizable `WKWebviewConfiguration` `processPool` property.


<blockquote>
It is recommended to use this option as it may be required if future API changes are made to `WKWebView`.
</blockquote>


Example:   

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@"ACCOUNT" profile:@"PROFILE" environment:@"ENV"];

WKWebviewConfiguration *webviewConfiguration = [[WKWebViewConfiguration alloc] init];
webviewConfiguration.processPool = MyApp.wkProcessPool;
_configuration.wkWebViewConfig = webviewConfiguration

self.tealium = [Tealium newInstanceForKey:@"INSTANCE_KEY" configuration:_configuration];
```
