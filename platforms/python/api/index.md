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
| `account` | `String` |Tealium account name |  `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealium profile name |  `&#34;main&#34;`  |
| `environment` | `String` |Tealium environment name | `&#34;prod&#34;`|
| `datasource`  | `String` |(Optional) data source key (required if PATH is omitted)  | `&#34;abc123&#34;` |

### `trackEvent()`

Track events with optional parameters for data and a callback.

```python
trackEvent(title, data, callback)
```

| Parameter | Type | Description | Example
|-----------| ---- | -------------| --- |
| `title`   | `String` | A name to identify the event, such as a `user_login` variable | `&#34;test&#34;` |
| `data`    | `Dictionary` | (Optional) Object with event data as key-value pairs | `{&#34;foo&#34;: &#34;bar&#34;, &#34;tealium_visitor_id&#34;: &#34;1234567890&#34;}` |
| `callback`| `Dictionary`   | (Optional) Object with a function assigned to the &#34;callback&#34; key | `callback = self.tealiumCallback` |
