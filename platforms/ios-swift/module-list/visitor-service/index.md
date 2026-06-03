---
title: VisitorService Module
description: Retrieves the updated visitor profile from the visitor service.
url: https://docs.tealium.com/platforms/ios-swift/module-list/visitor-service/
---

## Usage

The VisitorService module implements the [Data Layer Enrichment]() feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the VisitorService module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0&#43;, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `VisitorService`, `Core`, and either `Collect` or `TagManagement` modules from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

### CocoaPods

To install the VisitorService module with CocoaPods, add the following pods to your Podfile:  

```perl
pod &#39;tealium-swift/Core&#39;
pod &#39;tealium-swift/Collect&#39; //or &#39;tealium-swift/TagManagement&#39;
pod &#39;tealium-swift/VisitorService&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the VisitorService module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

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

Learn more about the [Carthage installation for iOS](/platforms/ios-swift/install/#carthage).

## Initialize

To initialize the module, verify that it&#39;s specified on the `TealiumConfig` [`collectors`](/platforms/ios-swift/api/tealium-config/#collectors) property

`config.collectors = [Collectors.VisitorService]`

## Visitor Data Object

The visitor profile is an object that contains friendly names for each attribute. There is a `currentVisit` property that lets you distinguish visitor/visit attribute types. Access each attribute value by ID using a subscript. If the attribute does not exist, `nil` is returned. See the below list for examples.

**Attribute Types**

| Parameters         | Properties                                                                                                       | Value                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `arraysOfBooleans` | id: String, value: [Bool]                                                                                        | `id: &#34;5129&#34;, value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: [Double]                                                                                      | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: [String]                                                                                      | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: &#34;tealiummobile\_demo\_103&#34;, value: &#34;iOS Users&#34;`                                                                              |
| `badges`           | id: String, value: Bool                                                                                          | `id: &#34;2815&#34;, value: true`                                                                                                         |
| `booleans`         | id: String, value: Bool                                                                                          | `id: &#34;4868&#34;, value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit visitorProfile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `dates`            | id: String, value: Int                                                                                           | `id: &#34;22&#34;, value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Double                                                                                        | `id: &#34;5728&#34;, value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set&lt;String&gt;                                                                                   | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                                                                               |
| `tallies`          | id: String, value: [String:Double]                                                                               | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Double                                                                                        | `[&#34;category 1&#34;: 2.0]`                                                                                                             |

If an Audience or Badge is not assigned, `nil` is returned.

#### `arraysOfBooleans`

