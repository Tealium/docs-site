---
title: Data Management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/xamarin-v1/data-management/
---
<blockquote>
For the current version, see [Tealium for Xamarin 2.x](https://docs.tealium.com/platforms/xamarin/).
</blockquote>


## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent Data

Persistent data is merged into your data dictionary on every tracking call, as well as persist between launches.

The `AddPersistentDataSources()` method adds persistent data, as shown in the following example:

```csharp
tealium.AddPersistentDataSources(new Dictionary<string, object>(1) {
  {"KEY", "VALUE"}});
```

## Volatile Data

Volatile data is merged into your data dictionary on every tracking call, but once the application is closed, volatile data is lost is not present on the next launch.  

The `AddVolatileDataSources()` method adds volatile data, as shown in the following example:

```csharp
tealium.AddVolatileDataSources(new Dictionary<string, object>(1) {
   {"KEY", "VALUE"}});
```
