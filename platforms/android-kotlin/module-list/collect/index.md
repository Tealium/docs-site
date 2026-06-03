---
title: Collect Module
description: Sends events to Tealium Customer Data Hub.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/collect/
---
## Usage

The Collect module dispatches tracking calls to the Tealium Customer Data Hub. Usage of this module is strongly recommended if you are using server-side products.

Alternatively, if you have Tealium iQ, use the Tealium Collect tag in partnership with the [Tag Management Dispatcher](/platforms/android-kotlin/module-list/tag-management/).

## Install

Install the Collect Dispatcher module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the Maven dependencies for the Tealium library and Collect Dispatcher
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-collect-dispatcher:1.1.1&#39;
      }
      ```

### Manual

To install the Collect Dispatcher manually:

1. Download the Tealium [Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher) module.

2. Copy the file `tealium-kotlin.collect-1.1.1.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
    ```groovy
    dependencies {
        implementation(name:&#39;tealium-kotlin.collect-1.1.1&#39;, ext:&#39;aar&#39;)
    }
    ```
The Collect Dispatcher has a dependency on the main Tealium Kotlin SDK, so ensure that you also make this available by following the [installation instructions](/platforms/android-kotlin/install/).

## Configuration Options

Configure the URL that the Collect Dispatcher sends your data to using the following setting when creating your TealiumConfig object:

```kotlin
val config = TealiumConfig(...)
config.overrideCollectUrl = &#34;https://your.endpoint.com/event&#34;
config.overrideCollectBatchUrl = &#34;https://your.endpoint.com/bulk-event&#34;
```

Configure the endpoints that individual events or [batched events](/platforms/getting-started-mobile/event-batching/) are sent to.

For deployments that make use of the CNAME or data-center specific requirements, override the domain and keep the Tealium defined endpoints. In the following example, individual events go to `https://cname.tealiumiq.com/event` and batched events go to `https://cname.tealiumiq.com/bulk-event`:

```kotlin
val config = TealiumConfig(...)
config.overrideCollectDomain = &#34;cname.tealiumiq.com&#34;
```

If you need to send events to a Tealium Profile that is different to the one used in the `TealiumConfig` object, then you can override this as follows - this has the effect of changing the value of the `tealium_profile` key in the event payload:
```kotlin
val config = TealiumConfig(..., profile=&#34;android&#34;, ...)
config.overrideCollectProfile = &#34;main&#34;
```
