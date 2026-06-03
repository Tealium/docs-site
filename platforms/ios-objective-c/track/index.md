---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/ios-objective-c/track/
---
## Track Views

Track screen views with the [`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) method. This is done in the [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) method of any View Controller. This method accepts two parameters: the name of the screen and (optionally) contextual view data. 

The screen name value is set in the event attribute `screen_title`.



```swift
// Retrieve instance
let tealium = Tealium.instance(forKey: &#34;INSTANCE&#34;)

// Basic
tealium?.trackViewWithTitle(&#34;SCREEN_NAME&#34;, dataSources: nil)

// With optional data
let optionalData = [&#34;KEY1&#34;: &#34;VALUE1&#34;]
tealium?.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: optionalData)

// With optional array data
let optionalData = [&#34;KEY1&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;]]
tealium?.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: optionalData)
```



```obj-c
// Retrieve instance
Tealium *tealium = [Tealium instanceForKey:@&#34;INSTANCE&#34;];

// Basic
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources:nil];

// With optional data
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @&#34;VALUE1&#34;};
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources: optionalData];

// With optional array data
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @[@&#34;STRING1&#34;, &#34;STRING2&#34;]};
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources: optionalData];
```



| Parameter | Type | Description | Swift Example | iOS Example |
| --- | --- | --- | --- | --- |
| `title` | `String` |Title of view |  `&#34;screenName&#34;` | `&#34;screenName&#34;` |
| `customDataSources` | `[String]` |(Optional) Custom datasources (key-value pairs) to be included in the event dispatch | `@{@&#34;someKey&#34;: @&#34;someValue&#34;}` | `[&#34;someKey&#34;: &#34;someValue&#34;]` |

## Track Events

Track non-view activity with the [`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) method. This method accepts two parameters: an event name and (optionally) contextual event data.

The event name value is populated in the event attribute named `tealium_event`.



```swift
// Retrieve instance
let tealium = Tealium.instance(forKey: &#34;INSTANCE&#34;)

// Basic
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: nil)

// With optional data
let optionalData = [&#34;KEY1&#34;: &#34;VALUE1&#34;]
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: optionalData)

// With optional array data
let optionalData = [&#34;KEY1&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;]]
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: optionalData)
```



```obj-c
// Retrieve instance
Tealium *tealium = [Tealium instanceForKey:@&#34;INSTANCE&#34;];

// Basic
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:nil];

// With optional data
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @&#34;VALUE1&#34;};
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:optionalData];

// With optional array data
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @[@&#34;STRING1&#34;, @&#34;STRING2&#34;]};
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:optionalData];
```



| Parameter | Type |Description | Swift Example | iOS Example |
| --- | --- | --- | --- | --- |
| `title` | `String` | Title of event |`&#34;someEvent&#34;` | `&#34;someEvent&#34;` |
| `customDataSources` | `[String]` | (Optional) Custom datasources (key-value pairs) to be included in the event dispatch | `@{@&#34;someKey&#34;: @&#34;someValue&#34;}` | `[&#34;someKey&#34;: &#34;someValue&#34;]` |
