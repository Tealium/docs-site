---
title: AppData Module
description: Adds information about the app bundle to the data layer.
url: https://docs.tealium.com/platforms/ios-swift/module-list/appdata/
---
## Usage
The AppData module gathers important information about the app bundle. Usage of this module is recommended, but not mandatory. If you choose to exclude it, the data layer variables are not included in tracking calls. The `tealium_visitor_id` is always transmitted, even if the module is disabled, as this is a required variable.

The following platforms are supported:

* iOS
* macOS
* watchOS
* tvOS

## Install

This module is included as part of the Core library and does not require separate installation.

## Initialize

To initialize the module, verify that it&#39;s specified on the `TealiumConfig` [`collectors`](/platforms/ios-swift/api/tealium-config/#collectors) property:

```swift
config.collectors = [Collectors.AppData]
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable             | Description                                                                                                                                                | Example                                  |
|:---------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------|
| `app_build`          | Minor build version of the app                                                                                                                             | `&#34;2213&#34;`                                 |
| `app_name`           | Name of the app (usually same as App Store name)                                                                                                           | `&#34;Digital Velocity&#34;`                     |
| `app_rdns`           | Fully-qualified name of the app bundle                                                                                                                     | `&#34;com.tealium.digitalvelocity&#34;`          |
| `app_uuid`           | Random uuid. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled. | `123e4567-e89b-12d3-a456-&#34;426655440000&#34;` |
| `app_version`        | Version of the app bundle                                                                                                                                  | `&#34;1.0&#34;`                                  |
| `tealium_visitor_id` | Persistent Tealium visitor ID                                                                                                                              | `&#34;123e4567e89b12d3a456426655440000&#34;`     |
