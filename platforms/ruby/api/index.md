---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Ruby.
url: https://docs.tealium.com/platforms/ruby/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for the Ruby library.

| Method | Description |
| ----- | ------ |
| `initialize()` | Initialize the Tealium instance. Called by `Tealium.new `.|
| `track()` | Track events |



### `initialize()`

Initialize the Tealium instance.

```ruby
initialize(account, profile, datasource)
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | Tealium account name | `&#34;account123&#34;` |
| `profile` | `String` | Tealium profile name | `&#34;main&#34;` |
| `datasource` | String | Data source key (`nil` if none provided) | `&#34;abc123&#34;` |

 When you call the method `new` on the Tealium class, as in `Tealium.new`, the class creates a new instance of itself. It will then, internally, call the `initialize()` method on the new object. Doing so it will simply pass all the arguments that you passed to new on to the `initialize()` method.

### `track()`

Tracks events.

```ruby
track(event_name, data)
```

| Parameter | Type |  Description | Example |
|------|------|-------| ------|
| `event`   | `String` |Title of the tracked event |  `&#34;some event&#34;` |
| `data`    | `Hash` | (Optional) Event data as key-value pairs |  `{:key =&gt; &#34;value&#34;}` |
