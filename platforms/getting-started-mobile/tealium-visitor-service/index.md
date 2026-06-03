---
title: Visitor Service
description: Use the visitor service module to retrieve AudienceStream visitor profile data in your mobile app.
url: https://docs.tealium.com/platforms/getting-started-mobile/tealium-visitor-service/
---
## Supported platforms

* [Tealium for Android: Visitor Service module](/platforms/android-kotlin/module-list/visitor-service/)
* [Tealium for iOS: Visitor Service module](/platforms/ios-swift/module-list/visitor-service/)

## How it works

The visitor service module provides two ways to access visitor profile data:

* **Event listener**  
Subscribe to visitor profile update events. When a new event is tracked, the module requests an updated visitor profile from Tealium. If the profile has changed since the last request, the update is delivered to all registered listeners (`VisitorUpdatedListener` on Android, `VisitorServiceDelegate` on iOS).
* **Direct request**  
Call `requestVisitorProfile()` at any time to fetch the latest visitor profile on demand.

To save device resources, the module polls for updates up to five times after each event, then pauses until the next event is tracked. The profile is considered updated when the built-in Lifetime Event Count metric increments.

## Visitor profile structure

The visitor profile is an object containing attributes keyed by their **attribute ID** from AudienceStream. Attribute IDs are numeric strings (for example, `&#34;22&#34;` for Lifetime Event Count). Audiences are keyed by audience ID, with the audience name as the value.

For a full list of attribute types and usage examples, see the platform-specific reference:

* [Tealium for Android: VisitorProfile](/platforms/android-kotlin/api/visitor-profile/)
* [Tealium for iOS: Visitor Data Object](/platforms/ios-swift/module-list/visitor-service/#visitor-data-object)

## Examples

**Example: Check if a user is a member of an audience.**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.audiences?.let { audiences -&gt;
                if (audiences.containsValue(&#34;Premium User&#34;)) {
                    // enable premium features
                }
            }
        }
    })
}
```




```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        guard let audiences = visitorProfile.audiences else {
            return
        }
        if audiences.contains(where: { $0.value == &#34;Premium User&#34; }) {
            // enable premium features
        }
    }
}
```




**Example: Access a number attribute from the visitor profile using its attribute ID.**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.numbers?.let { numbers -&gt;
                numbers[&#34;5057&#34;]?.let { sessionCount -&gt;
                    if (sessionCount &gt; 5) {
                        // take action for returning users
                    }
                }
            }
        }
    })
}
```




```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        guard let numbers = visitorProfile.numbers else {
            return
        }
        if let sessionCount = numbers[&#34;5057&#34;] {
            if sessionCount &gt; 5 {
                // take action for returning users
            }
        }
    }
}
```




## Use cases

Use the visitor service module to personalize your app in real time, for example:

* Display content based on the user&#39;s preferred product category
* Surface recommendations based on prior browsing or search behavior
* Show different UI for high-value or loyalty-program members
* Enable or disable features for specific audience segments

## Profile update timing

Visitor profile updates are near real-time in most cases, but not guaranteed to be instantaneous. Two scenarios can affect timing:

* **Polling limit**  
After each event, the module polls for profile updates up to five times, then waits until the next event. If no update is detected within five attempts, the profile refresh is deferred to the next event.
* **Asynchronous profile changes**  
Profile updates triggered outside the mobile device (such as file imports or visitor stitching) may arrive after the module has already completed its polling cycle. In these cases, the profile update is delivered after the next event is tracked.
