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
| `data` | JSON Object | Page view data as key-value pairs | `{&#34;tealium_event&#34; : &#34;user_login&#34;, &#34;customer_id&#34; : &#34;0123456789&#34;}` |

### `setConfig()`

Config settings used to build the path to the `utag.js` file.

```javascript
setConfig(config : {account, profile, environment})
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `string` | Tealium account name | `&#34;companyXYZ&#34;` |
| `profile` | `string` | Tealium profile name | `&#34;main&#34; ` |
| `environment` | `string` | Tealium environment name | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |

### `view()`

Track page views.

```javascript
view(data? : any)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | JSON Object | Event data as key-value pairs | `{&#34;tealium_event&#34; : &#34;product_view&#34;, &#34;page_type&#34; : &#34;product&#34;, &#34;product_id&#34; : [&#34;PROD123&#34;]}` |
