---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/ios-objective-c/track/
---
## Track Views

Track screen views with the [`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) method. This is done in the [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) method of any View Controller. This method accepts two parameters: the name of the screen and (optionally) contextual view data. 


<blockquote>
The screen name value is set in the event attribute `screen_title`.
</blockquote>




```swift
// Retrieve instance
let tealium = Tealium.instance(forKey: "INSTANCE")

// Basic
tealium?.trackViewWithTitle("SCREEN_NAME", dataSources: nil)

// With optional data
let optionalData = ["KEY1": "VALUE1"]
tealium?.trackView(withTitle: "SCREEN_NAME", dataSources: optionalData)

// With optional array data
let optionalData = ["KEY1": ["STRING1", "STRING2"]]
tealium?.trackView(withTitle: "SCREEN_NAME", dataSources: optionalData)
```



```obj-c
// Retrieve instance
Tealium *tealium = [Tealium instanceForKey:@"INSTANCE"];

// Basic
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources:nil];

// With optional data
NSDictionary *optionalData = @{@"KEY1" : @"VALUE1"};
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources: optionalData];

// With optional array data
NSDictionary *optionalData = @{@"KEY1" : @[@"STRING1", "STRING2"]};
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources: optionalData];
```



| Parameter | Type | Description | Swift Example | iOS Example |
| --- | --- | --- | --- | --- |
| `title` | `String` |Title of view |  `"screenName"` | `"screenName"` |
| `customDataSources` | `[String]` |(Optional) Custom datasources (key-value pairs) to be included in the event dispatch | `@{@"someKey": @"someValue"}` | `["someKey": "someValue"]` |

## Track Events

Track non-view activity with the [`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) method. This method accepts two parameters: an event name and (optionally) contextual event data.


<blockquote>
The event name value is populated in the event attribute named `tealium_event`.
</blockquote>




```swift
// Retrieve instance
let tealium = Tealium.instance(forKey: "INSTANCE")

// Basic
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: nil)

// With optional data
let optionalData = ["KEY1": "VALUE1"]
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: optionalData)

// With optional array data
let optionalData = ["KEY1": ["STRING1", "STRING2"]]
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: optionalData)
```



```obj-c
// Retrieve instance
Tealium *tealium = [Tealium instanceForKey:@"INSTANCE"];

// Basic
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:nil];

// With optional data
NSDictionary *optionalData = @{@"KEY1" : @"VALUE1"};
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:optionalData];

// With optional array data
NSDictionary *optionalData = @{@"KEY1" : @[@"STRING1", @"STRING2"]};
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:optionalData];
```



| Parameter | Type |Description | Swift Example | iOS Example |
| --- | --- | --- | --- | --- |
| `title` | `String` | Title of event |`"someEvent"` | `"someEvent"` |
| `customDataSources` | `[String]` | (Optional) Custom datasources (key-value pairs) to be included in the event dispatch | `@{@"someKey": @"someValue"}` | `["someKey": "someValue"]` |
