---
title: AdobeVisitorService Module
description: Provides a central cross-device visitor ID for each user.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/adobe-visitor-service/
---
The Adobe Visitor Service module interfaces directly with Adobe’s REST API to retrieve and maintain the Experience Cloud ID (ECID) for visitors.

Learn more about the [AdobeVisitorService](https://docs.tealium.com/platforms/getting-started-mobile/adobe-visitor-service/) module.

## Requirements

* [Tealium Kotlin for Android](https://docs.tealium.com/platforms/android-kotlin/)
* Valid Adobe account and Adobe organization ID

## Sample App

Explore the [AdobeVisitorService module sample app](https://github.com/Tealium/tealium-kotlin/tree/master/mobile) for Android to further your knowledge of the Tealium library and best practice implementations.

## Install

The AdobeVisitorService module is configured when initializing the Tealium SDK, and does not have remote configuration capabilities.

The module acts as a `DispatchValidator`, preventing calls being sent without an Adobe organization ID. It attempts to retrieve an ECID from the Adobe API, but after 5 failed attempts, calls are permitted to continue without an ECID to avoid data loss. Sending data is prioritized over having a valid ECID.

Possible causes for no ECID being retrieved are:

- Invalid response, such as a response was received but did not contain a valid ECID.
- There was no response.
- The Adobe organization ID was invalid.

### Maven

Add Tealium Maven Repo: http://maven.tealiumiq.com/releases/

Add dependency: `com.tealium:kotlin-adobe-visitor`


```kotlin
import com.tealium.adobe.api.AdobeAuthState
import com.tealium.adobe.api.AdobeVisitor
import com.tealium.adobe.api.ResponseListener
import com.tealium.adobe.kotlin.*

...

val config = TealiumConfig(
      app,
      "<account>",
      "<profile>",
      Environment.DEV,
      collectors = mutableSetOf(Collectors.AdobeVisitor),
      dispatchers = mutableSetOf(Dispatchers.Collect)
  )
  config.adobeVisitorOrgId = BuildConfig.ADOBE_ORG_ID

  tealium = Tealium.create(BuildConfig.TEALIUM_INSTANCE, config)
```


<blockquote>
To link a known visitor ID or set the authentication state, see [Set a known visitor ID and authentication state](https://docs.tealium.com/platforms/getting-started-mobile/adobe-visitor-service/#set-a-known-visitor-id-and-authentication-state).
</blockquote>

