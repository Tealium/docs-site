---
title: Install
description: Learn to install the Tealium SDK for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift/install/
---

<blockquote>
The current Tealium for Swift SDK version is 2.x. For previous versions, see [Swift 1.x](https://docs.tealium.com/platforms/ios-swift-v1) or [Objective-C](https://docs.tealium.com/platforms/ios-objective-c/). Swift code co-exists along side your existing Objective-C files in the same project, with full access to your Objective-C API, making it easy to adopt.
</blockquote>


## Requirements

* Xcode 7.0+
* iOS 9.0+, macOS 10.11+, watchOS 3.0+, or tvOS 9.2+
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Sample Apps

Explore the iOS (Swift) [sample apps](https://github.com/Tealium/tealium-swift/tree/master/samples) to help familiarize yourself with the Tealium library, tracking methods, and best practice implementation

To abstract the Tealium implementation from the rest of your app, we recommend using a helper class. This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single `View` or Swift file.

Explore our [sample helper class](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample).

## Install

The Tealium iOS library is divided into modules. It is recommended to install only the modules that you need to maintain a smaller resource footprint. [Learn more](https://docs.tealium.com/platforms/ios-swift/modules/) about the modules available for iOS.

Install the Tealium for iOS library with Swift Package Manager, CocoaPods, or Carthage.

### Swift Package Manager (Recommended)

Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `Up to next major` is recommended. If the current Tealium Swift library version does not appear in the list, then reset your Swift package cache.
1. Select the modules to install, and select the app target you want the modules to be installed in.

If your project has more than one app target and needs Tealium Swift libraries in more app targets, you have to manually add them in the **Frameworks and Libraries** section.

To install Tealium Swift libraries in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
1. In your Xcode project, select the app target under the **TARGETS** section.
1. Navigate to **Frameworks and Libraries** and select a Tealium Swift library to add it to your app target.


<blockquote>
Swift Package Manager cannot limit a target in a package to a specific platform. For example, modules such as [`TagManagement`](https://docs.tealium.com/platforms/ios-swift/module-list/tag-management/), supported only by iOS, also become available to non-iOS targets. Although these modules will technically be available through SPM on XCode to non-iOS targets, adding the modules to those targets will cause the compiler to throw errors due to unavailable system libraries. This limitation should not impact users because iOS-exclusive modules should only be added to iOS apps.
</blockquote>


### CocoaPods

To install the Tealium for iOS library with CocoaPods (Recommended):

1. Add the Tealium Swift pod `"tealium-swift"` to your Podfile. It has a subspec for each module, each of which depends on the "Core" module. If you do not specify any subspecs, all modules are installed by default.
      ```ruby
      # Uncomment the next line to define a global platform for your project
      platform :ios, '11.0'

      target 'CPodTest' do
            # Comment the next line if you don't want to use dynamic frameworks
            use_frameworks!

            # Pods for CPodTest

            # new entry for Tealium pod
            pod 'tealium-swift' # all modules
            # pod 'tealium-swift/TagManagement' # to install individual modules only, use subspecs
      end
      ```

2. Once you have added the modules you want, run the following command:
      ```ruby
      pod install
      ```

<blockquote>
If the command doesn't find the correct Pods, try running the command `pod repo update`.
</blockquote>


3. Open your Xcode project using the `.xcworkspace` file (Do not use the `.xcodeproj` file).

4. To import any number of modules, add the following import statement in the file you plan to instantiate Tealium from:
      ```swift
      import TealiumSwift
      ```

#### Recommended Podfile

The following is the list of recommended modules to add to your podfile:


<blockquote>
To disable specific modules from the Podfile, comment them out in the Podfile with `#` or delete the line.
</blockquote>


```ruby
# ...
# *** Recommended minimum:
# All pods depend on Core. Supports all platforms.
pod "tealium-swift/Core"
pod "tealium-swift/Lifecycle"
pod "tealium-swift/Collect" # for Server-side products. For example: EventStream - usually this or TealiumTagManagement, but not often both
# OR
pod "tealium-swift/TagManagement" # for Tealium iQ
pod "tealium-swift/RemoteCommands"

# *** Optional modules: You may not need these modules. Enable as required.   *** #

# Provides Visitor Audience and Attiribute information back to the app
# pod "tealium-swift/VisitorService"

# iOS Only. Gathers app attribution data and advertising IDs.
# pod "tealium-swift/Attribution"

# iOS and tvOS only. Generally not recommended. See separate notes in module documentation.
# pod "tealium-swift/Autotracking"

# See separate notes in module documentation.
# pod "tealium-swift/Location"

# iOS only. Reports detailed crash information.
# Installs separate TealiumCrashReporter dependency (based on PLCrashReporter).
# pod "TealiumCrashModule"
# ...
```

### Carthage

To install Tealium for iOS (Swift) with Carthage:

1. Add the following to your Cartfile:
      ```bash
      github "tealium/tealium-swift"
      ```

2. To produce frameworks for iOS, macOS, tvOS and watchOS, run the following command:
      ```bash
      carthage update
      ```

3. To build only for a particular platform, such as iOS, and to speed up subsequent builds after the initial build, use Carthage's `--platform` argument:
      ```bash
      carthage update --platform ios --cache-builds
      ```

4. Drag the frameworks you require into your Xcode project's **General > Embedded Binaries** section.

<blockquote>
Verify that the Tealium frameworks have been added to the Embedded Binaries section in your project settings, otherwise your app crashes at launch.
</blockquote>


5. Follow the instructions listed in the [Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) documentation to add the relevant build phases scripts, to ensure you don't run into any issues when submitting your app.

#### Importing Modules

The Tealium Swift SDK has been split up into separate modules/frameworks. Import only the specific frameworks for the modules you need to reduce the binary size and increase your app's performance.

**Module import statements**

*  **TealiumCore** - required for Tealium, TealiumConfig, TealiumInstanceManager
*  **TealiumTagManagement** - required to dispatch track calls to Tealium iQ
*  **TealiumCollect**  - required to dispatch track calls to Tealium's Customer Data Hub
*  **TealiumRemoteCommands** - required if you need to interact with the remote commands API
*  **TealiumLifecycle** - required if you need to collect lifecycle events and associated data

```swift
import TealiumCore
import TealiumTagManagement
import TealiumCollect
import TealiumRemoteCommands
import TealiumLifecycle
```

Due to Carthage limitations, we had to choose between the convenience of importing the entire SDK, and the flexibility and performance gains of a fully modular install. The downside to this is that it's necessary to add each module you want to use individually.

- Carthage builds _all_ the modules and output the resulting `.framework` files into your Carthage build directory.
- Delete any modules you don't need, and drag the modules that you do need into Xcode.

See [Modules](https://docs.tealium.com/platforms/ios-swift/modules/) for further details on recommended module lists.

## Initialize

To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/) instance to the [`Tealium()`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#tealium) constructor.


<blockquote>
Manage your [`Tealium`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium iOS library and simplifies future upgrades.
</blockquote>


```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
    var tealium: Tealium?

    private init() {

        // add necessary config options
        config.batchingEnabled = true
        config.logLevel = .debug

        // add the Collectors you want
        config.collectors = [Collectors.Lifecycle,
                             Collectors.Location,
                             Collectors.VisitorService]

        // add the Dispatchers you want
        config.dispatchers = [Dispatchers.TagManagement,
                              Dispatchers.RemoteCommands]

        tealium = Tealium(config: config)

        // optional post init processing
        tealium?.dataLayer.add(key: "mykey", value: "myvalue", expiry: .forever)

    }

    public func start() {
        _ = TealiumHelper.shared
    }

    class func trackView(title: String, data: [String: Any]?) {
      let tealView = TealiumView(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealView)
    }

    class func trackEvent(title: String, data: [String: Any]?) {
      let tealEvent = TealiumEvent(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealEvent)
    }
}
```

Replace the following:
* `ACCOUNT`: your Tealium account name you want to use to initialize the library in lowercase.
* `PROFILE`: your Tealium profile name you want to use to initialize the library in lowercase.
* `ENVIRONMENT`: the environment where you want to initialize Tealium.
* `DATASOURCE`: the Tealium data source you want to use.


<blockquote>
Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable them using `config.shouldUseRemotePublishSettings = false`.
</blockquote>


## Log Level

To set a log level, set the [`logLevel`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#loglevel) property on your `TealiumConfig` instance:
```swift
config.logLevel = .debug // or .info, .error, .fault, .silent
```

For debugging purposes, `.debug` is recommended.

The default log type used is [`OSLog`](https://developer.apple.com/documentation/os/oslog), but this is modifiable to use `.print` by updating the `logType` property on the `TealiumConfig` object:

```swift
config.logType = .print
```

It is also possible to add your own logger instead of using the `TealiumLogger` by conforming your `Logger` class to the `TealiumLoggerProtocol` and setting the instance of that class to the `logger` property on the `TealiumConfig` object. Here is an example:

```swift
class CustomLogger: TealiumLoggerProtocol {
	// ... conforming to the TealiumLoggerProtocol
	// plus your own custom methods
}

class TealiumHelper {
	let customLogger = CustomLogger()
	var tealium: Tealium?
	// ...

	private init() {
		config.logger = customLogger
		// ...
	}
}

```

## AppDelegate Proxy

By default, the Tealium Swift library includes a proxy for your app's AppDelegate which automatically tracks deep links and initiates Tealium trace sessions using the [Mobile Trace Tool](https://docs.tealium.com/platforms/getting-started-mobile/trace/#mobile-trace-tool). If you don't want to use this feature, set the `appDelegateProxyEnabled` property to `false` on your `TealiumConfig` instance.

```swift
config.appDelegateProxyEnabled = false
```

## Event Batching

Event Batching is either be configured locally on the `TealiumConfig` instance, or by using the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/). Local settings override remote settings.

This example enables event batching and sets the batch size and queue size.

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private init() {
		config.batchingEnabled = true            // enable batching
		config.batchSize = 10                    // size of batch
		config.dispatchAfter = 25                // flush after every 25 events
		config.dispatchQueueLimit = 100          // 100 max queued events
		config.dispatchExpiration = 5            // events expire/delete after 5 days
		// ...
	}
}
```

The following options are available to customize event batching.

| Property                                                                            | Description                                                                                                                             |
|:------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------|
| [`batchingEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#batchingenabled)       | Enables or disables event batching (default: `false`).                                                                                  |
| [`batchSize`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#batchsize)                   | Sets the amount of events to combine into a single batch request (max: 10).                                                             |
| [`dispatchAfter`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#dispatchafter)           | Sets the number of events after which the queue is flushed.                                                                             |
| [`dispatchExpiration`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#dispatchexpiration) | Sets the batch expiration in days. If the device is offline for an extended period, events older than this are deleted.                 |
| [`dispatchQueueLimit`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#dispatchqueuelimit) | Sets the maximum number of queued events. If this number is reached, and the queue has not been flushed, the oldest events are deleted. |

#### Tag Management

With Tag Management and event batching enabled, tracking calls are dispatched as individual JavaScript calls to the hidden WebView.

Configured tags are triggered individually, resulting in multiple requests per event leaving the device. This improves device performance by waking up the device less frequently than sending real-time events.

#### Tealium Collect

This endpoint currently only accepts batch data generated by the Tealium SDK, in a proprietary batch format.
