---
title: Modules
description: A list of the available modules.
url: https://docs.tealium.com/platforms/ios-swift-v1/modules/
---This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](/platforms/ios-swift/).

The Tealium Swift library is designed around a modular architecture. Modules are automatically instantiated if they are present, and retrieve their configuration from the `TealiumConfig` instance.

All modules have a dependency on `TealiumCore`. This means installing any of the optional modules installs `TealiumCore`.

## Module List

The modules are listed below in priority order (the internal order in which auto-instantiation takes place).

| Module Name | Module ID |Description | Supported Platforms |
| --- | --- | --- | --- |
| [AppData](/platforms/ios-swift-v1/module-list/appdata/)|`appdata` | Adds `app_uuid` to track data | iOS, macOS, tvOS, watchOS |
| [Attribution](/platforms/ios-swift-v1/module-list/attribution/)|`attribution` | Adds IDFA to track data | iOS |
| [AutoTracking](/platforms/ios-swift-v1/module-list/autotracking/)|`autotracking` | Prepares &amp; sends dispatches for most UI, including `viewDidAppear` events | iOS, tvOS |
| [Collect](/platforms/ios-swift-v1/module-list/collect/)|`collect` | Packages and delivers track call to Tealium Collect or other custom URL endpoint | iOS, macOS, tvOS, watchOS |
| [ConsentManager](/platforms/ios-swift/consent-management)|`consentmanager` | Aids GDPR/privacy compliance | iOS, macOS, tvOS, watchOS |
| [Connectivity](/platforms/ios-swift-v1/module-list/connectivity/)|connectivity | Adds ability to flag track messages for delayed delivery due to connectivity loss | iOS, macOS, tvOS, watchOS |
| [CrashReporter](/platforms/ios-swift-v1/module-list/crash-reporter/)|`crashreporter` | Automatically tracks crashes in your app. Once the module is enabled and the accompanying frameworks are installed, a crash event is triggered if a crash occurs in your app. | iOS |
| [DataSource](/platforms/ios-swift-v1/module-list/datasource/) | `datasource` | Adds an additional config init option for datasource IDs. Included in Core with Swift 1.8.0&#43;. | iOS, macOS, tvOS, watchOS |
| [DefaultStorage](/platforms/ios-swift-v1/module-list/defaults-storage/) | `defaultstorage` | Adds general persistence capability for any module (backed by UserDefaults). Included in Core with Swift 1.8.0&#43;. | iOS, tvOS, watchOS, macOS |
| [Delegate](/platforms/ios-swift-v1/module-list/delegate/)|`delegate` | Adds multicast delegates to monitor or suppress track dispatches | iOS, macOS, tvOS, watchOS |
| [DeviceData](/platforms/ios-swift-v1/module-list/device-data/)|`devicedata` | Add as additional device info to all track data | iOS, macOS, tvOS, watchOS |
| [DispatchQueue](/platforms/ios-swift-v1/module-list/dispatch-queue/)|`dispatchqueue` | Adds persistent storage for queued dispatches and manages Event Batching, if enabled | iOS, macOS, tvOS, watchOS |
| [FileStorage](/platforms/ios-swift-v1/module-list/file-storage/)|`filestorage` | Adds general persistence capability for any module - replaces the Defaults Storage module (backed by `NSKeyedArchiver`). Included in Core with Swift 1.8.0&#43;. | iOS, macOS, watchOS, tvOS |
| [Lifecycle](/platforms/ios-swift-v1/module-list/lifecycle/)|`lifecycle` | Tracks launches, wakes, sleeps, and crash instances (Auto or manually) | iOS, tvOS, watchOS |
| [Location](/platforms/ios-swift-v1/module-list/location/)| `location` | Provides device location data for your events, and the ability to add geofences around points of interest | iOS, Mac Catalyst, macOS, tvOS, watchOS |
| [Logger](/platforms/ios-swift-v1/module-list/logger/)|`logger` | Debug logging | iOS, macOS, tvOS, watchOs |
| [PersistentData](/platforms/ios-swift-v1/module-list/persistent-data/)|`persistentdata` | Adds ability to add persistent data to all track data | iOS, macOS, tvOS, watchOS |
| [RemoteCommands](/platforms/ios-swift-v1/module-list/remote-commands/)|`remotecommands` | Permits configurable remote code block execution through `URLScheme`, `UIWebView`, or `TagManagement` | iOS |
| [TagManagement](/platforms/ios-swift-v1/module-list/tag-management/)|`tagmanagement` | `UIWebview` based dispatch service that permits library to run TIQ/`utag.js` | iOS |
| [Visitor Service](/platforms/ios-swift-v1/module-list/visitor-service/)|`visitorservice` | Retrieves the updated visitor profile from the visitor service | iOS, macOS, tvOS, watchOS |
| [Volatile Data](/platforms/ios-swift-v1/module-list/volatile-data/)|`volatiledata` | Adds ability to add session persistent data to all track data (clears upon app termination/close) | iOS, macOS, tvOS, watchOS |

## Recommended Modules

The following sections lists the recommended modules.

### Base Implementation
This is the recommended list of modules for a base implementation.

* Core              
* Attribution       
* AppData           
* Connectivity        
* Delegate          
* DeviceData        
* DispatchQueue        
* Lifecycle         
* Logger            
* PersistentData    
* VolatileData

### Tag Management
In addition to the base modules, these modules are needed for a tag management installation.

* Consent Manager
* RemoteCommands
* TagManagement

### Tealium EventStream/AudienceStream
In addition to the base modules, these modules are needed for an EventStream/ AudienceStream installation.

* Collect
* Consent Manager

## Install Modules

Install the modules with CocoaPods or Carthage.

### CocoaPods

See [Install with CocoaPods](/platforms/ios-swift/install/#cocoapods) for instructions on including/excluding specific modules.

### Carthage

When you install with Carthage, you must explicitly import the modules you require. You may import all modules if you prefer, and use the module list, as described earlier, but your app is lighter if you only import the modules you need. See [Install with Carthage](/platforms/ios-swift/install/#carthage) for instructions on including/excluding specific modules.


## Disable Modules

Prior to version 1.6.5 of the Tealium Swift SDK, the only way to disable unneeded modules if you were using CocoaPods or Carthage through the [TealiumConfig](/platforms/ios-swift/api/tealium-config/) object, by setting an array of enabled/disabled modules (whitelist/blacklist). In this scenario, all the code was still compiled into your final app bundle, but any disabled modules were deactivated.

This method is still supported, but we recommend migrating to one of the other methods below to take advantage of the performance gains associated with compiling less code into your app bundle. Safely leave the module list enabled on the `TealiumConfig` object, and simultaneously remove unneeded modules. In the case where you attempt to enable a module, but the code is not present in your app bundle, it does not cause any unwanted consequences, and simply has no effect.

The following example blacklists the auto-tracking module:

```swift
let modulesList = TealiumModulesList(isWhitelist: false, moduleNames: [&#34;autotracking&#34;])
config.setModulesList(modulesList)
```
