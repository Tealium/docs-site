---
title: Visitor Service Module
description: Fetches the latest profile for the current visitor.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/visitor-service/
---
## Usage

The Visitor Service module brings [data layer enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) functionality to the native mobile app.

Usage of this module requires a license for Tealium AudienceStream. Use the retrieved visitor profile to enhance the customer experience or data layer throughout your application.

## Install

Install the Visitor Service module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library and Visitor Service Module
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-visitor-service:1.2.0'
      }
      ```

### Manual

To install the Visitor Service Module manually:

1. Download the Tealium [Visitor Service](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice) module.

2. Copy the file `tealium-kotlin.visitorservice-1.2.0.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.visitorservice-1.2.0', ext:'aar')
      }
      ```


<blockquote>
The Collect Dispatcher has a dependency on the main Tealium Kotlin SDK, so ensure that you also make this available by following the [installation instructions](https://docs.tealium.com/platforms/android-kotlin/install).
</blockquote>


## Visitor Profile Data

To make use of the current visitor data you need to register a delegate object to receive the latest Visitor Profile each time it gets updated:

```java
instance = Tealium.create("main", config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

The VisitorProfile object have access to many fields relating to your Visitor - the following outlines the available properties:

| Parameters | Properties |  Value |
| --- | --- | --- |
| `arraysOfBooleans` | key: String, value: List\<Boolean\> | `key: "5129", value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | key: String, value: List\<Double\>| `key: "57", value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | key: String, value: List\<String\> | `key: "5213", value: listOf("green shirts", "green shirts", "blue shirts")` |
| `audiences` | key: String, name: String | `key: "tealiummobile_demo_103", name: "Kotlin Users"` |
| `badges` | key: String, value: Boolean | `key: "2815", value: true` |
| `booleans` | key: String, value: Boolean | `key: "4868", value: true `|
| `currentVisit` | All attributes for current visit profile. The current visit profile does not contain Audiences or Badges. | `CurrentVisit` |
| `dates` | key: String, value: Long | `key: "22", value: 1567120112000` |
| `numbers` | key: String, value: Double | `key: "5728", value: 4.82125` |
| `setsOfStrings` | key: String, value: Set\<String\> | `key: "5211", value: setOf("green shirts", "red shirts", "blue shirts")` |
| `strings` | key: String, value: String | `key: "5380", value: "green shirts"` |
| `tallies` | key: String, value: Map<String, Double> |  `key: "57", mapOf("category 1" to 2.0, "category 2" to 1.0)` |


Below is a basic example of how to interact with the Visitor Profile once it has been retrieved. Key names differ per account/profile.
```java
val returningVisitor = visitorProfile.badges?.get("returning_visitor")
returningVisitor?.let {
    if (returningVisitor == true) {
        val ltv = visitorProfile.numbers?.get("lifetime_value")
        // take action
    }
}
```


## Configuration Options

Configure the URL that it used to retrieve the Visitor Profile using the following setting when creating your TealiumConfig object:

### Override Visitor Service Url

Sets the URL to use when fetching updates to the visitor profile.

See: [`TealiumConfig.overrideVisitorServiceUrl`](https://docs.tealium.com/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = "https://your.preferred.visitor-service.com"
```

Default: `https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### Override Visitor Service Profile

Sets the Tealium profile to use when fetching updates to the visitor profile. See: [`TealiumConfig.overrideVisitorServiceProfile`](https://docs.tealium.com/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = "someOtherTealiumProfile"
```

### Visitor Profile Refresh Interval

Sets the time interval, in seconds, between calls to get the latest VisitorProfile data. See: [`TealiumConfig.visitorServiceRefreshInterval`](https://docs.tealium.com/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval). 

Default: 300 (5 minutes)

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## API Reference

For the reference of methods used by the Visitor Service module, see the [`VisitorService`](https://docs.tealium.com/platforms/android-kotlin/api/visitor-service/) class in the Tealium SDK for Android API.
