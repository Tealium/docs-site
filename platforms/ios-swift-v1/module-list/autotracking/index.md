---
title: AutoTracking Module
description: Automatically triggers tracking calls when certain user interface interactions take place. For example, taps, swipes, screen views.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/autotracking/
---
## Usage
The AutoTracking module automatically triggers tracking calls when certain user interface interactions take place. For example, taps, swipes, screen views. In general, usage of this module is discouraged and **not recommended** for the following reasons:

* Increased memory usage.
* Increased possibility for crashes to occur due to UI changes outside of Tealium's control. For example, UI component being deallocated before the track call has completed.
* Increased battery consumption.
* Unwanted additional tracking calls.
* Does not fully remove the need to add additional tracking data/events, so additional coding is still required.

As an alternative to Autotracking, we strongly recommend you spend time carefully planning the tracking and data you need to capture, and have your developers pass this data to Tealium at the appropriate time. Autotracking may be useful if you are evaluating Tealium and need a quick implementation, but it is unlikely to fulfill all your tracking requirements on its own.

The following platforms are supported:

* iOS
* tvOS

## Features

The AutoTracking module provides the following features:

* Automatically trigger track calls from `UIViewController` view appearances.
* Automatically trigger track calls for UI Events, such as button taps.
* Includes delegate methods for reporting or suppressing auto-tracked data.
* Uses method swizzling on `UIApplication` and `UIViewController` classes. Disable/exclude if you prefer to avoid swizzling in your app.

## Requirements

* UIKit
* UIApplication

## Install

Install the AutoTracking module with CocoaPods or Carthage.

### CocoaPods

To install the AutoTracking module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumAutotracking'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the AutoTracking module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumAutotracking.framework
    ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

### Bridging Header
This module has been ported from Objective-C code, and as such, requires a Bridging Header.

To create a bridging header:

1. In your Swift project, create a new file. When prompted to select a file type, select "Objective-C File."

2. Give this file a temporary name, such as `placeholder.m`, as you are going to remove it later.

3. Click **Finish**. Xcode prompts you to create a Bridging Header (if it doesn't, you probably already have a Bridging Header in your project). Click **Create Bridging Header** to continue and have Xcode create the new header file for you.

4. Delete `placeholder.m` from your project. Notice a new file called `ProjectName-Bridging-Header.h`.

5. Add the following import statements to the new Bridging Header:  
    ```swift
    #import "uiapplication+tealiumtracker.h"
    #import "uiviewcontroller+tealiumtracker.h"
    ```

## Data Layer

The following variables are transmitted with each tracking call while the module is enabled:

| Variable  | Description                                             | Example  |
|---------------|---------------------------------------------------------|---------------|
| `autotracked`   | Set to true and added to each auto-tracked tracking call. | [`"true"`, `"false"`]          |

## API Reference

The following methods are available to change the default behavior of the Autotracking module, or to monitor auto-tracked tracking calls:

### `tealiumAutotrackingShouldTrack()`

```swift
tealiumAutotrackingShouldTrack(data: [String:Any]) -> Bool
```

| Parameters | Type | Description                                                      | Example   |
|------------|------|----------------------------------------------------------------- |-----------------|
| `data`     | `String` or `[String]` | Dictionary with String keys and Any value type | `["key":"value"]` |


### `tealiumAutotrackDidComplete()`

```swift
tealiumAutotrackDidComplete(success:Bool, info:[String:Any]?, error:Error?)
```

| Parameters | Type | Description | Example  |
|------------|------|----------| --- |
| `success`  | `Bool` | If the auto-tracked triggered call was successful | [`"true"`, `"false"`]      |
| `info`     | `String` or `[String]`  |(Optional) Holds delivery type info, final call format, and the payload (the data dictionary used to generate the call) |             |
| `error`    | `Error` | Error, if any    |               |
