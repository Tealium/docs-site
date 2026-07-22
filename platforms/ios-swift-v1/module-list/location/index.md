---
title: Location Module
description: Provides device location data for your events and the ability to add geofences around points of interest.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/location/
---
The Location module enables your iOS app to receive location information and the ability to configure and monitor geofences. [Learn more](https://docs.tealium.com/platforms/getting-started-mobile/location/) about location tracking and geofencing.

## Supported Platforms

The following platforms are supported:

* [iOS](https://docs.tealium.com/platforms/ios-swift-v1/)

## Requirements

* [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift-v1/) (1.9.0+)

## Sample App

Explore the [iOS sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample) to familiarize yourself with our library, tracking methods, and best practice implementation. The main sample app includes the Location module.

## Install

Install the Location module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

To install the Location module with SPM:

1. Add a Swift Package within Xcode or the command line tool using the repository: https://www.github.com/Tealium/tealium-swift

2. If using Xcode, select the `TealiumLocation` target in the installation process. If using the command line, add the `TealiumLocation` module in the list of dependencies within the `Package.swift` file.

The framework is auto-instantiated. It has a dependency on `TealiumCore` and requires a dispatcher (`TealiumCollect` or `TealiumTagManagement`). No additional import statements are necessary.

[Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#swift-package-manager-recommended) about the SPM installation for iOS.

### CocoaPods

To install the Location module with CocoaPods add the following pod to your Podfile:  

```ruby
pod 'tealium-swift/TealiumLocation'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod and requires a dispatcher (`TealiumCollect` or `TealiumTagManagement`). [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about the CocoaPods installation for iOS.

### Carthage

To install the Location module with Carthage:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumLocation.framework
    ```
The framework is auto-instantiated. It has a dependency on `TealiumCore` and requires a dispatcher (`TealiumCollect` or `TealiumTagManagement`). No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about the Carthage installation for iOS.

## Initialize

Location tracking is enabled by default when the module is added to your app. Configuration options for [location accuracy](#location-tracking) and [geofencing](#geofencing) are set using properties of an instance of `TealiumConfig`.

### Permissions

To authorize your app to collect location information, add the following keys to your app's `Info.plist` file:

- `Privacy - Location When In Use Usage Description`
- `Privacy - Location Always and When In Use Usage Description`

If the keys are not present, location requests fail immediately.  [Learn more](https://developer.apple.com/documentation/corelocation/requesting_authorization_for_location_services) about requesting authorization for location services.

## Location Tracking

The Location module performs continuous location tracking. Location updates are based on two settings: accuracy and distance.

By default, only significant location updates are monitored. This results in fewer updates and less battery consumption.

To enable higher accuracy updates, set the [`useHighAccuracy`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#usehighaccuracy) property to `true` and set the [`updateDistance`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#updatedistance) property to a value in meters at which to trigger updates.

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "PROFILE",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      config.useHighAccuracy = true
      config.updateDistance = 150
      //...
  }
```

## Geofencing

To enable geofencing, use one of the following methods to provide your [geofence JSON file](https://docs.tealium.com/platforms/getting-started-mobile/location/#json-file):

* **Hosted URL**  
Use your own hosted geofences file, provided as a URL to the property [`geofenceUrl`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#geofenceurl).   
This option is recommended if you have overridden the publish settings URL or want to use [Hosted Data Layer](https://docs.tealium.com/use-case-supplementing-product-data/).    
```swift
config.geofenceUrl = "https://example.com/geofences.json"
```
* **Local File**  
Use a geofences file stored in your app by setting the property [`geofenceFileName`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#geofencefilename). Omit the file extension.
```swift
config.geofenceFileName = "geofences" // geofences.json
```

## Additional Considerations

**Number of Active Geofences**  
Geofences are added and removed dynamically, using as few resources as possible. There is no limit to the number of geofences defined, but the number of active geofences is limited to 20 per device user across _all_ running applications.

**Initializing Geofences**  
If a user is within a geofence at the time of creation, the `"enter"` transition event does not fire. This is because `"exit"` and `"enter"` transition events are fired when crossing the perimeter and not when materializing inside.

## Data Layer

The following variables are populated by the Location module as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | The latitude of the user's most recently recorded location | `"32.906119"` |
| `longitude`    | `String` |The longitude of the user's most recently recorded location | `"-117.2367"` |
| `location_accuracy` | `String` | The accuracy setting for the Location module, such as `"high"` or `"low"` | `"high"`|

During geofencing, a tracking call containing location data is sent when the transition state of the user changes. Transition state changes include a user entering or exiting a geofence. The following additional variables are sent to the data layer:

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | The Tealium tracked geofence event | `"geofence_entered"` or `"geofence_exited"` |
| `geofence_name`            | `String` | The name of the geofence region | `"Tealium_San_Diego"` |
| `geofence_transition_type` | `String` | The type of geofence transition event | `"geofence_entered"` or `"geofence_exited"` |
| `movement_speed`           | `String` | The instantaneous speed of the device, measured in meters per second | `"1.0"` |
| `location_timestamp`       | `String` | The recorded date/time (GMT) the user entered/exited the geofence region | `"2020-01-28 16:29:46 +0000"`|

## API Reference

For the reference of methods used in the Location module, see the [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/) class in the Tealium SDK for iOS API.
