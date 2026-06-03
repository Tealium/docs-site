---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Roku.
url: https://docs.tealium.com/platforms/roku/api/
---
The following lists the available functions in the Tealium for Roku library. Apps for Roku are written in BrightScript, a powerful scripting language. [Learn more](https://sdkdocs.roku.com/display/sdkdoc/BrightScript&#43;Language&#43;Reference) about BrightScript.

## Class: `TealiumBuilder`

The following summarizes the commonly used methods of the `TealiumBuilder` class for the Roku library.

| Method | Description |
| ----- | ------ |
| `SetDatasource()` | Sets the data source key of the `Tealium` object. |
| `SetEnvironment()` | Sets the environment of the `Tealium` object.|
| `SetLogLevel()` | Sets the log level of the `Tealium` object.|
| `TealiumBuilder()` | A builder constructor function to help initialize the `Tealium` object. |

### `SetDatasource()`

Sets the data source key of the `Tealium` object.

```javascript
SetDatasource(datasource)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `datasource` | String | Data source key | `&#34;def456&#34;` |

### `SetEnvironment()`

Sets the environment of the `Tealium` object.

```javascript
SetEnvironment(environment)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `environment` | String | Tealium environment name | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |

### `SetLogLevel()`

Sets the log level of the `Tealium` object.

```javascript
SetLogLevel(logLevel)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `logLevel`  | Integer | Tealium log level | `1` |

### `TealiumBuilder()`

A builder function to help initialize the `Tealium` object. Set optional parameters using the utility functions. Create the Tealium object by calling `Build()`.

```javascript
TealiumBuilder(account, profile, logLevel)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | String | Tealium account name | `&#34;account123&#34;` |
| `profile` | String | Tealium profile name (default: `&#34;main&#34;`) | `&#34;main&#34;` |
| `logLevel` | String | Log level  | `1` |

## Class: `TealiumCore`

The following summarizes the commonly used methods of the `TealiumCore` class for Roku library.

| Method | Description |
| ----- | ------ |
| `ToStr()` | Returns a readable String containing the configuration details of the current Tealium instance. |
| `TrackEvent()` | Tracks an event with associated data and, optionally, triggers a callback function. |
| `ResetSessionId()` | Resets and returns a new session ID. |

### `ToStr()`

Returns a human-readable String containing the configuration details of the current Tealium instance.

```javascript
ToStr()
```

| Returns | Return Type | Example |
| --- | --- | --- |
| Human-readable String containing the configuration details of the current Tealium instance. | String | `&#34;Tealium instance for account: ACCOUNT profile: PROFILE environment: ENV&#34;` |

### `TrackEvent()`

Tracks an event with associated data and, optionally, triggers a callback function.

```javascript
trackEvent(eventType, title, data)
```

| Parameters | Type | Description |
| --- | --- | --- |
| `eventType` | String | Tealium event type (`activity`, `conversion`, `derived`, `interaction`, or `view`). |
| `eventName` | String | Name of event (becomes the `event_name` attribute in Tealium Customer Data Hub). |
| `data` | Object | Contextual event data, an `roAssociativeArray` object containing keys-value pairs .|

### `ResetSessionId()`

Resets and returns a new session ID. The session ID identifies the current user session, similar to a website session, but it does not expire. A new session ID is created each time `createTealium()` is called. 

```javascript
resetSessionId() as Integer
```
| Returns | Return Type |
| --- | --- |
| A new session ID | Integer |