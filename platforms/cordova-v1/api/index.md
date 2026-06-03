---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova-v1/api/
---
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](/platforms/cordova/).

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
| `track()`            | Track views by passing `&#34;view&#34;` as the first argument type, or track events by passing `&#34;link&#34;` as the first argument type |
| `trackEvent()`       | Tracks all non-view activity                                                                                               |
| `trackView()`        | Tracks every time a user opens or changes a screen in the app                                                              |


### `addPersistent()`

Adds persistent data to the Tealium persistent data store.

```javascript
tealium.addPersistent(key, data, instance);
```

| Parameter  | Type                   | Description                                                                     | Example                           |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:----------------------------------|
| `key`      | `String`               | Key name of value to be persisted                                               | `&#34;user_hashed_email&#34;`             |
| `data`     | `String` or `[String]` | The value to be persisted for this key                                          | `[&#34;testpersist&#34;, &#34;testpersist2&#34;]` |
| `instance` | `String`               | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`                  |

### `addVolatile()`

Adds data to the Tealium volatile data store.

```javascript
tealium.addVolatile(key, data, instance);
```

| Parameter  | Type                   | Description                                                                     | Example                              |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:-------------------------------------|
| `key`      | `String`               | Key name of value to be persisted                                               | `&#34;user_hashed_email&#34;`                |
| `data`     | `String` or `[String]` | The value to be persisted for this key                                          | `[&#34;testvolatile1&#34;, &#34;testvolatile2&#34;]` |
| `instance` | `String`               | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`                     |


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
| `account`                | `String` | Tealium account name                                                                       | `&#34;companyXYZ&#34;`                                                                                                                                                            |
| `profile`                | `String` | Tealium profile name                                                                       | `&#34;main&#34;`                                                                                                                                                                  |
| `environment`            | `String` | Tealium environment name                                                                   | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]                                                                                                                                               |
| `instance`               | `String` | Tealium instance name (multiple instances supported)                                       | `&#34;tealium_main`                                                                                                                                                           |
| `isLifecycleEnabled`     | `String` | (Optional) String value &#34;true&#34; or &#34;false&#34; to enable lifecycle tracking (default: `&#34;true&#34;`) | [`&#34;true&#34;`, `&#34;false&#34;`]                                                                                                                                                     |
| `collectDispatchURL`     | `String` | Override the full Tealium Collect endpoint URL                                             | `&#34;https: //collect. tealiumiq.com/ vdata/i.gif ?tealium_account =companyXYZ &amp;tealium_profile =main&#34;`                                                                      |
| `collectDispatchProfile` | `String` | Set the profile to use in the Tealium Collect endpoint                                     | `&#34;cordova-demo&#34;`                                                                                                                                                          |
| `isCrashReporterEnabled` | `String` | (Optional and for Android only) Enable crash reporting (uncaught exception handler)        | [`&#34;true&#34;`, `&#34;false&#34;`]                                                                                                                                                     |
| `logLevel`               | `String` | (Optional) Set the log level (defaults to your environment)                                | `tealium.logLevels.DEV` (Info, Warnings, Errors), `tealium.logLevels.QA` (Warnings, Errors), `tealium.logLevels.PROD` (Errors Only), `tealium.logLevels.SILENT` (No Logs) |
| `dataSourceId`           | `String` | (Optional) The data source key                                                             | &#34;abc123&#34;                                                                                                                                                                  |


### `getPersistent()`

Returns a value from the Tealium persistent data. Returns `null` on the JavaScript side if the requested data could not be found.


```javascript
tealium.getPersistent(key, instance, callback);
```

| Parameter  | Type       | Description                                                                     | Example               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | Key name of value to be retrieved from persistent storage                       | `&#34;user_hashed_email&#34;` |
| `instance` | `String`   | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`      |
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
| `key`      | `String`   | Key name of value to be retrieved from volatile storage                         | `&#34;user_hashed_email&#34;` |
| `instance` | `String`   | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`      |
| `callback` | `Function` | Callback object to return the value requested from the persistent storage       | `null`                |


### `removePersistent()`

Removes persistent data from the Tealium persistent data store.

```javascript
tealium.removePersistent(key, instance);
```

| Parameter  | Type     | Description                                                                     | Example               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | Key name of value to be removed from persistent storage                         | `&#34;user_hashed_email&#34;` |
| `instance` | `String` | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`      |


### `removeVolatile()`

Removes volatile data from the Tealium volatile data store.

```javascript
tealium.removeVolatile(key, instance);
```

| Parameter  | Type     | Description                                                                     | Example               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | Key name of value to be removed from volatile memory                            | `&#34;user_hashed_email&#34;` |
| `instance` | `String` | Arbitrary instance name constant, used to refer to a specific tracking instance | `&#34;tealium_main&#34;`      |

### `track()`

Track views by passing `&#34;view&#34;` as the first argument type, or track events by passing `&#34;link&#34;` as the first argument type.


```js
tealium.track(type, data, instance);
```

| Parameter  | Type                   | Description                                                                        | Example                           |
|:-----------|:-----------------------|:-----------------------------------------------------------------------------------|:----------------------------------|
| `type`     | `String`               | Tealium event type name - `&#34;link&#34;` (event) or `&#34;view&#34;` (screen view)               | [`&#34;link&#34;`, `&#34;view&#34;`]              |
| `data`     | JavaScript/JSON object | Populates the data layer for this tracking call with the key-value pairs specified | `{&#34;tealium_event&#34; : &#34;page_view&#34;}` |
| `instance` | `String`               | Tealium instance name - refers to a specific tracking instance                     | `&#34;tealium_main&#34;`                  |

### `trackEvent()`

Tracks all non-view activity.

```js
tealium.trackEvent(data, instance);
```

| Parameter  | Type                   | Description                                                   | Example                         |
|:-----------|:-----------------------|:--------------------------------------------------------------|:--------------------------------|
| `data`     | JavaScript/JSON object | Event data as key-value pairs                                 | `{&#34;tealium_event&#34;: &#34;cart_add&#34;}` |
| `instance` | `String`               | Tealium instance name - refer to a specific tracking instance | `&#34;tealium_main&#34;`                |

### `trackView()`

Tracks every time a user opens or changes a screen in the app.

```js
tealium.trackView(data, instance);
```

| Parameter  | Type                   | Description                   | Example                                                     |
|:-----------|:-----------------------|:------------------------------|:------------------------------------------------------------|
| `data`     | JavaScript/JSON object | `View data as key-value pairs | `{tealium_event:&#34;screen_view&#34;, &#34;screen_name&#34;:&#34;Homescreen&#34;}` |
| `instance` | `String`               | Tealium instance name         | `&#34;tealium_main&#34;`                                            |
