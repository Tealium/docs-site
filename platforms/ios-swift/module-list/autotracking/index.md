---
title: AutoTracking Module
description: Track screen views automatically.
url: https://docs.tealium.com/platforms/ios-swift/module-list/autotracking/
---
The AutoTracking module adds automatic tracking of screen views to your app with only a minimal amount of additional code.

The following platforms are supported:
* iOS
* tvOS
* watchOS
* macOS

## How It Works

Add the AutoTracking module to your build and initialization to take advantage of automatic screen view tracking. The module has several options to control which screens are tracked and how they are named.

The AutoTracking module supports two modes of tracking:

* **Full Tracking**
  * UIKit - Tracks all screen views automatically, with the option to omit screens using the block list.
  * SWiftUI - Not supported.
* **Partial Tracking**
  * UIKit - For each view to track, create a subclass of the view controller.
  * SwiftUI - For each view to track, either create a view modifier or embed the view in the Tealium tracking container.
  
### Full Tracking

Full tracking is only available in a UIKit app.

In UIKit, the AutoTracking module uses method swizzling on the `viewDidAppear` instance method of `ViewController`. The name of the tracked event is set to the `UIViewController.title` property or, if that&#39;s not available, is set to the `UIViewController` class name after removing the &#34;ViewController&#34; suffix.

### Partial Tracking

Use partial tracking for more control over automatic tracking and to optimize performance. This approach uses annotations in your `ViewController` code to only track the views you need. This approach is not dependent on any particular app design paradigm and it works with a UIKit app or a SwiftUI app.

### Block List

Use the block list feature in the full tracking mode to suppress specific tracking calls.
The block list is a JSON file that contains a single array of strings. The strings represent views to omit from automatic tracking. If a string in the block list appears anywhere in the view controller name, it will not be tracked. The string comparisons are case-insensitive.

For example, if you don&#39;t want to track any view controller names that contain the strings &#34;Settings&#34; or &#34;Profile&#34;, then the block list could contain:

```json
[
  &#34;settings&#34;, &#34;profile&#34;
]
```

The block list file can be stored locally in your app or hosted remotely as a URL.

Use the one of the following `TealiumConfig` properties to use a block list:

* [`autoTrackingBlocklistFilename`](/platforms/ios-swift/api/tealium-config/#autotrackingblocklistfilename)
* [`autoTrackingBlocklistUrl`](/platforms/ios-swift/api/tealium-config/#autotrackingblocklisturl)


## Requirements

* `UIKit` or `SwiftUI`
* `UIApplication`

## Install

Install the AutoTracking module with CocoaPods or Carthage.

### CocoaPods

To install the AutoTracking module with CocoaPods, add the following pod to your Podfile:  
```perl
pod &#39;tealium-swift/Autotracking&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the AutoTracking module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumAutotracking.framework
      ```

Learn more about the [Carthage installation for iOS](/platforms/ios-swift/install/#carthage).

## Initialize

To initialize the AutoTracking module, add it to the [`TealiumConfig.collectors`](/platforms/ios-swift/api/tealium-config/#collectors) property.

```swift
config.collectors = [Collectors.Autotracking]
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Partial Tracking Setup

### UIKit

In a UIKit app, use the following methods to implement partial tracking but modifiying only the view controllers that you want to track.

To turn off full tracking and add partial tracking, first add the entry `TealiumAutotrackingViewControllersEnabled` in the `info.plist` of the application with the value of `false`:

```xml
&lt;key&gt;TealiumAutotrackingViewControllersEnabled&lt;/key&gt;
&lt;false/&gt;
```

To automatically track a specific view controller, create a subclass of `TealiumViewController`:

```swift
class MyAutomaticallyTrackedViewController: TealiumViewController { 
    // ...
}
```

Alternatively, you can conform to `TealiumViewControllerTrackable` and call `trackViewControllerAppearence` on the `viewDidAppear` method of your view controller.

```swift
class MyViewController: UITableViewController, TealiumViewControllerTrackable {
     @objc
     open override func viewDidAppear(_ animated: Bool) {
         super.viewDidAppear(animated)
         trackViewControllerAppearence()
     }
 }
```

### SwiftUI

To automatically track specific views in SwiftUI, implement one or both of the following approaches: 

* Add a custom modifier to each view you want to track.
* Embed each view you want to track in the Tealium automatic tracking container.

Use one of following view modifiers:

#### `autoTracking(viewSelf:) -&gt; some View`

Use this modifier to automatically track a view using the class name.

Apply this modifier in the body of the view you want to track and pass `self` as parameter:

```swift
struct SomeView: View {
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracking(viewSelf: self) 
    }
}
```

#### `autoTracking(viewClass:) -&gt; some View`

Use this modifier to automatically track a view using the class name of the view class.

Apply this modifier in the body of the view you want to track and pass the name of the class you want to track (if you don&#39;t have access to the object instance):

```swift
struct SomeContainerView: View {
    var body: some View {
        SomeOtherView {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracking(viewClass: SomeOtherView.self) 
    }
}
```

#### `autoTracked(constantName:) -&gt; some View`

Use this modifier to automatically track a view with a custom constant name.

Changing the variable from which the constant is taken won’t change the tracked name.

Do not pass a state variable here as it may conflict with `onDisappear` calls. 

If you want to pass a state variable, pass the binding value instead, using the overloaded method.

```swift
struct SomeView: View {
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracked(constantName: &#34;Some Constant Name&#34;) 
    }
}
```

#### `autoTracked(name: Binding&lt;String&gt;) -&gt; some View`
  
Use this modifier to automatically track a view with a custom state variable name.

Changing the variable in this case results in a different event name for subsequent automatic tracking calls.

This method solves the issue of `onAppear` being called after `onDisappear` for state changes and allows for the variable name to change for subsequent automatically tracked names.

```swift
struct SomeView: View {
    @State var name = &#34;Some Variable Name&#34;
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracked(name: $name) 
    }
}
```

#### Embed Automatic Tracking Container

As an alternative to view modifiers, embed the automatic tracking container `TealiumViewTrackable` in each view you want to track.

There are three options to this approach:

* **Init with content view**  
Pass the content view in the initializer to track the content class name automatically.  
    ```swift
    TealiumViewTrackable {
      SomeView()
    }
    ```
* **Init with constant name and content view**  
Specify a constant name by passing a state variable to be tracked instead of the content class name.  
    ```swift
    TealiumViewTrackable(constantName: &#34;Some Constant Name&#34;) {
      SomeView()
    }
    ```
* **Init with state variable binding name and content view**  
Pass a binding from a state variable of your view. This uses the current value of the state variable when `onAppear` is triggered.  
    ```swift
    @State var name: String = &#34;Some Variable Name&#34;
    var body: some View {
      TealiumViewTrackable(viewName: $name) {
        SomeView()
      }
    }
    ```

## Data Layer

The following variables are included with each tracking call that is triggered by this module:

| Variable      | Description                                            | Example |
|:--------------|:-------------------------------------------------------|:--------|
| `autotracked` | Set for all events tracked by the Autotracking module. | `true`  |

## API Reference

* [`TealiumConfig`](/platforms/ios-swift/api/tealium-config/)

