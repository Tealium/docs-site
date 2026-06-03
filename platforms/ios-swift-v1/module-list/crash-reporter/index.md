---
title: CrashReporter Module
description: Automatically tracks crashes in your app. Once the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/crash-reporter/
---
##  Usage
The CrashReporter module automatically tracks crashes in your app. Once the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app.

Usage of this framework is recommended to get vital information regarding your app&#39;s crashes.

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
    pod &#39;tealium-swift/Crash&#39;
    ```

2. To automatically install the external `TealiumCrashReporteriOS` dependency, along with `TealiumAppData`, `TealiumDeviceData`, and `Core` modules, run the following command:
    ```ruby
    pod install
    ```

The framework is auto-instantiated. It has a dependency on the pods `TealiumCore` and `TealiumCrashReporteriOS`. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

The following video demonstrates how to setup the CrashReporter module with Carthage:



Framework is auto-instantiated, so long as it is compiled into your app (included in &#34;Embedded Binaries&#34;). Depends on `TealiumCore` and `TealiumCrashReporteriOS` (external dependency).

1. Follow the steps outlined in the [Swift Carthage Installation](/platforms/ios-swift-v1/install/#carthage).

2. Run the command `carthage update --platform iOS` and include the resulting frameworks in your app:  
      - `TealiumCore.framework` &#43; all standard Tealium frameworks
      - `TealiumCrash.framework`
      - `TealiumCrashReporteriOS.framework`

3. Follow the instructions in the [Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) guide to add the relevant Build Phases scripts for submitting your app to the App Store.

### Manual

1. Follow the Swift [manual installation](/platforms/ios-swift-v1/install/#manual) steps.
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
Once `TealiumCrashReporteriOS.framework` is added to your project, no additional initialization steps are needed. As long as the crash module is enabled and the Tealium SDK is initialized, when a crash is exhibited in your app, crash data automatically becomes part of the tracking call.


## API Reference

### `invokeCrash()`

Invokes a crash for the CrashReporter module.

```swift
TealiumCrashReporter.invokeCrash(name, reason)
```

| Parameters | Type | Description | Example |
| --- | --- | --- |  --- |
| `name` | `String` | Name of the crash  | `&#34;TEST_CRASH_NAME&#34;` |
| `reason` | `String` | Reason for crash | `&#34;TEST_CRASH_REASON&#34;` |
