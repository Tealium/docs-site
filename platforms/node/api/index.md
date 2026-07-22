---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Node.
url: https://docs.tealium.com/platforms/node/api/
---

## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for the Node library.

| Method | Description |
| ----- | ------ |
| `addModule()` | Add a module |
| `Tealium()`| Constructor to build the Tealium instance |
| `track()` | Track views and events |

### `addModule()`

Add a module to the tealium instance


```javascript
addModule(module)
```

| Parameter | Type | Description | Example
|-----------|------| --- | --- |
| `module` |  `var` |  Module name | `tealiumCollect` |

### `Tealium()`
Constructor to build the Tealium instance

```javascript
Tealium(config);
```

| Parameter | Type | Description | Example
|-----------|------| --- | --- |
| `config` | var | Tealium configuration object data as key-value pairs | `{"account":"ACCOUNT", "profile":"PROFILE", "datasource":"DATASOURCE"};` |

The `config` object parameter has the following has the following key-value pairs

| Parameter | Type | Description | Example
|-----------|------| --- | --- |
| `account` |  `String` |  Tealium profile name | `"companyXYZ"` |
| `profile` | `String`| Tealium profile name | `"main"` |
| `datasource` | `String` | (Optional) The data source key | `"abc123"` |
### `track()`

Tracks views and events.

```javascript
tealium.track(event, data); 
```

| Parameters | Type | Description | Example |
| --- |  --- | --- | --- |
| `event` | `String` | Name of the event (sets the value of `tealium_event`)| `"event"` |
| `data` | `Dictionary` | Object with event data as key-value pairs | `{"some_key": "some_value"}` |
