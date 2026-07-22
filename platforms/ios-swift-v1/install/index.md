---
title: Install
description: How to install the Tealium SDK for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift-v1/install/
---

<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


## Requirements

* Xcode 7.0+
* iOS 9.0+, macOS 10.11+, watchOS 3.0+, or tvOS 9.2+
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Sample Apps

Explore the Swift [sample apps](https://github.com/Tealium/tealium-swift/tree/master/samples) to help familiarize yourself with the Tealium library, tracking methods, and best practice implementation

To abstract the Tealium implementation from the rest of your app, we recommend using a helper class. This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single `ViewController` or Swift file.

Explore our [sample helper class](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample).

## Install

The Tealium iOS library is divided into modules. It is recommended to install only the modules that you need to maintain a smaller resource footprint. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/modules/) about the modules available for iOS.

Install the Tealium for iOS library with Swift Package Manager, CocoaPods, or Carthage.



<blockquote>
If you do not require consent management, exclude or disable the consent manager module. The [consent manager](https://docs.tealium.com/platforms/ios-swift-v1/consent-management/) module is enabled by default, which initially prevents tracking calls from being sent. To allow tracking calls, set the consent status to `.consented`.
</blockquote>
  

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**
2. Enter the repository URL: `https://github.com/tealium/tealium-swift`
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current Tealium Swift library version does not appear in the list, then reset your Swift package cache.
4. Select the modules to install, and select the app target you want the modules to be installed in.

If your project has more than one app target and needs Tealium Swift libraries in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install Tealium Swift libraries in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select a Tealium Swift library to add it to your app target.

The Swift Package Manager has the following limitations:

- Due to lack of mixed-language source in a single target, the [`CrashReporter`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/crash-reporter/) and [`AutoTracking`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/autotracking/) modules are not supported through the Swift Package Manager. Verify that you do not need these modules before using Swift Package Manager.
- Restricting a target within a package to a specific platform is not possible. Modules such as [`TagManagement`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/tag-management/), which are only supported for iOS, also become available to non-iOS targets. Adding one of these modules to an non-iOS target causes the compiler throws errors due to unavailable system libraries.

### CocoaPods

To install the Tealium for iOS library with CocoaPods (Recommended):

1. Add the Tealium Swift pod `"tealium-swift"` to your Podfile. It has a subspec for each module, each of which depends on the "Core" module. If you do not specify any subspecs, all modules are installed by default.  
      ```ruby
      # Uncomment the next line to define a global platform for your project
      platform :ios, '9.0'

      target 'CPodTest' do
            # Comment the next line if you don't want to use dynamic frameworks
            use_frameworks!

            # Pods for CPodTest

            # new entry for Tealium pod
            pod 'tealium-swift' # all modules
            # pod 'tealium-swift/TealiumTagManagement' # to install individual modules only, use subspecs
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

The following is the recommended Podfile:


<blockquote>
To disable specific modules from the Podfile, comment them out in the Podfile with `#`.
</blockquote>


```ruby
# Podfile
# replace CPodTest with your target
target 'CPodTest' do
    # Comment the next line if you're not using Swift and don't
    # want to use dynamic frameworks
    use_frameworks!

    # Pods for CPodTest
    # *** Recommended minimum:
    # Only disable if you're sure you don't need them.  ***

    # All pods depend on Core. Supports all platforms.
    pod "tealium-swift/Core"
    # All platforms. Provides important info about
    # the app bundle.
    pod "tealium-swift/TealiumAppData"
    # All platforms. Sends data to Tealium Customer Data Hub.
    pod "tealium-swift/TealiumCollect"
    # All platforms. Assists with GDPR/privacy compliance.
    pod "tealium-swift/TealiumConsentManager"
    # iOS, macOS, tvOS only. Detects connectivity state and queues track calls while offline.
    # Should be used in conjunction with TealiumDispatchQueue module.
    pod "tealium-swift/TealiumConnectivity"

    # DataSource is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Adds "tealium_datasource" to each dispatch, and extends TealiumConfig class.
    # pod "tealium-swift/TealiumDataSource"

    # FileStorage is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Stores persistent data to File Storage.
    # Bundles PersistentData module.
    # Should not be used if DefaultsStorage module is in use.
    # Pick the option that best suits you.
    # pod "tealium-swift/TealiumFileStorage"

    # All platforms. Enables the use of delegates
    # and completion handlers on the Tealium class.
    pod "tealium-swift/TealiumDelegate"
    # All platforms. Adds device information to each dispatch.
    pod "tealium-swift/TealiumDeviceData"
    # All platforms. Enables offline storage of queued events.
    # (required for Consent, Connectivity).
    pod "tealium-swift/TealiumDispatchQueue"
    # All platforms. Add app lifecycle information to each dispatch.
    pod "tealium-swift/TealiumLifecycle"
    # All platforms. Enables logging information to the LLDB console.
    pod "tealium-swift/TealiumLogger"
    # iOS only. Used with the TagManagement module to trigger Remote Commands
    pod "tealium-swift/TealiumRemoteCommands"
    # iOS only. Enables Tealium iQ Tag Management.
    pod "tealium-swift/TealiumTagManagement"
    # All platforms. Adds important data to each dispatch, and enables temporary storage of data for the current session.
    pod "tealium-swift/TealiumVolatileData"

    # *** Optional modules: You may not need these modules. Enable as required.   *** #

    # iOS Only. Gathers app attribution data and advertising IDs.
    # pod "tealium-swift/TealiumAttribution"

    # iOS and tvOS only. Generally not recommended. See separate notes in module documentation.
    # pod "tealium-swift/TealiumAutotracking"

    # DefaultStorage is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Stores persistent data to UserDefaults. Bundles PersistentData module. Should not be used if FileStorage module is in use.
    # pod "tealium-swift/TealiumDefaultsStorage"

    # iOS only. Reports detailed crash information. Installs separate TealiumCrashReporter dependency (based on PLCrashReporter).
    # pod "tealium-swift/Crash"
end
```

#### Full Podfile

The full Podfile imports the entire Tealium for iOS (Swift), including all modules specified as optional:

```ruby
# Uncomment the next line to define a global platform for your project
platform :ios, '9.0'

target 'CPodTest' do
    # Comment the next line if you're not using Swift and don't want to use dynamic frameworks
    use_frameworks!

    # Pods for CPodTest

    # new entry for Tealium pod
    pod 'tealium-swift'
end
```
To disable specific modules, see the `TealiumModulesList` struct and relevant methods to blacklist the modules in the [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/) class.

### Carthage

To install Tealium for iOS (Swift) with Carthage:

1. Add the following to your Cartfile:    
      ```ruby
      github "tealium/tealium-swift"
      ```

2. To produce frameworks for iOS, macOS, tvOS and watchOS, run the following command:  
      ```ruby
      carthage update
      ```

3. To build only for a particular platform, such as iOS, and to speed up subsequent builds after the initial build, use Carthage's `--platform` argument:  
      ```ruby
      carthage update --platform ios --cache-builds
      ```

4. Drag the frameworks you require into your Xcode project's **General > Embedded Binaries** section.  
      
<blockquote>
Verify that the Tealium frameworks have been added to the Embedded Binaries section in your project settings, otherwise your app crashes at launch.
</blockquote>
  

5. Follow the instructions listed in the Carthage [Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) documentation to add the relevant build phases scripts, to ensure you don't run into any issues when submitting your app.


#### About Modules (1.6.5+)
As of version 1.6.5, the Tealium Swift SDK has been split up into separate modules/frameworks. This means you need only import the specific frameworks for the modules you need to use, which helps to reduce the binary size and, ultimately, increase your app's performance.

**Module import statements**  
```swift
import TealiumCore              // required for Tealium, TealiumConfig, TealiumInstanceManager
import TealiumVolatileData      // required if you want to store volatile data through the Volatile Data API
//import TealiumFileStorage     // Included in TealiumCore for Swift 1.8.0+. Import for prior versions.
//import TealiumDefaultsStorage // Included in TealiumCore for Swift 1.8.0+. Import for prior versions if you need to store persistent data
import TealiumRemoteCommands    // required if you need to interact with the Remote Commands API
import TealiumDelegate          // required if you need to set up a tracking delegate
//import TealiumDataSource      // Included in TealiumCore for Swift 1.8.0+. Import for prior versions to
                                //     allow datasource param to be set on the TealiumConfig class instance
import TealiumLifecycle         // only required if you need to manually call the Lifecycle API
```

Due to Carthage limitations, we had to choose between the convenience of importing the entire SDK, and the flexibility and performance gains of a fully modular install. The downside to this approach is that it's now necessary to add each module you want to use individually.

- Carthage builds _all_ the modules and output the resulting `.framework` files into your Carthage build directory.
- Delete any modules you don't need, and drag the modules that you do need into Xcode.

See [Modules](https://docs.tealium.com/platforms/ios-swift-v1/modules/) for further details on recommended module lists.


## Initialize

It is recommended to manage the initialization of the [`Tealium`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#class-tealium) class. This provides a single point of entry for the Tealium iOS library, and simplifies future upgrades.

To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/) instance to the [`Tealium()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#tealium) constructor, as shown in the following example:

```swift
class TealiumHelper {

static let shared = TealiumHelper()
var tealium: Tealium?

	private init() {
		initTealium()
	}

	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
   	       		                   profile: "PROFILE",
        	   	                   environment: "ENVIRONMENT",
           		                   datasource: "DATASOURCE")
		// add config options as required
		config.setLogLevel(.verbose)
		// initialize and keep a reference to Tealium
		tealium = Tealium(config: config) { moduleResponses in
		    // Completion block; perform post-init tasks here
		}
	}
}
```



<blockquote>
In version 1.9.0+, Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable it using `config.shouldUseRemotePublishSettings = false`.
</blockquote>


## Log Level

To set a log level, call the [`setLogLevel()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#setloglevel) method on your `TealiumConfig` instance with one of the following values:

* `none`
* `.errors`
* `.warnings`
* `.verbose`

For debugging purposes, `.verbose` is recommended, as shown in the following example:

```swift
config.setLogLevel(.verbose)
```

## Event Batching

Prior to version 1.9.0, the Tealium Swift library did not use [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/). Therefore, event batching must be enabled and configured when the SDK is initialized. Version 1.9.0+ provides Mobile Publish Settings support, allowing event batching to be configured remotely.

This example enables event batching and sets the batch size and queue size.

```swift
import TealiumDispatchQueue // required for event batching options
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                   profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
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

| Property | Description |
| --- | --- |
| [`batchingEnabled`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#batchingenabled) | Enables or disables event batching (default: `false`). |
| [`batchSize`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#batchsize) | Sets the amount of events to combine into a single batch request (max: 10). |
| [`dispatchAfter`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#dispatchafter) | Sets the number of events after which the queue will be flushed. |
| [`dispatchExpiration`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#dispatchexpiration) | Sets the batch expiration in days. If the device is offline for an extended period, events older than this will be deleted. |
| [`dispatchQueueLimit`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#dispatchqueuelimit) | Sets the maximum number of queued events. If this number is reached, and the queue has not been flushed, the oldest events will be deleted. |

### Tag Management

With Tag Management and event batching enabled, tracking calls are dispatched as individual JavaScript calls to the hidden webview.

Configured tags are triggered individually, resulting in multiple requests per event leaving the device. This improves device performance by waking up the device less frequently than sending real-time events.

### Tealium Collect

This endpoint currently only accepts batch data generated by the Tealium SDK, in a proprietary batch format.
