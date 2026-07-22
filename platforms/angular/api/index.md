---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Angular.
url: https://docs.tealium.com/platforms/angular/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the Angular `Tealium` class.

| Method | Description |
| ----- | ------ |
| `link()` | Track in-page events |
| `setConfig()` |  Config settings used to build the path to the `utag.js` file |
| `view()` | Track page views |


### `link()`

Track in-page events.

```javascript
link(data? : any)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | JSON Object | Page view data as key-value pairs | `{"tealium_event" : "user_login", "customer_id" : "0123456789"}` |

### `setConfig()`

Config settings used to build the path to the `utag.js` file.

```javascript
setConfig(config : {account, profile, environment})
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `string` | Tealium account name | `"companyXYZ"` |
| `profile` | `string` | Tealium profile name | `"main" ` |
| `environment` | `string` | Tealium environment name | [`"dev"`, `"qa"`, `"prod"`] |

### `view()`

Track page views.

```javascript
view(data? : any)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | JSON Object | Event data as key-value pairs | `{"tealium_event" : "product_view", "page_type" : "product", "product_id" : ["PROD123"]}` |
