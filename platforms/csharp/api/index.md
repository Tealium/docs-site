---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for C#.
url: https://docs.tealium.com/platforms/csharp/api/
---
## Class: `Config`

The following summarizes the commonly used methods of the C# `Config` class.

| Method | Description |
| ----- | ------ |
| `Config()` | Tealium configuration constructor |

### `Config()`

Constructor to configure the Tealium instance

```csharp
Config tealConfig = new Config(account, profile, environment,
                               visitorID, modules, dataSourceKey,
                               overrideCollectUrl, optionalData, method);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `string` | Tealium Account name  | `&#34;companyXYZ&#34;` |
| `profile` | `string` |Tealium profile  name|  `&#34;main&#34;` |
| `environment` | `string` |(Optional) Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `visitorID` | `string` |32-char alphanumeric string ID, unique to a user, app instance, or device (`null` ok) |  `&#34;t3aL...1uM&#34;` |
| `modules` | `[string]` | (Optional) Modules to be initialized with Collect library |  See [Available Modules](#available-modules) |
| `dataSourceKey` | `string` |(Optional) Data source key |  | `&#34;abc123&#34;` |
| `overrideCollectUrl` | `string` |(Optional) Override Collect URL (custom destination URL for data) |   |
| `optionalData` | `Dictionary&lt;string, object&gt;` |(Optional) Data as key-value pairs for module use (`null` acceptable - not needed for most setups) | |
| `method` | `Method` enum | (Optional) Determines HTTP method used to send data to the Tealium Collect Endpoint | [`Method.POST`, `Method.GET`] |

## Class: `Tealium`

The following summarizes the commonly used methods of the C# `Tealium` class.

| Method | Description |
| ------ | ----------- |
| `Disable()` | Disable Tealium library modules |
| `Enable()`| Enable Tealium library modules |
| `JoinTrace()` | Join a trace |
| `KillTraceSession()` | Kill/end a trace |
| `LeaveTrace()`| Leave a trace |
| `Tealium()` | Tealium constructor |
| `Track()` | Track events |

### `Enable()`

Enable the `Tealium` instance, after a `Disable()` call. Automatically called with the initial initialization. Re-enable the Tealium instance and any internal modules if the library had been disabled prior.   

```csharp
tealium.Enable()
```

### `Disable()`
Diable the `Tealium` instance. Disables library modules from temporarily processing events. It may de-initialize internal class objects.

```csharp
tealium.Disable()
```

### `JoinTrace()`

Join a trace identified by the `traceId` parameter. `traceId` will be sent on all subsequent events as the key, allowing you to debug your events, until the `LeaveTrace()` method is called.  The `traceId` parameter should be generated in advance within Tealium Customer Data Hub.

```csharp
tealium.JoinTrace(traceId);
```

| Parameters | Type | Description  | Example |
|----------- | ----------- | -----| ------- |
| `traceId`  | `string` |Trace ID to join   | `&#34;12345&#34;` |

### `KillTraceSession()`

Kill a trace. Issues a specific event that kills the trace visitor session at the server. This is useful for testing end-of-session behavior in Customer Data Hub.

```csharp
tealiumObj.KillTraceSession();
```

### `LeaveTrace()`

Leave a trace, if one has been joined.

```csharp
tealiumObj.LeaveTrace();
```

### `Tealium()`

Constructor method of the `Tealium` class.

```csharp
Tealium tealium = new Tealium(tealConfig);
```

| Parameters  | Type | Description  |
| ----------- | ----------- | -----|
| `tealConfig` | `Config` | Config instance  |

### `Track()`

Track Events.

```csharp
tealium.Track(title, customData, completion);
```

| Parameters | Type | Description |
| --- | --- | ---  |
| `title` | `string` | Event identifier |
| `customData` | `Dictionary&lt;string, object&gt;` | (Optional) Event data as key-value pairs (set to `null` if none) |
| `completion` | `TrackCompletion` (set to `null` if none)| (Optional) Completion block to trigger after track call |



## Available Modules

The following constant string values are used to enable modules with the current build:

```csharp
config.Modules = new string[] { AppDataModule.Name,
                                CollectModule.Name,
                                LoggerModule.Name };
```

| Module Name | Description |
| --- | --- |
| `AppDataModule` | Adds automatic data points to calls |
| `CollectModule` | Delivers processed events to Tealium Collect endpoint |
| `LoggerModule` | Provides debug output |

Use the `.Name` constant of each Module class.
