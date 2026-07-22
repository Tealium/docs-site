---
title: Delegate Module
description: A multicast delegate handler to allow delegates to monitor or suppress dispatch events.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/delegate/
---## Usage

The Delegate module provides a multicast delegate handler to allow delegates to monitor or suppress dispatch events. Usage of this module is optional. You only need to use it if you need fine control over individual dispatches/events. For example, to block an event from being sent, or to monitor tracking calls for success/failure.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the Delegate module with CocoaPods or Carthage.

### CocoaPods

To install the Delegate module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumDelegate'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the Delegate module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumDelegate.framework
    ```
3. To setup a tracking delegate, add the following required import statement to your project:  
    ```swift
    import TealiumDelegate
    ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.


## Data Layer

No additional variables are introduced by this module.

## API Reference

### `add()`
Adds a weak pointer to a class instance conforming to the `TealiumDelegate` protocol.

```swift
add(delegate)
```

| Parameters  | Type    | Description                                       | Example |
|-------------|---------|---------------------------------------------------| ---|
| `delegate`  | `TealiumDelegate`  | Any class conforming to the TealiumDelegate protocol | `delegate:self` |


### `remove()`
Removes the weak pointer reference to the given class conforming to the `TealiumDelegate` protocol.

```swift
remove(delegate)
```

| Parameters  | Type    | Description                                       | Example |
|-------------|---------|---------------------------------------------------| --- |
| `delegate`  | `TealiumDelegate`  | Any class conforming to the TealiumDelegate protocol	  | `delegate:self` |


### `removeAll()`

Removes all weak pointers from tracking.

```swift
removeAll()
```

### `tealiumShouldTrack()`

If method returns `true`, the tracking call is allowed to complete. If method returns false, tracking call is canceled.

```swift
tealiumShouldTrack(data: [String:Any]) -> Bool
```

| Parameters | Description   | Example             |
|------------|---------------|---------------------------|
| `data`     | `[String:Any]`| `["somekey" : "somevalue"]` |


### `tealiumTrackCompleted()`
Allows monitoring of completed track calls and handling of any errors.

```swift
tealiumTrackCompleted(success: Bool, info: [String:Any]?, error: Error?)
```

| Parameters | Type             | Description                                                  | Example |
|------------|------------------|--------------------------------------------------------------| ------- |
| `success`    | `Bool`         | If dispatch completed acceptably                                                       |[`"true"`, `"false"`] |
| `info`       | `[String:Any]` | Dictionary of the original payload and any other returned data regarding dispatch     |`["somekey" : "somevalue"]`  |
| `error`      | `Error`        | Error, if any, encountered during dispatch processing|  `TealiumCollectError.xErrorDetected` |
