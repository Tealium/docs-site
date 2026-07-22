---
title: VisitorService Module
description: Retrieves the updated visitor profile from the visitor service.
url: https://docs.tealium.com/platforms/ios-swift/module-list/visitor-service/
---

## Usage

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the VisitorService module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `"Up to next major"` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `VisitorService`, `Core`, and either `Collect` or `TagManagement` modules from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

### CocoaPods

To install the VisitorService module with CocoaPods, add the following pods to your Podfile:  

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' //or 'tealium-swift/TagManagement'
pod 'tealium-swift/VisitorService'
```

Learn more about the [CocoaPods installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the VisitorService module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  

      ```perl
      TealiumVisitorService.framework
      ```
3. To setup the VisitorService module, add the following required import statements to your project:  

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

Learn more about the [Carthage installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#carthage).

## Initialize

To initialize the module, verify that it's specified on the `TealiumConfig` [`collectors`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#collectors) property

`config.collectors = [Collectors.VisitorService]`

## Visitor Data Object

The visitor profile is an object that contains friendly names for each attribute. There is a `currentVisit` property that lets you distinguish visitor/visit attribute types. Access each attribute value by ID using a subscript. If the attribute does not exist, `nil` is returned. See the below list for examples.

**Attribute Types**

| Parameters         | Properties                                                                                                       | Value                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `arraysOfBooleans` | id: String, value: [Bool]                                                                                        | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: [Double]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: [String]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Bool                                                                                          | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Bool                                                                                          | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit visitorProfile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Int                                                                                           | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Double                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set<String>                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: [String:Double]                                                                               | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Double                                                                                        | `["category 1": 2.0]`                                                                                                             |


<blockquote>
If an Audience or Badge is not assigned, `nil` is returned.
</blockquote>


#### `arraysOfBooleans`

| Usage                                     | Description                                                | Type               | Example                                       |
| ----------------------------------------- | ---------------------------------------------------------- | ------------------ | --------------------------------------------- |
| `visitorProfile.arraysOfBooleans`         | Returns all the arrays of booleans in the visitor profile. | `[String: [Bool]]` | `["2333": [true,false], "1123": [true,true]]` |
| `visitorProfile.arraysOfBooleans["2815"]` | Returns the array of booleans by id.                       | `[Bool]`           | `[true,true]`                                 |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of booleans value
    if let arraysOfBooleans = visitorProfile.arraysOfBooleans?["5279"] {
        let numberOfPositiveBools = arraysOfBooleans.filter { $0 == true }.count
        print(numberOfPositiveBools)
    }
}
```

#### `arraysOfNumbers`  

| Usage                                    | Description                                               | Type                 | Example                                        |
| ---------------------------------------- | --------------------------------------------------------- | -------------------- | ---------------------------------------------- |
| `visitorProfile.arraysOfNumbers`         | Returns all the arrays of numbers in the visitor profile. | `[String: [Double]]` | `["2333": [2.0, 1.0], "1123": [4.82125, 3.0]]` |
| `visitorProfile.arraysOfNumbers["2815"]` | Returns the array of numbers by id.                       | `[Double]`           | `[4.82125, 3.0]`                               |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of numbers value
    if let arraysOfNumbers = visitorProfile.arraysOfNumbers?["5279"] {
        arraysOfNumbers.forEach { number in
    		if number > 3.0 {
    			// ... take action
    		}
        }
    }
}
```

#### `arraysOfStrings`  

| Usage                                    | Description                                               | Type                 | Example                                                                     |
| ---------------------------------------- | --------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------- |
| `visitorProfile.arraysOfStrings`         | Returns all the arrays of strings in the visitor profile. | `[String: [String]]` | `["1033": ["Foundation", "Perfume"], "3390": ["Bootleg Jeans", "Dresses"]]` |
| `visitorProfile.arraysOfStrings["3390"]` | Returns the array of strings by id.                       | `[String]`           | `["Bootleg Jeans", "Dresses"]`                                              |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of strings value
    if let arraysOfStrings = visitorProfile.arraysOfStrings?["3390"] {
        arraysOfStrings.forEach { string in
    		if string.lowercased().contains("Jeans") {
    			// ... take action
    		}
        }
    }
}
```
#### `audiences`

