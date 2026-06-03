---
title: Ad Identifier Module
description: Provides the ability to make use of the device "Ad Identifier" (ADID) to help identify interactions with display ad networks.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/adid/
---
## Requirements

* [Google Play Services SDK](https://developers.google.com/android/guides/setup)

## Install

Install the Ad Identifier module with Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies{
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-ad-identifier:1.1.1&#39;
      }
      ```

### Manual

To install the Ad Identifier module manually:

1. Download the Tealium [AdIdentifier](https://github.com/Tealium/tealium-kotlin/tree/master/adidentifier) module.

2. In your top-level `build.gradle` file, verify the following:  
      ```groovy
      allprojects {
            repositories {
            mavenCentral()
            flatDir {
                  dirs &#39;libs&#39;
            }
            }
      }
      ```

3. Copy the file `tealium.adidentifier-1.1.1.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation (name:&#39;tealium-kotlin.adidentifier-1.1.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## Initialize

Initialize the Ad Identifier module, as shown in the following example:

```kotlin
val config = TealiumConfig(application,
              &#34;ACCOUNT&#34;,
              &#34;PROFILE&#34;,
              ENVIRONMENT,
              modules = mutableSetOf(Modules.AdIdentifier), // Ad Identifier module
              dispatchers = mutableSetOf(Dispatchers.Collect,
              Dispatchers.TagManagement,
              Dispatchers.RemoteCommands)
)
```

## Data Layer

The Ad Identifier module adds the following variables to the data layer:

| Variable | Type | Description | Example |
| --- | --- | --- | --- |     
| `google_adid` | `String` | The Google Ad Identifier | `ca-app-pub-0123456789012345~0123456789` |
| `google_limit_ad_tracking` | `Boolean` | Is `true` if limit ad tracking is enabled on the device, or `false` otherwise  | `true` |

## API Reference

### `removeAdInfo()`

Removes the stored Ad Identifier string from the data layer.

```kotlin
tealium?.adIdentifier?.removeAdInfo()
```

### `removeAppSetIdInfo()`

Removes the stored App Set data from the data layer.

```kotlin
tealium?.adIdentifier?.removeAppSetIdInfo()
```