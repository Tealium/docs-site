---
title: VisitorService Module
description: Retrieves the updated visitor profile from the visitor service.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/visitor-service/
---

## Usage

The VisitorService module implements the [Data Layer Enrichment]() feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and would like to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the VisitorService module with CocoaPods or Carthage.

### CocoaPods

To install the VisitorService module with CocoaPods, add the following pods to your Podfile:  

```ruby
pod &#39;tealium-swift/TealiumCore&#39;
pod &#39;tealium-swift/TealiumCollect&#39; //or &#39;tealium-swift/TealiumTagManagement&#39;
pod &#39;tealium-swift/TealiumVisitorService&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod, and one of the dispatch service pods (either `TealiumCollect` or `TealiumTagManagement`). [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the VisitorService module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  

      ```ruby
      TealiumVisitorService.framework
      ```
3. To setup the VisitorService module, add the following required import statements to your project:  

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`, and at least one dispatch service (`TealiumCore` or `TealiumTagManagement`). No additional import statements are necessary.

[Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Visitor Data Object

The visitor profile is an object that contains native structs for each attribute type. Within the visitor profile object, there is a `currentVisit` property that lets you distinguish visitor/visit attribute types. With the exception of audiences, each attribute value is accessible by ID using a subscript. The `audiences` attribute simply returns `true`/`false` if a visitor is a member of the audience queried through a subscript. See the below list for examples.

**Attribute Types**

| Parameters | Properties |  Value |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: [Bool] | `id: &#34;5129&#34;, value: [true,false,true,true]` |
| `arraysOfNumbers` | id: String, value: [Double] | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings` | id: String, value: [String] | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `audiences` | id: String, name: String | `id: &#34;tealiummobile\_demo\_103&#34;, name: &#34;iOS Users&#34;` |
| `badges` | id: String, value: Bool | `id: &#34;2815&#34;, value: true` |
| `booleans` | id: String, value: Bool | `id: &#34;4868&#34;, value: true `|
| `currentVisit` | All attributes for current visit profile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: [DateTime(id: &#34;5376&#34;, value: 1567536668080), DateTime(id: &#34;10&#34;, value: 1567536668000)], booleans: [Boolean(id: &#34;4530&#34;, value: true], numbers: [Number(id: &#34;32&#34;, value: 3.8)])` |
| `dates` | id: String, value: Int | `id: &#34;22&#34;, value: 1567120112000` |
| `numbers` | id: String, value: Double | `id: &#34;5728&#34;, value: 4.82125` |
| `setOfStrings` | id: String, value: Set[String] | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]` |
| `strings` | id: String, value: String | `id: &#34;5380&#34;, value: &#34;green shirts&#34;` |
| `tallies` | id: String, value: [TallyValue] |  `id: &#34;57&#34;, [[key: &#34;category 1&#34; count: 2.0], key: &#34;category 2&#34;, count: 1.0]]` |
| `tallyValue` | key: String, count: Double | `[key: &#34;category 1&#34; count: 2.0]` |

#### `arraysOfBooleans`
Custom subscripting allows for querying the array of booleans value by id.  

| Usage | Description |  Type | Example |
| --- | --- | --- | --- |
| `profile.arraysOfBooleans` | Returns all the arrays of booleans in the visitor profile. | `[BooleanArray]` | `[BooleanArray(id: &#34;2333&#34;, value: [true,false]), BooleanArray(id: &#34;1123&#34;, value: [true,true])]` |
| `profile.arraysOfBooleans[&#34;2815&#34;]` | Returns the array of booleans by id. | `[Bool]` | `true` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of booleans value
        if let arraysOfBooleans = profile.arraysOfBooleans?[&#34;5279&#34;] {
            let numberOfPositiveBools = arraysOfBooleans.map { $0 == true }.count
            print(numberOfPositiveBools)
        }
}
```

#### `arraysOfNumbers`
Custom subscripting allows for querying the array of numbers value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.arraysOfNumbers` | Returns all the arrays of numbers in the visitor profile. | `[NumberArray]` | `[NumberArray(id: &#34;2333&#34;, value: [2.0, 1.0]), NumberArray(id: &#34;1123&#34;, value: [4.82125, 3.0])]`|
| `profile.arraysOfNumbers[&#34;2815&#34;]` | Returns the array of numbers by id. | `[Double]` | `[4.82125, 3.0]` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of numbers value
        if let arraysOfNumbers = profile. arraysOfNumbers?[&#34;5279&#34;] {
            arraysOfNumbers.forEach { number in
        		if number &gt; 3.0 {
        			// ... take action
        		}
            }
        }
}
```

#### `arraysOfStrings`
Custom subscripting allows for querying the array of strings value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.arraysOfStrings` | Returns all the arrays of strings in the visitor profile. | `[StringArray]` | `[StringArray(id: &#34;1033&#34;, value: [&#34;Foundation&#34;, &#34;Perfume&#34;), StringArray(id: &#34;3390&#34;, value: [&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;])]` |
| `profile.arraysOfStrings[&#34;3390&#34;]` | Returns the array of strings by id. | `[String]` | `[&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;]` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of strings value
        if let arraysOfStrings = profile.arraysOfStrings?[&#34;3390&#34;] {
            arraysOfStrings.forEach { string in
        		if string.lowercased().contains(&#34;Jeans&#34;) {
        			// ... take action
        		}
            }
        }
}
```
#### `audiences`
Custom subscripting allows for checking visitor audience membership by audience id and audience name.

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.audiences` | Returns all audiences for which the visitor is a member. | `[Audience]` | `[Audience(id: &#34;tealiummobile\_demo\_103&#34;, name: &#34;iOS Users&#34;), Audience(id: &#34;tealiummobile\_demo\_110&#34;, name: &#34;Visitors - Known&#34;)]` |
| `profile.audiences[id: &#34;103&#34;]` | Returns true/false depending on whether or not the visitor is a member of the audience based on the id passed in. | `Bool` | `true`|
| `profile.audiences[name: &#34;ios users&#34;]` | Returns true/false depending on whether or not the visitor is a member of the audience based on the name passed in. The name is case insensitive. | `Bool` | `false` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return the current Audiences for which the user is assigned
        if let currentVisitorAudiences = profile.audiences {
            print(&#34;Visitor audiences: \(currentVisitorAudiences)&#34;)

            // Check if an Audience is assigned to a user by id
            if currentVisitorAudiences[id: &#34;106&#34;] {
                print(&#34;Visitor is a member of audience id 106&#34;)
                // ... Visitor is a member of this audience, take appropriate action
            }

            // Check if an Audience is assigned to a user by name
            if currentVisitorAudiences[name: &#34;ios users&#34;] {
                print(&#34;Visitor is a member of audience iOS Users&#34;)
                // ... Visitor is a member of this audience, take appropriate action
            }
        }
}
```

#### `badges`
Custom subscripting allows for querying the badge value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.badges` | Returns all badges in the visitor profile. | `[Badge]` | `[Badge(id: &#34;2815&#34;, value: true), Badge(id: &#34;2813&#34;, value: false)]`|
| `profile.badges[&#34;2815&#34;]` | Returns true/false depending on whether or not the visitor is assigned the badge. | `Bool` | `true` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a badge value
        if let badgeAssigned = profile.badges?[&#34;5279&#34;] {
            print(badgeAssigned ? &#34;Badge id 5279 is assigned&#34; : &#34;Badge id 5945 is not assigned&#34;)
        }
}
```

#### `booleans`
Custom subscripting allows for querying the boolean value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.booleans` | Returns all the booleans in the visitor profile. | `[Boolean]` | `[Boolean(id: &#34;5784&#34;, value: true), Boolean(id: &#34;1453&#34;, value: false)]` |
| `profile.booleans[&#34;4692&#34;]` | Returns the boolean by id. | `Bool` | `true` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a boolean value
        if let booleanValue = profile. booleans?[&#34;4479&#34;] {
            if booleanValue {
            	// ... do something
            }
        }
}
```

#### `currentVisit`
Access to the attributes for the current visit instead of the lifetime attributes for a visitor.

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile. currentVisit` | Returns the current visit scoped attributes. | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile (dates: [DateTime(id: &#34;5376&#34;, value: 1567536668080), DateTime(id: &#34;10&#34;, value: 1567536668000)], booleans: [Boolean(id: &#34;4530&#34;, value: true], numbers: [Number(id: &#34;32&#34;, value: 3.8)])` |
| `profile. currentVisit. ###` | Returns the attribute you want, depending on ###. All the same methods listed above apply except for Audiences and Badges. These are exclusively visitor attributes and do not apply to the visit. | Varies | Varies |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a current visit string attribute
        if let currentVisit = profile.currentVisit,
           let string = currentVisit.strings?[&#34;34&#34;] {
            print(string)
            // ... take action
        }
}
```

#### `dates`
Custom subscripting allows for querying the date value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.dates` | Returns all the dates in the visitor profile. | `[DateTime]` | `[DateTime(id: &#34;22&#34;, value: 1567120112000), DateTime(id: &#34;13&#34;, value: 1567120113245)]`|
| `profile.dates[&#34;4692&#34;]` | Returns the date by id. | `Int` | `1567120112000` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a date value
        if let date = profile.dates?[&#34;33&#34;] {
            print(date)
            // .. take action
        }
}
```

#### `numbers`
Custom subscripting allows for querying the number value by id.  

| Usege | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.numbers` | Returns all the numbers in the visitor profile. | `[Number]` | `[Number(id: &#34;83&#34;, value: 0.5714285714285714), Number(id: &#34;1399&#34;, value: 2.0)]` |
| `profile.numbers[&#34;1399&#34;]` | Returns the number by id. | `Double` | `4.82125` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a number value
        if let number = profile. numbers?[&#34;1399&#34;] {
            if number &gt; 3.0 {
            	// ... take action
            }
        }
}
```


#### `setsOfStrings`

Custom subscripting allows for querying the set of strings value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.setsOfStrings` | Returns all the sets of strings in the visitor profile. | `[SetOfStrings]` | `[SetOfStrings(id: &#34;9938&#34;, value: [&#34;shirts&#34;]), SetOfStrings(id: &#34;2300&#34;, value: [&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;])]` |
| `profile.setsOfStrings[&#34;2300&#34;]` | Returns the set of strings by id. | `Set&lt;String&gt;`| `[&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;]` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an set of strings value
        if let setOfStrings = profile.setsOfStrings?[&#34;5279&#34;] {
            if setOfStrings.contains(&#34;toys&#34;) {
            	// ... take action
            }
        }
}
```


#### `strings`
Custom subscripting allows for querying the string value by id.  

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.strings` | Returns all the strings in the visitor profile. | `[VisitorString]` | `[Number(id: &#34;83&#34;, value: &#34;Toy Truck&#34;), Number(id: &#34;5699&#34;, value: &#34;Toy Tea Set&#34;)]`|
| `profile.strings[&#34;5699&#34;]` | Returns the string by id. | `String` | `&#34;Toy Tea Set&#34;` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a string value
        if let string = profile.strings?[&#34;5699&#34;] {
            print(string)
            // ... take action
        }
}
```

#### `tallies` and `tallyValue`
Custom subscripting allows for querying the tally by id, and to query the tally value by id.

| Usage | Description |  Type | Example  |
| --- | --- | --- | --- |
| `profile.tallies` | Returns all the tallies in the visitor profile. | `[Tally]` | `[Tally(id: &#34;2983&#34;, value: [TallyValue(key: &#34;red shirts category&#34;, count: 4.0), TallyValue(key: &#34;green shirts category&#34;, count: 2.0)]), Tally(id: &#34;5643&#34;, value: [TallyValue(key: &#34;girls&#34;, count: 3.0), TallyValue(key: &#34;womens&#34;, count: 1.0)]`]
| `profile.tallies[tally: &#34;1399&#34;]` | Returns the tally by id. | `[TallyValue]` | `[TallyValue(key: &#34;girls&#34;, count: 3.0), TallyValue(key: &#34;womens&#34;, count: 1.0)]` |
| `profile.tallies[tally: &#34;1399&#34;, key: &#34;womens&#34;]` | Returns the tally by id. | `Double` | `3.0` |

Example usage:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an entire tally
        if let tally = profile.tallies?[&#34;1399&#34;] {
            print(&#34;Tally id 5377: \(tally)&#34;)
        }

        // Return a tally value by using the tally ID and the key for the value  you want
        if let tallyValue = profile.tallies?[tally: &#34;5381&#34;, key: &#34;red shirts&#34;]{
            print(&#34;Tally value for id 5381 and key &#39;red shirts&#39;: \(tallyValue)&#34;)
        }
}
```

## API Reference

### Class `Tealium`

The following API methods are available to act upon the updated visitor profile.

#### `visitorService()`


Usage Example:

```swift
class MyHelperClass {
    var tealium: Tealium?

    public init () {
        let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                   profile: &#34;PROFILE&#34;,
                                   environment: &#34;ENVIRONMENT&#34;,
                                   datasource: &#34;DATASOURCE&#34;,
                                   optionalData: nil)
        config.addVisitorServiceDelegate(self)                           
	     config.setVisitorServiceRefresh(interval: 10)		
		self.tealium = Tealium(config) {
			// Note: this is inside the completion block after initialization

			// self.tealium is guaranteed to be initialized inside the completion block

			self.tealium?.visitorService()?.#### // where #### is any public API method on the visitorProfile object - see other methods for examples
		}
	}
}
```

#### `requestVisitorProfile()`

This method triggers an immediate request to the VisitorService to retrieve the current profile. If the profile has been updated since the last fetch, the `profileDidUpdate` delegate method will be called.

This method is called automatically whenever a track request is sent, if your visitor profile refresh interval is set to `0`. If you have a higher value set for the refresh interval, then you may call this method to retrieve the profile instantly, without waiting for the next scheduled update.

```swift
self.tealium?.visitorService()?.requestVisitorProfile()
```

Usage Example:

```swift
func track(title: String, data: [String: Any]?) {
        tealium?.track(title: title, data: data, completion: { success, \_, error in
            if error != nil {
                print(&#34;*** Track not completed because of error: \n\(String(describing: error))&#34;)
            }
            if success {
                print(&#34;*** Track with VisitorService completed ***&#34;)
                self.tealium?.visitorProfile()?.requestVisitorProfile()

            }
        })
    }
```

#### `getCachedProfile()`

Returns the most recently retrieved visitor profile from persistent storage, without triggering a new request. Useful in situations where there is no internet connection, but a prior successful request has been made.

Example:

```swift
self.tealium?.visitorService()?.getCachedProfile(completion: { profile in
                guard let profile = profile else { return }
                if let json = try? JSONEncoder().encode(profile), let string = String(data: 					json, encoding: .utf8) {
                    print(string)
   		}
})
```

| Parameters | Description | Example Value |
| --- | --- | --- |
| completion: TealiumVisitorProfile? | |  |

#### `removeAllVisitorServiceDelegates()`

Removes all visitor profile delegates.

```swift
self.tealium?.visitorService()?.removeAllVisitorServiceDelegates()
```

#### `addVisitorServiceDelegate()`

Adds a new class conforming to `VisitorServiceDelegate`


```swift
self.tealium?.visitorService()?.addVisitorServiceDelegate(self)
```

| Parameters | Description | Example  |
| --- | --- | --- |
| delegate: Class conforming to `VisitorServiceDelegate` | | `ViewController, TealiumHelper` |

#### `removeSingleDelegate()`

Removes a specific visitor profile delegate.

Example:

```swift
self.tealium?.visitorService()?.removeSingleDelegate(self)
```
| Parameters | Description | Example Value |
| --- | --- | --- |
| delegate: Class conforming to `VisitorServiceDelegate` | | `ViewController, TealiumHelper` |


### Class: `TealiumVisitorServiceDelegate`

#### `profileDidUpdate()`

This method is called whenever the visitor profile was updated. This will most likely be called every time the `requestVisitorProfile()` method is used.


```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // act on profile attributes
        print(profile.audiences)

        ...
}
```

### Class: `TealiumConfig`

#### `setVisitorServiceRefresh()`

This lets you set the frequency of visitor profile retrieval. The default value is 5 minutes for this setting. Use this method to adjust the frequency. Even if you add the `requestVisitorProfile` method to every tracking call, the profile will not be fetched every time unless you set this to 0.

```swift
let config = TealiumConfig(...)
config.setVisitorServiceRefresh(3)
```

| Parameters | Description | Example  |
| --- | --- | --- |
| interval | The frequency for which to fetch the visitor profile. Integer, minutes. (default: `5`)| `3`  |

#### `addVisitorServiceDelegate()`

```swift
config.addVisitorServiceDelegate(self)
```
Add a delegate to an array of VisitorService delegates to use the `profileDidUpdate` delegate method. There can be multiple objects assigned as delegates.

| Parameters | Description | Example  |
| --- | --- | --- |
| class responsible for the profile updates (delegate) | | `ViewController, TealiumHelper` |

#### `getVisitorServiceDelegates()`

Returns a list of delegates assigned to the VisitorService module.


```swift
config.getVisitorServiceDelegates()
```

#### `setVisitorServiceOverrideProfile()`

Overrides the profile from which to fetch the visitor profile. Should align with the profile used for data collection in the Collect module.


```swift
config. setVisitorServiceOverrideProfile(&#34;PROFILE&#34;)
```

#### `setVisitorServiceOverrideURL()`

```swift
config. setVisitorServiceOverrideURL(&#34;https://overridden-subdomain.yourdomain.com/&#34;)
```
Overrides the base URL from which the visitor profile will be retrieved. ACCOUNT, PROFILE, and visitor ID will be automatically appended to the URL.


## Release Notes

1.8.0

* Initial release