| Usage                                     | Description                                                | Type               | Example                                       |
| ----------------------------------------- | ---------------------------------------------------------- | ------------------ | --------------------------------------------- |
| `visitorProfile.arraysOfBooleans`         | Returns all the arrays of booleans in the visitor profile. | `[String: [Bool]]` | `[&#34;2333&#34;: [true,false], &#34;1123&#34;: [true,true]]` |
| `visitorProfile.arraysOfBooleans[&#34;2815&#34;]` | Returns the array of booleans by id.                       | `[Bool]`           | `[true,true]`                                 |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of booleans value
    if let arraysOfBooleans = visitorProfile.arraysOfBooleans?[&#34;5279&#34;] {
        let numberOfPositiveBools = arraysOfBooleans.filter { $0 == true }.count
        print(numberOfPositiveBools)
    }
}
```

#### `arraysOfNumbers`  

| Usage                                    | Description                                               | Type                 | Example                                        |
| ---------------------------------------- | --------------------------------------------------------- | -------------------- | ---------------------------------------------- |
| `visitorProfile.arraysOfNumbers`         | Returns all the arrays of numbers in the visitor profile. | `[String: [Double]]` | `[&#34;2333&#34;: [2.0, 1.0], &#34;1123&#34;: [4.82125, 3.0]]` |
| `visitorProfile.arraysOfNumbers[&#34;2815&#34;]` | Returns the array of numbers by id.                       | `[Double]`           | `[4.82125, 3.0]`                               |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of numbers value
    if let arraysOfNumbers = visitorProfile.arraysOfNumbers?[&#34;5279&#34;] {
        arraysOfNumbers.forEach { number in
    		if number &gt; 3.0 {
    			// ... take action
    		}
        }
    }
}
```

#### `arraysOfStrings`  

| Usage                                    | Description                                               | Type                 | Example                                                                     |
| ---------------------------------------- | --------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------- |
| `visitorProfile.arraysOfStrings`         | Returns all the arrays of strings in the visitor profile. | `[String: [String]]` | `[&#34;1033&#34;: [&#34;Foundation&#34;, &#34;Perfume&#34;], &#34;3390&#34;: [&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;]]` |
| `visitorProfile.arraysOfStrings[&#34;3390&#34;]` | Returns the array of strings by id.                       | `[String]`           | `[&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;]`                                              |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of strings value
    if let arraysOfStrings = visitorProfile.arraysOfStrings?[&#34;3390&#34;] {
        arraysOfStrings.forEach { string in
    		if string.lowercased().contains(&#34;Jeans&#34;) {
    			// ... take action
    		}
        }
    }
}
```
#### `audiences`

| Usage                             | Description                                                                                                       | Type               | Example                                                                                     |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------- |
| `visitorProfile.audiences`        | Returns all audiences for which the visitor is a member.                                                          | `[String: String]` | `[&#34;tealiummobile\_demo\_103&#34;: &#34;iOS Users&#34;, &#34;tealiummobile\_demo\_110&#34;: &#34;Visitors - Known&#34;]` |
| `visitorProfile.audiences[&#34;103&#34;]` | Returns true/false depending on whether or not the visitor is a member of the audience based on the id passed in. | `Bool`             | `true`                                                                                      |

If an Audience is not assigned, `nil` is returned.

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return the current Audiences for which the user is assigned
    if let audiences = visitorProfile.audiences {
        print(&#34;Visitor audiences: \(audiences)&#34;)

        // Check if an Audience is assigned to a user by id
        if audiences[&#34;account_profile_106&#34;] != nil {
            print(&#34;Visitor is a member of audience id 106&#34;)
            // ... Visitor is a member of this audience, take appropriate action
        }

    }
}
```

#### `badges`  

| Usage                           | Description                                                                       | Type             | Example                        |
| ------------------------------- | --------------------------------------------------------------------------------- | ---------------- | ------------------------------ |
| `visitorProfile.badges`         | Returns all badges in the visitor profile.                                        | `[String: Bool]` | `[&#34;2815&#34;: true, &#34;2813&#34;: true]` |
| `visitorProfile.badges[&#34;2815&#34;]` | Returns true/false depending on whether or not the visitor is assigned the badge. | `Bool`           | `true`                         |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a badge value
    if let badgeAssigned = visitorProfile.badges?[&#34;5279&#34;] {
        print(badgeAssigned ? &#34;Badge id 5279 is assigned&#34; : &#34;Badge id 5945 is not assigned&#34;)
    }
}
```

If a Badge is not assigned, `nil` is returned.

#### `booleans`

| Usage                             | Description                                      | Type             | Example                         |
| --------------------------------- | ------------------------------------------------ | ---------------- | ------------------------------- |
| `visitorProfile.booleans`         | Returns all the booleans in the visitor profile. | `[String: Bool]` | `[&#34;5784&#34;: true, &#34;1453&#34;: false]` |
| `visitorProfile.booleans[&#34;4692&#34;]` | Returns the boolean by id.                       | `Bool`           | `true`                          |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a boolean value
    if let booleanValue = visitorProfile.booleans?[&#34;4479&#34;] {
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
| `visitorProfile.currentVisit`     | Returns the current visit scoped attributes.                                                                                                                                                     | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `visitorProfile.currentVisit.###` | Returns the attribute you want, depending on ###. All the same methods listed above apply except for audiences and badges. These are exclusively visitor attributes and do not apply to the visit. | Varies                       | Varies                                                                                                                            |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a current visit string attribute
    if let currentVisit = visitorProfile.currentVisit,
       let string = currentVisit.strings?[&#34;34&#34;] {
        print(string)
        // ... take action
    }
}
```

#### `dates`

| Usage                          | Description                                   | Type            | Example                                      |
| ------------------------------ | --------------------------------------------- | --------------- | -------------------------------------------- |
| `visitorProfile.dates`         | Returns all the dates in the visitor profile. | `[String: Int]` | `[&#34;25&#34;: 1567120112000, &#34;13&#34;: 1567120145666]` |
| `visitorProfile.dates[&#34;4692&#34;]` | Returns the date by id.                       | `Int`           | `1567120112000`                              |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a date value
    if let date = visitorProfile.dates?[&#34;33&#34;] {
        print(date)
        // .. take action
    }
}
```

#### `numbers`

| Usege                            | Description                                     | Type               | Example                                   |
| -------------------------------- | ----------------------------------------------- | ------------------ | ----------------------------------------- |
| `visitorProfile.numbers`         | Returns all the numbers in the visitor profile. | `[String: Double]` | `[&#34;83&#34;: 0.5714285714285714, &#34;1399&#34;: 2.0]` |
| `visitorProfile.numbers[&#34;1399&#34;]` | Returns the number by id.                       | `Double`           | `4.82125`                                 |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a number value
    if let number = visitorProfile.numbers?[&#34;1399&#34;] {
        if number &gt; 3.0 {
        	// ... take action
        }
    }
}
```


#### `setsOfStrings`

| Usage                                  | Description                                             | Type                    | Example                                                              |
| -------------------------------------- | ------------------------------------------------------- | ----------------------- | -------------------------------------------------------------------- |
| `visitorProfile.setsOfStrings`         | Returns all the sets of strings in the visitor profile. | `[String: Set&lt;String&gt;]` | `[&#34;9938&#34;: [&#34;shirts&#34;], &#34;2300&#34;: [&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;]]` |
| `visitorProfile.setsOfStrings[&#34;2300&#34;]` | Returns the set of strings by id.                       | `Set&lt;String&gt;`           | `[&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;]`                               |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an set of strings value
    if let setOfStrings = visitorProfile.setsOfStrings?[&#34;5279&#34;] {
        if setOfStrings.contains(&#34;toys&#34;) {
        	// ... take action
        }
    }
}
```


#### `strings`

| Usage                            | Description                                     | Type     | Example                                     |
| -------------------------------- | ----------------------------------------------- | -------- | ------------------------------------------- |
| `visitorProfile.strings`         | Returns all the strings in the visitor profile. | `String` | `&#34;83&#34;: &#34;Toy Truck&#34;, &#34;5699&#34;: &#34;Toy Tea Set&#34;]` |
| `visitorProfile.strings[&#34;5699&#34;]` | Returns the string by id.                       | `String` | `&#34;Toy Tea Set&#34;`                             |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a string value
    if let string = visitorProfile.strings?[&#34;5699&#34;] {
        print(string)
        // ... take action
    }
}
```

#### `tallies`

| Usage                                      | Description                                     | Type                         | Example                                                                                                        |
| ------------------------------------------ | ----------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.tallies`                   | Returns all the tallies in the visitor profile. | `[String: [String: Double]]` | `[&#34;2983&#34;: [&#34;red shirts category&#34;: 4.0, &#34;green shirts category&#34;: 2.0], &#34;5643&#34;: [&#34;girls&#34;: 3.0, &#34;womens&#34;: 1.0]]`] |
| `visitorProfile.tallies[&#34;1399&#34;]`           | Returns the tally by id.                        | `[String: Double]`           | `[&#34;girls&#34;: 3.0, &#34;womens&#34;: 1.0]`                                                                                |
| `visitorProfile.tallies[&#34;1399&#34;][&#34;womens&#34;]` | Returns the tally by id.                        | `Double`                     | `3.0`                                                                                                          |

Example usage:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an entire tally
    if let tally = visitorProfile.tallies?[&#34;1399&#34;] {
        print(&#34;Tally id 5377: \(tally)&#34;)
    }

    // Return a tally value by using the tally id and the key for the value you want
    if let tally = visitorProfile.tallies?[&#34;5381&#34;], let tallyValue = tally[&#34;red shirts&#34;] {
        print(&#34;Tally value for id 5381 and key &#39;red shirts&#39;: \(tallyValue)&#34;)
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
        let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
            profile: &#34;PROFILE&#34;,
            environment: &#34;ENVIRONMENT&#34;,
            datasource: &#34;DATASOURCE&#34;,
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
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
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
config.visitorServiceOverrideProfile = &#34;PROFILE&#34;
```

| Type | Description | Example |
| --- | --- | --- |
| `String` | Sets the Audience Stream profile from which to fetch the visitor profile | `&#34;main&#34;` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideProfile = &#34;main&#34;
  }
```

#### `visitorServiceOverrideURL`

Overrides the base URL from which the visitor profile is retrieved. ACCOUNT, PROFILE, and visitor ID are automatically appended to the URL.


```swift
config.visitorServiceOverrideURL = &#34;https://overridden-subdomain.yourdomain.com/&#34;
```

| Type | Description | Example |
| --- | --- | --- |
| `String` | Sets the URL from which to fetch the visitor profile | `&#34;https://overridden-subdomain.yourdomain.com/&#34;` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideURL = &#34;https://overridden-subdomain.yourdomain.com/&#34;
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
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
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
