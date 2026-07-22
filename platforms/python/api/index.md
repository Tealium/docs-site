---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Python.
url: https://docs.tealium.com/platforms/python/api/
---

## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for Python library.

| Method | Description |
| ----- | ------ |
| `Tealium()` | Constructor to create a `Tealium` object that is used to track events |
| `trackEvent()` | Track events with optional parameters for data and a callback |

### `Tealium()`

Creates a `Tealium` object that is used to track events.

```python
Tealium(account, profile, environment, path, datasource)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` |Tealium account name |  `"companyXYZ"` |
| `profile` | `String` |Tealium profile name |  `"main"`  |
| `environment` | `String` |Tealium environment name | `"prod"`|
| `datasource`  | `String` |(Optional) data source key (required if PATH is omitted)  | `"abc123"` |

### `trackEvent()`

Track events with optional parameters for data and a callback.

```python
trackEvent(title, data, callback)
```

| Parameter | Type | Description | Example
|-----------| ---- | -------------| --- |
| `title`   | `String` | A name to identify the event, such as a `user_login` variable | `"test"` |
| `data`    | `Dictionary` | (Optional) Object with event data as key-value pairs | `{"foo": "bar", "tealium_visitor_id": "1234567890"}` |
| `callback`| `Dictionary`   | (Optional) Object with a function assigned to the "callback" key | `callback = self.tealiumCallback` |
