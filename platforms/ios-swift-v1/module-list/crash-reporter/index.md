---
title: CrashReporter Module
description: Automatically tracks crashes in your app. Once the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/crash-reporter/
---
##  Usage
The CrashReporter module automatically tracks crashes in your app. Once the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.

Usage of this framework is recommended to get vital information regarding your app's crashes.

The following platforms are supported:

* iOS

## Requirements

* `TealiumCrashReporteriOS`


## Install

Install the CrashReporter module with CocoaPods, Carthage, or manually.

### CocoaPods

To install the CrashReporter module with CocoaPods:

1. Add the following pod to your Podfile:  
    ```ruby
    pod 'tealium-swift/Crash'
    ```

2. To automatically install the external `TealiumCrashReporteriOS` dependency, along with `TealiumAppData`, `TealiumDeviceData`, and `Core` modules, run the following command:
    ```ruby
    pod install
    ```

The framework is auto-instantiated. It has a dependency on the pods `TealiumCore` and `TealiumCrashReporteriOS`. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

The following video demonstrates how to setup the CrashReporter module with Carthage:



Framework is auto-instantiated, so long as it is compiled into your app (included in "Embedded Binaries"). Depends on `TealiumCore` and `TealiumCrashReporteriOS` (external dependency).

1. Follow the steps outlined in the [Swift Carthage Installation](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage).

2. Run the command `carthage update --platform iOS` and include the resulting frameworks in your app:  
      - `TealiumCore.framework` + all standard Tealium frameworks
      - `TealiumCrash.framework`
      - `TealiumCrashReporteriOS.framework`

3. Follow the instructions in the [Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) guide to add the relevant Build Phases scripts for submitting your app to the App Store.

### Manual

1. Follow the Swift [manual installation](https://docs.tealium.com/platforms/ios-swift-v1/install/#manual) steps.
2. Download the [`TealiumCrashReporteriOS.framework`](https://github.com/Tealium/plcrashreporter).
3. Build the `Tealium` and `TealiumCrash` scheme.
4. Drag and drop the following to the Embedded Binaries section within Xcode:
      - `TealiumCore.framework`
      - `TealiumCrash.framework`
      - `TealiumAppData.framework`
      - `TealiumDeviceData.framework`
      - `TealiumCrashReporteriOS.framework`



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
Once `TealiumCrashReporteriOS.framework` is added to your project, no additional initialization steps are needed. As long as the crash module is enabled and the Tealium SDK is initialized, when a crash is exhibited in your app, crash data automatically becomes part of the tracking call.


## API Reference

### `invokeCrash()`

Invokes a crash for the CrashReporter module.

```swift
TealiumCrashReporter.invokeCrash(name, reason)
```

| Parameters | Type | Description | Example |
| --- | --- | --- |  --- |
| `name` | `String` | Name of the crash  | `"TEST_CRASH_NAME"` |
| `reason` | `String` | Reason for crash | `"TEST_CRASH_REASON"` |