| Usage                             | Description                                                                                                       | Type               | Example                                                                                     |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------- |
| `visitorProfile.audiences`        | Returns all audiences for which the visitor is a member.                                                          | `[String: String]` | `["tealiummobile\_demo\_103": "iOS Users", "tealiummobile\_demo\_110": "Visitors - Known"]` |
| `visitorProfile.audiences["103"]` | Returns true/false depending on whether or not the visitor is a member of the audience based on the id passed in. | `Bool`             | `true`                                                                                      |


<blockquote>
If an Audience is not assigned, `nil` is returned.
</blockquote>


Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return the current Audiences for which the user is assigned
    if let audiences = visitorProfile.audiences {
        print("Visitor audiences: \(audiences)")

        // Check if an Audience is assigned to a user by id
        if audiences["account_profile_106"] != nil {
            print("Visitor is a member of audience id 106")
            // ... Visitor is a member of this audience, take appropriate action
        }

    }
}
```

#### `badges`  

| Usage                           | Description                                                                       | Type             | Example                        |
| ------------------------------- | --------------------------------------------------------------------------------- | ---------------- | ------------------------------ |
| `visitorProfile.badges`         | Returns all badges in the visitor profile.                                        | `[String: Bool]` | `["2815": true, "2813": true]` |
| `visitorProfile.badges["2815"]` | Returns true/false depending on whether or not the visitor is assigned the badge. | `Bool`           | `true`                         |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a badge value
    if let badgeAssigned = visitorProfile.badges?["5279"] {
        print(badgeAssigned ? "Badge id 5279 is assigned" : "Badge id 5945 is not assigned")
    }
}
```


<blockquote>
If a Badge is not assigned, `nil` is returned.
</blockquote>


#### `booleans`

| Usage                             | Description                                      | Type             | Example                         |
| --------------------------------- | ------------------------------------------------ | ---------------- | ------------------------------- |
| `visitorProfile.booleans`         | Returns all the booleans in the visitor profile. | `[String: Bool]` | `["5784": true, "1453": false]` |
| `visitorProfile.booleans["4692"]` | Returns the boolean by id.                       | `Bool`           | `true`                          |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a boolean value
    if let booleanValue = visitorProfile.booleans?["4479"] {
        if booleanValue {
        	// ... do something
        }
    }
}
```

#### `currentVisit`
Access to the attributes for the current visit instead of the lifetime attributes for a visitor.

| Usage                             | Description                                                                                                                                                                                      | Type                         | Example                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.currentVisit`     | Returns the current visit scoped attributes.                                                                                                                                                     | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `visitorProfile.currentVisit.###` | Returns the attribute you want, depending on ###. All the same methods listed above apply except for audiences and badges. These are exclusively visitor attributes and do not apply to the visit. | Varies                       | Varies                                                                                                                            |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a current visit string attribute
    if let currentVisit = visitorProfile.currentVisit,
       let string = currentVisit.strings?["34"] {
        print(string)
        // ... take action
    }
}
```

#### `dates`

| Usage                          | Description                                   | Type            | Example                                      |
| ------------------------------ | --------------------------------------------- | --------------- | -------------------------------------------- |
| `visitorProfile.dates`         | Returns all the dates in the visitor profile. | `[String: Int]` | `["25": 1567120112000, "13": 1567120145666]` |
| `visitorProfile.dates["4692"]` | Returns the date by id.                       | `Int`           | `1567120112000`                              |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a date value
    if let date = visitorProfile.dates?["33"] {
        print(date)
        // .. take action
    }
}
```

#### `numbers`

| Usege                            | Description                                     | Type               | Example                                   |
| -------------------------------- | ----------------------------------------------- | ------------------ | ----------------------------------------- |
| `visitorProfile.numbers`         | Returns all the numbers in the visitor profile. | `[String: Double]` | `["83": 0.5714285714285714, "1399": 2.0]` |
| `visitorProfile.numbers["1399"]` | Returns the number by id.                       | `Double`           | `4.82125`                                 |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a number value
    if let number = visitorProfile.numbers?["1399"] {
        if number > 3.0 {
        	// ... take action
        }
    }
}
```


#### `setsOfStrings`

| Usage                                  | Description                                             | Type                    | Example                                                              |
| -------------------------------------- | ------------------------------------------------------- | ----------------------- | -------------------------------------------------------------------- |
| `visitorProfile.setsOfStrings`         | Returns all the sets of strings in the visitor profile. | `[String: Set<String>]` | `["9938": ["shirts"], "2300": ["Luxury Couch 1", "Luxury Couch 2"]]` |
| `visitorProfile.setsOfStrings["2300"]` | Returns the set of strings by id.                       | `Set<String>`           | `["Luxury Couch 1", "Luxury Couch 2"]`                               |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an set of strings value
    if let setOfStrings = visitorProfile.setsOfStrings?["5279"] {
        if setOfStrings.contains("toys") {
        	// ... take action
        }
    }
}
```


