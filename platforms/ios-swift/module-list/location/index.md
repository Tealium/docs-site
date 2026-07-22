---
title: Location Module
description: Provides device location data for your events and the ability to add geofences around points of interest.
url: https://docs.tealium.com/platforms/ios-swift/module-list/location/
---
The Location module enables your iOS app to receive location information and the ability to configure and monitor geofences. [Learn more](https://docs.tealium.com/platforms/getting-started-mobile/location/) about location tracking and geofencing.

## Supported Platforms

The following platforms are supported:

* [iOS](https://docs.tealium.com/platforms/ios-swift/)

## Requirements

* [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) (1.9.0+)

## Sample App

Explore the [iOS sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample) to familiarize yourself with our library, tracking methods, and best practice implementation. The main sample app includes the Location module and an example of the geofencing feature.

## Install

Install the Location module with Swift Package Manager, CocoaPods or Carthage. The Location module requires a dispatcher (`TealiumCollect` or `TealiumTagManagement`) to transmit location events.

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `Up to next major` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `Location` module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

Learn more about the [Swift Package Manager installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended).

### CocoaPods

To install the Location module with CocoaPods add the following pod to your Podfile:  

```perl
pod 'tealium-swift/Location'
```

Learn more about the [CocoaPods installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the Location module with Carthage:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumLocation.framework
      ```

Learn more about the [Carthage installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#carthage).

## Initialize

To initialize the module, verify that it's specified on the `TealiumConfig` [`collectors`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#collectors) property

`config.collectors = [Collectors.Location]`

Additional options for [location accuracy](#location-tracking) and [geofencing](#geofencing) are also configurable for your `TealiumConfig` instance.


<blockquote>
Review the [Collectors](https://docs.tealium.com/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.
</blockquote>


### Authorization

To authorize your app to collect location information, add the following keys to your app's `Info.plist` file:

- `Privacy - Location When In Use Usage Description`
- `Privacy - Location Always and When In Use Usage Description`

If the keys are not present, location requests fail immediately.  [Learn more](https://developer.apple.com/documentation/corelocation/requesting_authorization_for_location_services) about requesting authorization for location services.

If you do not already request location authorizaiton within your current implementation, you can use the Location module's API method `requestAuthorization()` in the Tealium completion callback like so:

```swift
func start() {
      //...
      tealium = Tealium(config: config) { _ in
      		self.tealium?.location?.requestAuthorization()
      }
  }
```

### Approximate Location Tracking (iOS 14+)

Apple iOS 14+ provides an app setting for sharing your approximate location rather than your precise location. This method is recommended if your app requires precise location, and if the user initially disabled precise location tracking through their device settings.

If you are not already requesting temporary full authorization in your codebase, use the Tealium helper method `requestTemporaryFullAccuracyAuthorization` shown in the following example which requests temporary full accuracy.

```swift
func start() {
    //...
    tealium = Tealium(config: config) { _ in
      guard let location = self.tealium?.location else {
          return
      }
      if location.isAuthorized {
          location.requestTemporaryFullAccuracyAuthorization(purposeKey: "NearStore")
      } else {
          location.requestAuthorization()
      }
    }
}
```

The `String` parameter `purposeKey` corresponds to the key in the `NSLocationTemporaryUsageDescriptionDictionary` dictionary of your app `Info.plist` file, as shown in the following example:

```html
    <key>NSLocationTemporaryUsageDescriptionDictionary</key>
    <dict>
        <key>NearStore</key>
        <string>To send you discounts when you are near a store</string>
    </dict>
```

Learn more about [requesting temporary full authorization](https://developer.apple.com/documentation/corelocation/cllocationmanager/3600217-requesttemporaryfullaccuracyauth).

## Location Tracking

The Location module performs continuous location tracking once the user has authorized location services. Location updates are based on two settings: accuracy and distance.

If you disable the geofence feature, only significant location updates are monitored by Apple's [`startMonitoringSignificantLocationChanges()`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati) method, which results in fewer updates and less battery consumption. This method is called if either property [`config.geofencesTrackingEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#geofencetrackingenabled) or [`config.useHighAccuracy`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#usehighaccuracy) are set to false, otherwise the Apple's [`startUpdatingLocation`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation) method is called

The geofence feature is enabled by default and location updates are more frequent to provide better accuracy. To enable or disable more frequent location updates, set the [`useHighAccuracy`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#usehighaccuracy) property.

If you would like a more accurate location and distance setting, set the [`updateDistance`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#updatedistance) property to a value in meters at which to trigger updates.

There is also an extended accuracy setting, [`desiredAccuracy`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#desiredaccuracy) that specifies the level of accuracy which the app wants to receive. This is the similar to the [`CLLocationManager desiredAccuracy`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy) property. In iOS 14+, the default value is `.reduced` and in previous versions it is `.nearestHundredMeters`.

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "PROFILE",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      config.useHighAccuracy = false
      config.updateDistance = 150
      config.desiredAccuracy = .nearestThreeKilometers
  }
```

## Geofencing

Geofencing is enabled by default, and to configure geofences, use one of the following methods to provide your [geofence JSON file](https://docs.tealium.com/platforms/getting-started-mobile/location/#json-file):

* **Hosted URL**  
Use your own hosted geofences file, provided as a URL to the property [`geofenceUrl`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#geofenceurl).   
This option is recommended if you have overridden the publish settings URL or want to use [Hosted Data Layer](https://docs.tealium.com/use-case-supplementing-product-data/).    
```swift
config.geofenceUrl = "https://example.com/geofences.json"
```
* **Local File**  
Use a geofences file stored in your app by setting the property [`geofenceFileName`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#geofencefilename). Omit the file extension.
```swift
config.geofenceFileName = "geofences" // geofences.json
```

To disable geofencing set the [`geofenceTrackingEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#geofencetrackingenabled) property:

```swift
config.geofenceTrackingEnabled = false
```

## Additional Considerations

**Number of Active Geofences**  
Geofences are added and removed dynamically, using as few resources as possible. There is no limit to the number of geofences defined, but the number of active geofences is limited to 20 per device user across _all_ running applications.

**Initializing Geofences**  
If a user is within a geofence at the time of creation, the `enter` transition event does not fire. This is because `exit` and `enter` transition events are fired when crossing the perimeter and not when materializing inside.


## Data Layer

The following variables are populated by the Location module as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | The latitude of the user's most recently recorded location | `32.906119` |
| `longitude`    | `String` |The longitude of the user's most recently recorded location | `-117.2367` |
| `location_accuracy` | `String` | The frequency for which the location updates are requested, such as `high` or `low` | `high`|
| `location_accuracy_extended` | `String` | The accuracy setting for the Location module, such as `best` or `reduced` | `reduced`|

During geofencing, a tracking call containing location data is sent when the transition state of the user changes. Transition state changes include a user entering or exiting a geofence. The following additional variables are sent to the data layer:

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | The Tealium tracked geofence event | `geofence_entered` or `geofence_exited` |
| `geofence_name`            | `String` | The name of the geofence region | `Tealium_San_Diego` |
| `geofence_transition_type` | `String` | The type of geofence transition event | `geofence_entered` or `geofence_exited` |
| `movement_speed`           | `String` | The instantaneous speed of the device, measured in meters per second | `1.0` |
| `location_timestamp`       | `String` | The recorded date/time (GMT) the user entered/exited the geofence region | `2020-01-28 16:29:46 +0000`|

## API Reference

For the reference of methods used by the Location module, see the [`LocationModule`](https://docs.tealium.com/platforms/ios-swift/api/location-module/) class in the Tealium SDK for iOS API.
