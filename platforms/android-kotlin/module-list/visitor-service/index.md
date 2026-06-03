---
title: Visitor Service Module
description: Fetches the latest profile for the current visitor.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/visitor-service/
---
## Usage

The Visitor Service module brings [data layer enrichment]() functionality to the native mobile app.

Usage of this module requires a license for Tealium AudienceStream. Use the retrieved visitor profile to enhance the customer experience or data layer throughout your application.

## Install

Install the Visitor Service module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the Maven dependencies for the Tealium library and Visitor Service Module
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-visitor-service:1.2.0&#39;
      }
      ```

### Manual

To install the Visitor Service Module manually:

1. Download the Tealium [Visitor Service](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice) module.

2. Copy the file `tealium-kotlin.visitorservice-1.2.0.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.visitorservice-1.2.0&#39;, ext:&#39;aar&#39;)
      }
      ```

The Collect Dispatcher has a dependency on the main Tealium Kotlin SDK, so ensure that you also make this available by following the [installation instructions](/platforms/android-kotlin/install).

## Visitor Profile Data

To make use of the current visitor data you need to register a delegate object to receive the latest Visitor Profile each time it gets updated:

```java
instance = Tealium.create(&#34;main&#34;, config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev(&#34;--&#34;, &#34;VisitorProfile updated: $visitorProfile&#34;)
        }
    })
}
```

The VisitorProfile object have access to many fields relating to your Visitor - the following outlines the available properties:

| Parameters | Properties |  Value |
| --- | --- | --- |
| `arraysOfBooleans` | key: String, value: List\&lt;Boolean\&gt; | `key: &#34;5129&#34;, value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | key: String, value: List\&lt;Double\&gt;| `key: &#34;57&#34;, value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | key: String, value: List\&lt;String\&gt; | `key: &#34;5213&#34;, value: listOf(&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;)` |
| `audiences` | key: String, name: String | `key: &#34;tealiummobile_demo_103&#34;, name: &#34;Kotlin Users&#34;` |
| `badges` | key: String, value: Boolean | `key: &#34;2815&#34;, value: true` |
| `booleans` | key: String, value: Boolean | `key: &#34;4868&#34;, value: true `|
| `currentVisit` | All attributes for current visit profile. The current visit profile does not contain Audiences or Badges. | `CurrentVisit` |
| `dates` | key: String, value: Long | `key: &#34;22&#34;, value: 1567120112000` |
| `numbers` | key: String, value: Double | `key: &#34;5728&#34;, value: 4.82125` |
| `setsOfStrings` | key: String, value: Set\&lt;String\&gt; | `key: &#34;5211&#34;, value: setOf(&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;)` |
| `strings` | key: String, value: String | `key: &#34;5380&#34;, value: &#34;green shirts&#34;` |
| `tallies` | key: String, value: Map&lt;String, Double&gt; |  `key: &#34;57&#34;, mapOf(&#34;category 1&#34; to 2.0, &#34;category 2&#34; to 1.0)` |


Below is a basic example of how to interact with the Visitor Profile once it has been retrieved. Key names differ per account/profile.
```java
val returningVisitor = visitorProfile.badges?.get(&#34;returning_visitor&#34;)
returningVisitor?.let {
    if (returningVisitor == true) {
        val ltv = visitorProfile.numbers?.get(&#34;lifetime_value&#34;)
        // take action
    }
}
```


## Configuration Options

Configure the URL that it used to retrieve the Visitor Profile using the following setting when creating your TealiumConfig object:

### Override Visitor Service Url

Sets the URL to use when fetching updates to the visitor profile.

See: [`TealiumConfig.overrideVisitorServiceUrl`](/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = &#34;https://your.preferred.visitor-service.com&#34;
```

Default: `https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### Override Visitor Service Profile

Sets the Tealium profile to use when fetching updates to the visitor profile. See: [`TealiumConfig.overrideVisitorServiceProfile`](/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = &#34;someOtherTealiumProfile&#34;
```

### Visitor Profile Refresh Interval

Sets the time interval, in seconds, between calls to get the latest VisitorProfile data. See: [`TealiumConfig.visitorServiceRefreshInterval`](/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval). 

Default: 300 (5 minutes)

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## API Reference

For the reference of methods used by the Visitor Service module, see the [`VisitorService`](/platforms/android-kotlin/api/visitor-service/) class in the Tealium SDK for Android API.
