---
title: Data Management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/ios-objective-c/data-management/
---
## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

Persistent and volatile data values are stored on the device as an [NSDictionary](https://developer.apple.com/documentation/foundation/nsdictionary) objects.

[Learn more](/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.


## Persistent Data

The persistent object is merged into each event and preserved between launches of the app.

The [`addPersistentDataSources()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/addPersistentDataSources:) method adds key-value data into the library instance&#39;s persistent data store, as shown in the following example:

```obj-c
[self.tealium addPersistentDataSources:@{@&#34;KEY&#34;: @&#34;VALUE&#34;}];
NSDictionary *persistentDataSources = [self.tealium persistentDataSourcesCopy];
```


## Volatile Data

A volatile object is discarded upon closing the app and restarting.

The [`addVolatileDataSources()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/addVolatileDataSources:) method adds key-value data into the temporary data sources dictionary, as shown in the following example:

```obj-c
[self.tealium addVolatileDataSources:@{@&#34;KEY&#34;: @&#34;VALUE&#34;}];
NSDictionary *volatileDataSources = [self.tealium volatileDataSourcesCopy];
```