#### `strings`

| Usage                            | Description                                     | Type     | Example                                     |
| -------------------------------- | ----------------------------------------------- | -------- | ------------------------------------------- |
| `visitorProfile.strings`         | Returns all the strings in the visitor profile. | `String` | `"83": "Toy Truck", "5699": "Toy Tea Set"]` |
| `visitorProfile.strings["5699"]` | Returns the string by id.                       | `String` | `"Toy Tea Set"`                             |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a string value
    if let string = visitorProfile.strings?["5699"] {
        print(string)
        // ... take action
    }
}
```

#### `tallies`

| Usage                                      | Description                                     | Type                         | Example                                                                                                        |
| ------------------------------------------ | ----------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.tallies`                   | Returns all the tallies in the visitor profile. | `[String: [String: Double]]` | `["2983": ["red shirts category": 4.0, "green shirts category": 2.0], "5643": ["girls": 3.0, "womens": 1.0]]`] |
| `visitorProfile.tallies["1399"]`           | Returns the tally by id.                        | `[String: Double]`           | `["girls": 3.0, "womens": 1.0]`                                                                                |
| `visitorProfile.tallies["1399"]["womens"]` | Returns the tally by id.                        | `Double`                     | `3.0`                                                                                                          |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an entire tally
    if let tally = visitorProfile.tallies?["1399"] {
        print("Tally id 5377: \(tally)")
    }

    // Return a tally value by using the tally id and the key for the value you want
    if let tally = visitorProfile.tallies?["5381"], let tallyValue = tally["red shirts"] {
        print("Tally value for id 5381 and key 'red shirts': \(tallyValue)")
    }
}
```

## API Reference

### Class `Tealium`

The following summarizes the commonly used methods and properties of the VisitorService module.

| Method/Property | Description |
| ----- | ------ |
| [`cachedProfile`](#cachedprofile) | Returns the most recently-retrieved visitor profile from persistent storage, without triggering a new request|
| [`requestVisitorProfile()`](#requestvisitorprofile) | Triggers an immediate request to the VisitorService to retrieve the current visitor profile |
| [`visitorService`](#visitorservice)  | The VisitorService module property |


#### `cachedProfile`

Returns the most recently-retrieved visitor profile from persistent storage, without triggering a new request. Useful in situations where there is no internet connection, but a prior successful request has been made.

Usage example:

```swift
let profile = self.tealium?.visitorService?.cachedProfile
guard let json = try? JSONEncoder().encode(profile),
    let cachedProfileString = String(data: json, encoding: .utf8) else {
        return
}
print(cachedProfileString)
```

#### `requestVisitorProfile()`

Triggers an immediate request to the VisitorService to retrieve the current visitor profile. If the profile has been updated since the last fetch, the [`didUpdate()`](#didupdate) delegate method is called.

This method is called automatically whenever a track request is sent, if your visitor profile refresh interval is set to `0`. If you have a higher value set for the refresh interval, then you may call this method to retrieve the profile instantly, without waiting for the next scheduled update.

```swift
self.tealium?.visitorService?.requestVisitorProfile()
```

Usage example:

```swift
func track(title: String, data: [String: Any]?) {
   let tealEvent = TealiumEvent(title, dataLayer: data)
   tealium?.track(tealEvent)
   tealium?.visitorService?.requestVisitorProfile()
}
```

#### `visitorService`

The VisitorService module.

```swift
self.tealium?.visitorService?.####
```
The `####` is any public API method on the `visitorService` object. The following is a full usage example:

