---
title: CrashReporter Module
description: Automatically tracks crashes in your app. After the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.
url: https://docs.tealium.com/platforms/ios-swift/module-list/crash-reporter/
---
##  Usage

The CrashReporter module automatically tracks crashes in your app. After the module is enabled and the accompanying frameworks are installed, crash data is added to track events following a crash occurred in your app.

Optionally, you can configure the SDK to send an additional `crash` event by setting the `sendCrashDataOnCrashDetected` configuration flag to `true`. If you do so the crash data will only be added to this specific event.

Usage of this framework is recommended to get vital information regarding your app&#39;s crashes.

The following platforms are supported:

* iOS
* tvOS
* macOS

## Install

Install the Crash module with Swift Package Manager or CocoaPods.

### Swift Package Manager (Recommended)

Supported in version 1.9.0&#43;, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift-crash-reporter`
1. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `TealiumCrashModule and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.
1. Follow [these instructions](/platforms/ios-swift/install/#swift-package-manager) to add other modules from the `tealium-swift` library.

### CocoaPods

To install the CrashReporter module with CocoaPods:

1. Add the following pod to your Podfile:  
      ```perl
      pod &#39;TealiumCrashModule&#39;
      ```
      Your Podfile already contains the following line:

      ```perl
      pod &#39;tealium-swift&#39;
      ```

2. Run the following command:
      ```perl
      pod install
      ```

### Carthage

To install the CrashReporter module with Carthage:

1. Add the following to your Cartfile:

      ```bash
      github &#34;tealium/tealium-swift-crash-reporter&#34;
      ```

2. Go to the app target&#39;s General configuration page in Xcode.

3. Add the following frameworks to the **Embedded Binaries** section: 
      ```perl
      TealiumCrashModule.framework
      CrashReporter.framework
      ```

[Learn more](/platforms/ios-swift/install/#carthage) about Carthage installation for iOS.

## Configure

To instantiate the CrashReporter module, you must specify it in your `TealiumConfig` object when initializing the SDK:

```swift
import TealiumCore
import TealiumCrashModule

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// add the Collectors you want
config.collectors = [Collectors.AppData, Collectors.Crash] // Instantiates the CrashReporter module
config.sendCrashDataOnCrashDetected = true // optional, If true it sends an extra crash event when a crash is detected and only attaches crash data to that event
tealium = Tealium(config: config) { _ in }                               
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Data Layer

The following variables are transmitted with each tracking call while the module is enabled:

| Variable  | Description | Example |
| :-- | :-- | :-- |
| `crash_uuid` | Unique identifier for this specific crash | `&#34;CC2DA0E9-E544-429A-AC5E-A268FC62F02A&#34;` |
| `device_memory_usage*`     | Current memory used by the app on the device at the time of the crash| `&#34;143.57MB&#34; ` |
| `app_memory_usage`          | Current memory used by the app on the device at the time of the crash| `&#34;143.57MB&#34;`  |
| `device_memory_available*` | Free memory on device at the time of the crash                         | `&#34;1068.88MB&#34;` |
| `memory_free`               | Free memory on device at the time of the crash                       | `&#34;1068.88MB&#34;` |
| `device_os_build`           | Current OS build number                                              | `&#34;15E217&#34;`    |
| `crash_process_id`          | PID of the app at time of crash                                      | `&#34;84351&#34;`     |
| `crash_process_path`        | Path the app was running under                                       | `&#34;/DemoApp.app/DemoApp&#34;` |
| `crash_parent_process`      | Parent process that launched the app                                 | `&#34;launchd_sim&#34;` |
| `crash_parent_process_id`   | Parent process PID                                                   | `&#34;83183&#34;`      |
| `crash_name`                | Friendly name of the crash, if available                             | `&#34;Crash Name&#34;` |
| `crash_cause`               | Cause of the crash                                                   | `&#34;Crash Reason&#34;` |
| `crash_signal_code`         | Signal code causing the crash                                        | `&#34;#0&#34;` |
| `crash_signal_name`         | Signal name causing the crash                                        | `&#34;SIGABRT&#34;`    |
| `crash_signal_address`      | Signal address of the crash                                          | `&#34;4572945982&#34;` |
| `crash_libraries`           | List of loaded libraries at the time of the crash                    | ```[{&#34;baseAddress&#34;: &#34;0xa3e0000&#34;, &#34;codeType&#34;: { &#34;arch&#34;: 64, &#34;typeEncoding&#34;: &#34;Mach&#34;}, &#34;imageName&#34;: &#34;/Applications/Xcode9.3.app/Contents/ Developer/Platforms/iPhoneOS.platform/ Developer/Library/CoreSimulator/Profiles /Runtimes/iOS.simruntime/Contents/ Resources/RuntimeRoot/usr/lib/dyld_sim&#34;, &#34;imageSize&#34;: 212992, &#34;imageUuid&#34;: &#34;4015e9b70bde&#34;}]``` |
| `crash_threads`              | Returns all active threads at the time of the crash                  |```{&#34;crashed&#34;: 1,&#34;registers&#34;: {&#34;cs&#34;: &#34;0x07&#34;},&#34;stack&#34;: {&#34;instructionPointer&#34;: 4572945982,&#34;symbolInfo&#34;: {&#34;symbolName&#34;: &#34;&#34;,&#34;symbolStartAddr&#34;: 0},&#34;threadId&#34;: &#34;&#34;}}``` |

* These variables are duplicated for backward-compatibility with previous releases

## Invoke a Crash

After `TealiumCrashReporteriOS.framework` is added to your project, no additional initialization steps are needed. As long as the crash module is enabled and the Tealium SDK is initialized, when a crash is exhibited in your app, crash data automatically becomes part of the tracking call.

### Testing

For a local test to report a crash, uncheck **Debug executable** in the app&#39;s run scheme before intentionally crashing the app so there is no debugger attached to the app. If a debugger is attached to the app&#39;s running process, the crash reporter won&#39;t catch any crashes.

## API Reference

### `invokeCrash()`

Invokes a crash for the CrashReporter module.

```swift
TealiumCrashReporter.invokeCrash(name: name, reason: reason)
```

| Parameters | Type | Description | Example |
| --- | --- | --- |  --- |
| `name` | `String` | Name of the crash  | `&#34;TEST_CRASH_NAME&#34;` |
| `reason` | `String` | Reason for crash | `&#34;TEST_CRASH_REASON&#34;` |
