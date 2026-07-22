---
title: VisitorService
description: Reference guide for VisitorService class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/visitor-service/
---
## Class: `VisitorService`

The following summarizes the commonly used methods and properties of the `VisitorService` module for Kotlin.

| Method/Property | Description |
| ----- | ------ |
| [`overrideVisitorServiceUrl`](#overridevisitorserviceurl) | `TealiumConfig` option to override the URL used to retrieve the current VisitorProfile |
| [`overrideVisitorServiceProfile`](#overridevisitorserviceprofile) | `TealiumConfig` option to override the profile name used to retrieve the current VisitorProfile |
| [`requestVisitorProfile()`](#requestvisitorprofile) | Method to request that the current VisitorProfile be updated |
| [`visitorServiceRefreshInterval`](#visitorservicerefreshinterval) | `TealiumConfig` option to set the minimum time interval before the SDK will automatically retrieve the latest VisitorProfile |

### `overrideVisitorServiceUrl`

Extension property on the `TealiumConfig` object; only available when the VisitorService module is included in your project.

Overrides the URL used by the VisitorService module to get the VisitorProfile object.
Default URL: `"https://visitor-service.tealiumiq.com/{ACOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}"`

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = url
```

### `overrideVisitorServiceProfile`

Extension property on the `TealiumConfig` object; only available when the VisitorService module is included in your project.

Overrides the Tealium profile name used by the VisitorService module to fetch the VisitorProfile object. By default the VisitorService module uses the profile name set in `TealiumConfig`.

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = "main"
```

### `requestVisitorProfile`

Method to request that the VisitorProfile be updated. This happens after each dispatch, or batch of dispatches, has been sent to the Tealium Customer Data Hub.

Use this method to request an update at any other point in time. It's a `suspend` function that needs to be called from a coroutine. As it makes a network request, your coroutine is not called on main thread.

```java
runBlocking(Dispatchers.IO) {
    tealium.visitorService?.requestVisitorProfile()
}
```

### `visitorServiceRefreshInterval`

Sets the time interval in seconds between updates to the VisitorProfile data. Calls to `requestVisitorProfile()` ignore this setting.

Default: 300 (5 minutes)

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## Interface: `VisitorUpdatedListener`

The `VisitorUpdatedListener` is a listener class. Register to receive the latest version of the VisitorProfile each time there has been an update. There is only a single method to implement: [`onVisitorUpdated(visitorProfile: VisitorProfile)`](#onVisitorUpdated).

### `onVisitorUpdated`

Implement the `onVisitorUpdated` method on an existing class, or pass in an anonymous object after creating your `Tealium` instance. The below example shows the latter.

```java
val tealium = Tealium.create(...) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

See the [VisitorProfile](https://docs.tealium.com/platforms/android-kotlin/api/visitor-profile/) documentation for full details on available properties.
