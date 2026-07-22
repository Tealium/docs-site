---
title: Tag Management Dispatcher Module
description: A client-side implementation of the Universal Tag (`utag.js`) which uses a non-rendered WebView instance to execute JavaScript.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/tag-management/
---
## Usage

The Tag Management Dispatcher module is a client-side implementation of the Universal Tag (`utag.js`) which uses a non-rendered `WebView` instance to execute JavaScript. This Dispatcher is required in apps that make use of Tealium iQ Tag Management.

## Install

Install the Tag Management Dispatcher module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library and Tag Management Dispatcher
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-tagmanagement-dispatcher:1.2.2'
      }
      ```

### Manual

To install the Tag Management Dispatcher manually:

1. Download the Tealium [Tag Management Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/tagmanagementdispatcher) module.

2. Copy the file `tealium-kotlin.tagmanagement-1.2.1.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.tagmanagement-1.2.1', ext:'aar')
      }
      ```

## Configuration Options

Override the URL used in the Tag Management Dispatcher to download and run the Universal Tag (`utag.js`) using the following `TealiumConfig` option:
```kotlin
val config = TealiumConfig(...)

config.overrideTagManagementUrl = "https://yourcustomdomain.com"
```

Enable or disable the `remote_api` events that get sent to the Tag Management webview. This effectively disables remote commands that are triggered by the webview, which are enabled by default.

```kotlin
val config = TealiumConfig(...)

config.remoteApiEnabled = false
```
