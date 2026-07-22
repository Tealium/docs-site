---
title: CrashReporter Module
description: Automatically tracks crashes in your app. After the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.
url: https://docs.tealium.com/platforms/ios-swift/module-list/crash-reporter/
---
##  Usage

The CrashReporter module automatically tracks crashes in your app. After the module is enabled and the accompanying frameworks are installed, crash data is added to track events following a crash occurred in your app.

Optionally, you can configure the SDK to send an additional `crash` event by setting the `sendCrashDataOnCrashDetected` configuration flag to `true`. If you do so the crash data will only be added to this specific event.

Usage of this framework is recommended to get vital information regarding your app's crashes.

The following platforms are supported:

* iOS
* tvOS
* macOS

## Install

Install the Crash module with Swift Package Manager or CocoaPods.

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift-crash-reporter`
1. Configure the version rules. Typically, `"Up to next major"` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `TealiumCrashModule and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.
1. Follow [these instructions](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager) to add other modules from the `tealium-swift` library.

### CocoaPods

To install the CrashReporter module with CocoaPods:

1. Add the following pod to your Podfile:  
      ```perl
      pod 'TealiumCrashModule'
      ```
      Your Podfile already contains the following line:

      ```perl
      pod 'tealium-swift'
      ```

2. Run the following command:
      ```perl
      pod install
      ```

### Carthage

To install the CrashReporter module with Carthage:

1. Add the following to your Cartfile:

      ```bash
      github "tealium/tealium-swift-crash-reporter"
      ```

2. Go to the app target's General configuration page in Xcode.

3. Add the following frameworks to the **Embedded Binaries** section: 
      ```perl
      TealiumCrashModule.framework
      CrashReporter.framework
      ```

[Learn more](https://docs.tealium.com/platforms/ios-swift/install/#carthage) about Carthage installation for iOS.

## Configure

To instantiate the CrashReporter module, you must specify it in your `TealiumConfig` object when initializing the SDK:

```swift
import TealiumCore
import TealiumCrashModule

let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")

// add the Collectors you want
config.collectors = [Collectors.AppData, Collectors.Crash] // Instantiates the CrashReporter module
config.sendCrashDataOnCrashDetected = true // optional, If true it sends an extra crash event when a crash is detected and only attaches crash data to that event
tealium = Tealium(config: config) { _ in }                               
```


<blockquote>
Review the [Collectors](https://docs.tealium.com/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.
</blockquote>


## Data Layer

The following variables are transmitted with each tracking call while the module is enabled:

| Variable  | Description | Example |
| :-- | :-- | :-- |
| `crash_uuid` | Unique identifier for this specific crash | `"CC2DA0E9-E544-429A-AC5E-A268FC62F02A"` |
| `device_memory_usage*`     | Current memory used by the app on the device at the time of the crash| `"143.57MB" ` |
| `app_memory_usage`          | Current memory used by the app on the device at the time of the crash| `"143.57MB"`  |
| `device_memory_available*` | Free memory on device at the time of the crash                         | `"1068.88MB"` |
| `memory_free`               | Free memory on device at the time of the crash                       | `"1068.88MB"` |
| `device_os_build`           | Current OS build number                                              | `"15E217"`    |
| `crash_process_id`          | PID of the app at time of crash                                      | `"84351"`     |
| `crash_process_path`        | Path the app was running under                                       | `"/DemoApp.app/DemoApp"` |
| `crash_parent_process`      | Parent process that launched the app                                 | `"launchd_sim"` |
| `crash_parent_process_id`   | Parent process PID                                                   | `"83183"`      |
| `crash_name`                | Friendly name of the crash, if available                             | `"Crash Name"` |
| `crash_cause`               | Cause of the crash                                                   | `"Crash Reason"` |
| `crash_signal_code`         | Signal code causing the crash                                        | `"#0"` |
| `crash_signal_name`         | Signal name causing the crash                                        | `"SIGABRT"`    |
| `crash_signal_address`      | Signal address of the crash                                          | `"4572945982"` |
| `crash_libraries`           | List of loaded libraries at the time of the crash                    | ```[{"baseAddress": "0xa3e0000", "codeType": { "arch": 64, "typeEncoding": "Mach"}, "imageName": "/Applications/Xcode9.3.app/Contents/ Developer/Platforms/iPhoneOS.platform/ Developer/Library/CoreSimulator/Profiles /Runtimes/iOS.simruntime/Contents/ Resources/RuntimeRoot/usr/lib/dyld_sim", "imageSize": 212992, "imageUuid": "4015e9b70bde"}]``` |
| `crash_threads`              | Returns all active threads at the time of the crash                  |```{"crashed": 1,"registers": {"cs": "0x07"},"stack": {"instructionPointer": 4572945982,"symbolInfo": {"symbolName": "","symbolStartAddr": 0},"threadId": ""}}``` |

* These variables are duplicated for backward-compatibility with previous releases

## Invoke a Crash

After `TealiumCrashReporteriOS.framework` is added to your project, no additional initialization steps are needed. As long as the crash module is enabled and the Tealium SDK is initialized, when a crash is exhibited in your app, crash data automatically becomes part of the tracking call.

### Testing

For a local test to report a crash, uncheck **Debug executable** in the app's run scheme before intentionally crashing the app so there is no debugger attached to the app. If a debugger is attached to the app's running process, the crash reporter won't catch any crashes.

## API Reference

### `invokeCrash()`

Invokes a crash for the CrashReporter module.

```swift
TealiumCrashReporter.invokeCrash(name: name, reason: reason)
```

| Parameters | Type | Description | Example |
| --- | --- | --- |  --- |
| `name` | `String` | Name of the crash  | `"TEST_CRASH_NAME"` |
| `reason` | `String` | Reason for crash | `"TEST_CRASH_REASON"` |
