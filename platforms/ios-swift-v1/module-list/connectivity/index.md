---
title: Connectivity Module
description: Automatically queues dispatches if the device reports no network connectivity.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/connectivity/
---
## How It Works

The Connectivity module automatically queues dispatches if the device reports no network connectivity, using Apple's Reachability API to monitor the network connectivity.

Each time a tracking call is sent, the module checks the current connection status, and begins queueing requests if the internet is unreachable. Each time a new tracking call is received, it checks the connection status again, and if the connectivity state has changed to reachable again, previously queued requests are all sent, and the queue is cleared.

Additionally, as of 1.6.5, the connectivity status is automatically checked every 30 seconds by default (overridable by `TealiumConfig`) after the status has been detected as "not reachable." If the status changes from "not reachable" to "reachable," the queue is flushed automatically (meaning all tracking calls in the queue are dispatched).

The automatic connectivity check is canceled once the connectivity status changes to "reachable" and resumes when the status is detected as "not reachable." This conserves resources by only monitoring for connection changes when strictly necessary.

## Usage
Usage of this module is strongly recommended. Without it, dispatches fail and be dropped if the device is offline.

The following platforms are supported:

* iOS
* tvOS
* macOS
* watchOS

## Requirements

* `SystemConfiguration`
* `TealiumDispatchQueue`. Not strictly a compile-time dependency, but dispatches are not successfully stored if this module isn't included.


## Install

Install the Connectivity module with CocoaPods or Carthage.

### CocoaPods

To install the Connectivity module with CocoaPods:

1. Add the following pod to your Podfile:  
    ```ruby
    pod 'tealium-swift/TealiumConnectivity'
    ```

2. Add the following required pod when using Connectivity module to persist dispatches:  
    ```ruby
    pod 'tealium-swift/TealiumDispatchQueue'
    ```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod.  [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the Connectivity module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following frameworks to the **Embedded Binaries** section:  
    ```ruby
    TealiumConnectivity.framework
    TealiumDispatchQueue.framework
    ```

The frameworks are auto-instantiated. They have a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.


## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable   | Description                                                                                                                      | Example  |
|------------|----------------------------------------------------------------------------------------------------------------------------------|---------------|
| `was_queued` | Indicates whether a tracking call was queued due to no connectivity. Only present for queued events; absent for all other events | [`"true"`, `"false"`]   |
| `queue_reason` | Indicates the reason this event was queued (currently `connectivity` or `consent`) | connectivity          |
| `network_connection_type`   | Current connection type                                                               | [`"wifi"`, `"cellular"`]             |
