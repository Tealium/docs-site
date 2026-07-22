---
title: Event Batching
description: This document explains how event batching works in the Tealium Collect mobile module.
url: https://docs.tealium.com/platforms/getting-started-mobile/event-batching/
---
Event batching is a feature of the Tealium Collect module that optimizes the transmission of data between a mobile device and Tealium by sending multiple events in a single HTTP request. Event batching works with a dedicated data collection endpoint that is optimized to eliminate repetitive data layer variables and to accept payloads compressed with gzip.

## Batch vs. Queue

Event batching refers to how a device transmits data across the network. The event queue refers to how the device stores data temporarily before dispatching it. Event batching combines multiple events into a single network request, as opposed to each tracked event in its own request.

The device uses batching under the following conditions:

* Batching is enabled in **Publish Configuration > Mobile Library Publishing > Batching**. For more information, see [Create a mobile profile](https://docs.tealium.com/creating-a-mobile-profile/#batching).
* The device has no stable internet connection. The device stores events until a connection is available.
* The user has not selected any preferences in the **Consent Manager**. The device stores events until the user selects a **Consent Manager** preference. For more information, see [About consent management](https://docs.tealium.com/about-consent-management/).

The device's batch sending behavior depends on the app's status on the device:

* If the user sends the app to the background:
  * The device sends the lifecycle "sleep" event.
  * If an interet connection is available, the device immediately sends any events generated prior to the app going to the background.
* If the user sends the app ito the foreground:
  * The device sends any events in the queue, in addition to the lifecycle "wake" event.

Event batching works with the event queue by processing multiple events at once until the queue is empty.

For example, a device is offline and the event queue grows to contain 25 events. After the device comes online, the device processes the queue in batches of 10 events until the queue is empty. In this case, two batched requests with 10 events each and one batch for the remaining five events are sent, for a total of 25 tracked events using only three network requests.


<blockquote>
The batch size maximum is 10 events.
</blockquote>


## Benefits

The benefits of event batching include:

* Reduced size of total transmitted data.
* Fewer network requests for the same number of events.
* Improved battery performance on the device.

### Data Layer Optimization

The Tealium mobile libraries send a lot of [device information to the data layer](https://docs.tealium.com/platforms/getting-started-mobile/data-layer/), such as app name, screen resolution, and OS version. The device includes these variables in every network request, even though their values do not change between events. Event batching optimizes the data layer so that the device sends these common variables only once per batch.

### Payload Compression

The device compresses the event batch payload with gzip to minimize the size of the HTTP request. This compression reduces the size of each network request by up to 90%.

### Event batching for Tealium iQ Tag Management

If the **Tag Management** module is in use and event batching is enabled, the device queues these events as normal, and then dispatches them as individual JavaScript calls to the WKWebView instance. The device triggers any configured tags individually, which results in multiple requests leaving the device (one per event in the batch). This reduces the device's battery consumption because the device's radio does not need to wake up as frequently as sending events in real-time.

## Supported Platforms

The following platforms support event batching:

* [Android](https://docs.tealium.com/platforms/android-java/install/#event-batching)
* [iOS](https://docs.tealium.com/platforms/ios-swift/install/#event-batching)
