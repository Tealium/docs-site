---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova-v1/api/
---

<blockquote>
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](https://docs.tealium.com/platforms/cordova/).
</blockquote>


## Class: `Tealium`

The following summarizes the commonly used methods of the Cordova `Tealium` class.

| Method               | Description                                                                                                                |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------------|
| `addPersistent()`    | Adds data to the Tealium persistent data store                                                                             |
| `addVolatile()`      | Adds data to the Tealium volatile data store                                                                               |
| `init()`             | Initializes the Tealium Cordova plugin                                                                                     |
| `getPersistent()`    | Returns a value from the Tealium persistent data                                                                           |
| `getVisitorID()`     | Returns the current Tealium visitor ID for the current user                                                                |
| `getVolatile()`      | Returns a value from the Tealium volatile data store                                                                       |
| `removePersistent()` | Removes data from the Tealium persistent data store                                                                        |
| `removeVolatile()`   | Removes volatile data from the Tealium volatile data store                                                                 |
| `track()`            | Track views by passing `"view"` as the first argument type, or track events by passing `"link"` as the first argument type |
| `trackEvent()`       | Tracks all non-view activity                                                                                               |
| `trackView()`        | Tracks every time a user opens or changes a screen in the app                                                              |


### `addPersistent()`

Adds persistent data to the Tealium persistent data store.

```javascript
tealium.addPersistent(key, data, instance);
```

| Parameter  | Type                   | Description                                                                     | Example                           |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:----------------------------------|
| `key`      | `String`               | Key name of value to be persisted                                               | `"user_hashed_email"`             |
| `data`     | `String` or `[String]` | The value to be persisted for this key                                          | `["testpersist", "testpersist2"]` |
| `instance` | `String`               | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`                  |

### `addVolatile()`

Adds data to the Tealium volatile data store.

```javascript
tealium.addVolatile(key, data, instance);
```

| Parameter  | Type                   | Description                                                                     | Example                              |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:-------------------------------------|
| `key`      | `String`               | Key name of value to be persisted                                               | `"user_hashed_email"`                |
| `data`     | `String` or `[String]` | The value to be persisted for this key                                          | `["testvolatile1", "testvolatile2"]` |
| `instance` | `String`               | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`                     |


### `init()`

Initializes the Tealium Cordova plugin.

```java
tealium.init(config, successCallBack, errorCallback);
```

| Parameter         | Type                   | Description                                                             |
|:------------------|:-----------------------|:------------------------------------------------------------------------|
| `config`          | JavaScript/JSON object | The config object (see table below)                                     |
| `successCallback` | Function               | Overrides the default Success Callback to allow custom success handling |
| `errorCallback`   | Function               | Overrides the default Success Callback to allow custom success handling |

The `config` object is passed as the first argument, and contains the following data:

```java
tealium.init({account, profile, environment, instance,
                isLifecycleEnabled,
                collectDispatchURL,
                collectDispatchProfile,
                isCrashReporterEnabled,
                logLevel,
                dataSourceId});
```

| Parameter                | Type     | Description                                                                                | Example                                                                                                                                                                   |
|:-------------------------|:---------|:-------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `account`                | `String` | Tealium account name                                                                       | `"companyXYZ"`                                                                                                                                                            |
| `profile`                | `String` | Tealium profile name                                                                       | `"main"`                                                                                                                                                                  |
| `environment`            | `String` | Tealium environment name                                                                   | [`"dev"`, `"qa"`, `"prod"`]                                                                                                                                               |
| `instance`               | `String` | Tealium instance name (multiple instances supported)                                       | `"tealium_main`                                                                                                                                                           |
| `isLifecycleEnabled`     | `String` | (Optional) String value "true" or "false" to enable lifecycle tracking (default: `"true"`) | [`"true"`, `"false"`]                                                                                                                                                     |
| `collectDispatchURL`     | `String` | Override the full Tealium Collect endpoint URL                                             | `"https: //collect. tealiumiq.com/ vdata/i.gif ?tealium_account =companyXYZ &tealium_profile =main"`                                                                      |
| `collectDispatchProfile` | `String` | Set the profile to use in the Tealium Collect endpoint                                     | `"cordova-demo"`                                                                                                                                                          |
| `isCrashReporterEnabled` | `String` | (Optional and for Android only) Enable crash reporting (uncaught exception handler)        | [`"true"`, `"false"`]                                                                                                                                                     |
| `logLevel`               | `String` | (Optional) Set the log level (defaults to your environment)                                | `tealium.logLevels.DEV` (Info, Warnings, Errors), `tealium.logLevels.QA` (Warnings, Errors), `tealium.logLevels.PROD` (Errors Only), `tealium.logLevels.SILENT` (No Logs) |
| `dataSourceId`           | `String` | (Optional) The data source key                                                             | "abc123"                                                                                                                                                                  |


### `getPersistent()`

Returns a value from the Tealium persistent data. Returns `null` on the JavaScript side if the requested data could not be found.


```javascript
tealium.getPersistent(key, instance, callback);
```

| Parameter  | Type       | Description                                                                     | Example               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | Key name of value to be retrieved from persistent storage                       | `"user_hashed_email"` |
| `instance` | `String`   | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`      |
| `callback` | `Function` | Callback object to return the value requested from the persistent storage       | `null`                |

### `getVisitorID()`

Returns the current Tealium visitor ID for the current user.

| Returns            | Return Type |
|:-------------------|:------------|
| Current visitor ID | `String`    |

### `getVolatile()`

Returns a value from the Tealium volatile data store. Returns `null` on the JavaScript side if the requested data could not be found.

```javascript
tealium.getVolatile(key, instance, callback);
```

| Parameter  | Type       | Description                                                                     | Example               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | Key name of value to be retrieved from volatile storage                         | `"user_hashed_email"` |
| `instance` | `String`   | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`      |
| `callback` | `Function` | Callback object to return the value requested from the persistent storage       | `null`                |


### `removePersistent()`

Removes persistent data from the Tealium persistent data store.

```javascript
tealium.removePersistent(key, instance);
```

| Parameter  | Type     | Description                                                                     | Example               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | Key name of value to be removed from persistent storage                         | `"user_hashed_email"` |
| `instance` | `String` | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`      |


### `removeVolatile()`

Removes volatile data from the Tealium volatile data store.

```javascript
tealium.removeVolatile(key, instance);
```

| Parameter  | Type     | Description                                                                     | Example               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | Key name of value to be removed from volatile memory                            | `"user_hashed_email"` |
| `instance` | `String` | Arbitrary instance name constant, used to refer to a specific tracking instance | `"tealium_main"`      |

### `track()`

Track views by passing `"view"` as the first argument type, or track events by passing `"link"` as the first argument type.


```js
tealium.track(type, data, instance);
```

| Parameter  | Type                   | Description                                                                        | Example                           |
|:-----------|:-----------------------|:-----------------------------------------------------------------------------------|:----------------------------------|
| `type`     | `String`               | Tealium event type name - `"link"` (event) or `"view"` (screen view)               | [`"link"`, `"view"`]              |
| `data`     | JavaScript/JSON object | Populates the data layer for this tracking call with the key-value pairs specified | `{"tealium_event" : "page_view"}` |
| `instance` | `String`               | Tealium instance name - refers to a specific tracking instance                     | `"tealium_main"`                  |

### `trackEvent()`

Tracks all non-view activity.

```js
tealium.trackEvent(data, instance);
```

| Parameter  | Type                   | Description                                                   | Example                         |
|:-----------|:-----------------------|:--------------------------------------------------------------|:--------------------------------|
| `data`     | JavaScript/JSON object | Event data as key-value pairs                                 | `{"tealium_event": "cart_add"}` |
| `instance` | `String`               | Tealium instance name - refer to a specific tracking instance | `"tealium_main"`                |

### `trackView()`

Tracks every time a user opens or changes a screen in the app.

```js
tealium.trackView(data, instance);
```

| Parameter  | Type                   | Description                   | Example                                                     |
|:-----------|:-----------------------|:------------------------------|:------------------------------------------------------------|
| `data`     | JavaScript/JSON object | `View data as key-value pairs | `{tealium_event:"screen_view", "screen_name":"Homescreen"}` |
| `instance` | `String`               | Tealium instance name         | `"tealium_main"`                                            |