```swift
class MyHelperClass {
    var tealium: Tealium?

    public init () {
        let config = TealiumConfig(account: "ACCOUNT",
            profile: "PROFILE",
            environment: "ENVIRONMENT",
            datasource: "DATASOURCE",
            optionalData: nil)

        config.visitorServiceDelegate = self
        config.visitorServiceRefresh = .every(10, .minutes)

        self.tealium = Tealium(config) {
            // Note: this is inside the completion block after initialization

            // self.tealium is guaranteed to be initialized inside the completion block
            self.tealium?.visitorService?.####
        }
    }
}
```

### Class: `VisitorServiceDelegate`

The following summarizes the commonly used methods and properties of the VisitorService module.

| Method/Property | Description |
| ----- | ------ |
| [`didUpdate()`](#didupdate)  | Callback method that returns the updated visitor profile when the profile has updated. |

#### `didUpdate()`

Callback method that returns the updated visitor profile when the profile has updated, or when the `requestVisitorProfile()` method is called.  This depends on the set value of the refresh interval, which default to 5 minutes.

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Act on profile attributes
    print(visitorProfile.audiences)
    //...
}
```

| Parameter   | Description | Example                           |
| ------      | ----------- | --------------------------------- |
| `TealiumVisitorProfile` | Tealium visitor profile | `visitorProfile` |


### Class: `TealiumConfig`

The following summarizes the commonly used methods and properties of the VisitorService module.

| Method/Property | Description |
| ----- | ------ |
| [`visitorServiceDelegate`](#visitorservicedelegate) | Set a delegate to use the `didUpdate` delegate method |
| [`visitorServiceOverrideProfile`](#visitorserviceoverrideprofile) | Overrides the profile from which to fetch the visitor profile |
| [`visitorServiceOverrideURL`](#visitorserviceoverrideurl) | Overrides the base URL from which the visitor profile is retrieved |
| [`visitorServiceRefresh`](#visitorservicerefresh) | Sets the frequency of visitor profile retrieval |


#### `visitorServiceDelegate`

Set a delegate to use the [`didUpdate`](#didupdate) delegate method.  

```swift
config.visitorServiceDelegate = self
```

| Type   | Description | Example                           |
| ------ | ----------- | --------------------------------- |
| `Class` | Class responsible for the profile updates (delegate) | `AnalyticsManager`, `TealiumHelper` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium VisitorService module config methods
      config.visitorServiceDelegate = self
  }
```

```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        if let json = try? JSONEncoder().encode(visitorProfile),
           let string = String(data: json, encoding: .utf8) {
            print(string)
        }
    }
}
```

#### `visitorServiceOverrideProfile`

Overrides the profile from which to fetch the visitor profile. Align it with the profile used for data collection in the Collect module.


```swift
config.visitorServiceOverrideProfile = "PROFILE"
```

| Type | Description | Example |
| --- | --- | --- |
| `String` | Sets the Audience Stream profile from which to fetch the visitor profile | `"main"` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideProfile = "main"
  }
```

#### `visitorServiceOverrideURL`

Overrides the base URL from which the visitor profile is retrieved. ACCOUNT, PROFILE, and visitor ID are automatically appended to the URL.


```swift
config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
```

| Type | Description | Example |
| --- | --- | --- |
| `String` | Sets the URL from which to fetch the visitor profile | `"https://overridden-subdomain.yourdomain.com/"` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
  }
```

#### `visitorServiceRefresh`

Use this property to adjust the frequency of visitor profile retrieval. The default value is 5 minutes. Even if you add the `requestVisitorProfile()` method to every tracking call, the profile is not fetched every time unless you set this to 0.

```swift
let config = TealiumConfig(...)
config.visitorServiceRefresh = .every(3, .seconds)
```

`RefreshInterval` options: `seconds`, `minutes`, or `hours`

| Parameters | Description                                                                            | Example |
| ---------- | -------------------------------------------------------------------------------------- | ------- |
|`.every(Int, RefreshInterval)`   | The frequency for which to fetch the visitor profile.  (default: `.every(5, .minutes)`) | `.every(15, .seconds)`     |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceRefresh = .every(3, .seconds)
  }
```

## Release Notes

2.0.0

**High Impact Changes**

 * Updated TealiumVisitorProfile to be more performant
 * Removed multicast delegate capability for simplicity
 * Removed completion from cached profile method

**Low Impact Changes**

* Added more options to refresh interval
* Updated class names for consistency
* Updated delegate method signature
* Improved tests

1.8.0

* Initial release
