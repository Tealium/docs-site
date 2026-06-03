---
title: Tealium.Config
description: Reference guide for Tealium.Config class and methods provided by Tealium for Android.
url: https://docs.tealium.com/platforms/android-java/api/tealium-config/
---

## Class: `Tealium.Config`

The following summarizes the commonly used methods of the `Tealium.Config` class.

| Method | Description |
| ----- | ------ |
| [`create()`](#create)| Create instance of the Config object |
| [`enableConsentManager()`](#enableconsentmanager)| Enable consent manager |
| [`isConsentManagerEnabled()`](#isconsentmanagerenabled)| Checks if consent manager is enabled |
| [`sessionCountingEnabled`](#sessioncountingenabled) | Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files |
| [`setDatasourceId()`](#setdatasourceid) | Sets the data source key |
| [`setForceOverrideLogLevel()`](#setforceoverrideloglevel) | Set to force a specific log level at init time |
| [`setOverrideCollectDispatchProfile()`](#setoverridecollectdispatchprofile) | Overrides the Tealium Collect profile |
| [`setOverrideCollectDispatchUrl()`](#setoverridecollectdispatchurl) | Overrides the Tealium Collect URL |
| [`setOverrideVisitorServiceDomain()`](#setoverridevisitorservicedomain) | Overrides the Tealium Collect visitor service domain |
| [`setSecondsBeforeBatchTimeout()`](#setsecondsbeforebatchtimeout) | Sets the number of seconds before batch timeout |

### `create()`

Create instance of the Config object.

```java
Tealium.Config config = Tealium.Config.create(
      application,
      account,
      profile,
      environment);
```

The Tealium `Config` instance is configured with the following parameters:

| Parameters  | Type | Description | Example |
| --- | --- | --- | --- |
| `application` | `Application` |The application instance |  `applicationObj` |
| `account` | `String` |Tealium account name |  `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealium profile name |  `&#34;main&#34;` |
| `environment` | `String` |Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |

### `enableConsentManager()`

Enable consent manager. This method is to be used before Tealium initialization.

```java
public final String TEALIUM_INSTANCE = &#34;main&#34;;
final Tealium.Config config = Tealium.Config.create(...);
config.enableConsentManager(TEALIUM_INSTANCE);
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `instance` | `String` | Tealium instance name | `&#34;main&#34;` |

### `isConsentManagerEnabled()`

Checks if consent manager is enabled.

```java
config.isConsentMangerEnabled()
```

### `sessionCountingEnabled`
Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files. Default `true`.                         

```swift
config.sessionCountingEnabled = false
```

### `setDatasourceId()`

Sets the data source key.

```java
config.setDataSourceId(dataSourceId);
```
| Parameters  | Type | Description | Example |
| --- | --- | --- | --- |
| `dataSourceId` | `String` | Data source key (Set to `null` if none) | `&#34;abc123&#34;` |

### `setForceOverrideLogLevel()`

Set to force a specific log level at init time. Returns instance of the config object for method chaining.

```java
config.setForceOverrideLogLevel(forceOverrideLogLevel);
```

The following `String` options are available for `forceOverrideLogLevel`:

| Log Level | Description                     |
|------------ | ------------------------------- |
| `&#34;dev&#34;`     | Activity, Info, Warnings, and Errors|
| `&#34;qa&#34;`      | Info, Warnings, and Errors      |
| `&#34;prod&#34;`    | Errors                          |
| `&#34;silent&#34;`  | None |

### `setOverrideCollectDispatchProfile()`

Overrides the Tealium Collect dispatch profile.

```java
config.setOverrideCollectDispatchProfile(profile);
```

| Parameters  | Type | Description |
| --- | --- | --- |
| `profile` | `String` | The Tealium Collect profile to override |


### `setOverrideCollectDispatchUrl()`

Overrides the Tealium Collect dispatch URL to send data to a different endpoint.

```java
config.setOverrideCollectDispatchUrl(url);
```

| Parameters  | Type | Description |
| --- | --- | --- |
| `url` | `String` | The URL to override |

The default URL is:  
```bash
https://collect.tealiumiq.com/event/
```
The default URL with event batching is:
```bash
https://collect.tealiumiq.com/bulk-event/
```
The method is typically used to set a custom hostname, or to set a specific region hostname. The following example sets the Tealium Collect base URL to stay within the EU Central region:

```java
config.setOverrideCollectDispatchUrl(&#34;https://collect-eu-central-1.tealiumiq.com/event/&#34;);
```


### `setOverrideVisitorServiceDomain()`

Overrides the Tealium Collect visitor service domain to send data to a different domain.

```java
config.setOverrideVisitorServiceDomain(domain);
```

| Parameters  | Type | Description |
| --- | --- | --- |
| `domain` | `String` | The visitor service domain to override |

### `setSecondsBeforeBatchTimeout()`

Sets the number of seconds before batch timeout. If the batch size limit has not been reached before reaching the timeout, the queued events are dispatched.

```java
config.setSecondsBeforeBatchTimeout(timeout);
```

| Parameters  | Type | Description | Example |
| --- | --- | --- | --- |
| `timeout` | `int` |The timeout, in seconds, for the batch to be sent. | `30` |
