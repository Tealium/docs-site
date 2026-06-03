---
title: DispatchQueue Module
description: This module works in conjunction with the Connectivity module to store pending dispatches to disk while the device is offline. When connectivity is restored the queue of events is sent.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/dispatch-queue/
---

## Usage

The DispatchQueue module works in conjunction with the Connectivity module and the consent manager module to store any pending dispatches to disk while the device is offline, or the user has not yet consented to tracking. When connectivity is restored, or if the user consents to tracking, the queue of dispatches are sent. There is a default limit of 20 dispatches in the queue, and when this is exceeded, the oldest dispatch are cleared to make way for the most recent. Data is stored in UserDefaults.

Usage of this module is required if using consent manager or Connectivity modules. Otherwise, it is still strongly recommended to aid with pre-init queueing of events by the TealiumCore module.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the DispatchQueue module with CocoaPods or Carthage.

### CocoaPods

To install the DispatchQueue module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod &#39;tealium-swift/TealiumDispatchQueue&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the DispatchQueue module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumDispatchQueue.framework
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable| Description| Example Value|
|-----------------------------------|--------------------------------|--------------------------------------|
|`was_queued`|Indicates that the dispatch was queued|[`&#34;true&#34;`, `&#34;false&#34;`]|

## API Reference

There are no public API methods for this module. Successes and failures may be monitored through the Delegate module.

The following additional methods are provided by the [`TealiumConfig`](/platforms/ios-swift-v1/api/tealium-config/) class:

### `setMaxQueueSize()`

Sets the maximum persistent queue size for dispatch storage. Default is 20 events.

```swift
tealConfig.setMaxQueueSize(size)
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `size` | `Int` | Maximum persistent queue size for dispatch storage (default: `20`)| `50` |

### `getMaxQueueSize()`

Gets the maximum queue size.

```swift
tealConfig.getMaxQueueSize();
```

| Returns | Return Type |
| --- | --- |
| Maximum persistent queue size for dispatch storage | `Int` |
