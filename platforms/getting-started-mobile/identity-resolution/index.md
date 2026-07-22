---
title: Identity Resolution
description: Learn about identity resolution.
url: https://docs.tealium.com/platforms/getting-started-mobile/identity-resolution/
---
## Anonymous ID

The Tealium library generates a unique persistent anonymous ID the first time it is launched and stores it in `tealium.visitorId`. This value is included in each tracked event as the attribute `tealium_visitor_id`.




```java
class TealiumHelper {
	lateinit var tealium: Tealium

    fun getVisitorId(): String {
        return tealium.visitorId
    }
}
```




```swift
class TealiumHelper {
	var tealium: Tealium?

    var visitorId: String? {
		tealium?.visitorId
	}
}
```




If you are using Tealium AudienceStream, `visitorId` is the anonymous ID associated with the visitor. Learn more about [anonymous IDs in AudienceStream](https://docs.tealium.com/anonymous-user-visitor-id-attributes/).

## Reset Anonymous ID

If needed, you can reset the current `visitorId` by calling this method: 

```
tealium.resetVisitorId()
```

## User Identifier

When you identify known users, add a user identifier attribute to the persistent data storage.

To add a user identifier, such as a customer ID:  




```java
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString("customer_id", id, Expiry.FOREVER)
}
```




```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: "customer_id", value: id, expiration: .forever)
}
```




## Visitor Switching

If your app supports multiple users, it is important to separate their AudienceStream CDP profiles to avoid sending targeted messages or advertisements to the wrong user. When enabled, Tealium SDK's Visitor Switching feature automatically monitors the app for user changes, and resets the `tealium_visitor_id` whenever a new user is detected.

To enable this feature, a visitor identity key must be passed to the `TealiumConfig` instance. This key tells the SDK which data layer item to monitor to determine if a new visitor has logged in. Once a new visitor is detected, a new visitor ID is assigned and inserted into the data layer, affecting any event generated from the point of the visitor switch.

To reduce the number of visitor IDs assigned to each user (recommended for performance reasons in AudienceStream), if the SDK detects a switch to a user who has previously logged in, their original visitor ID is used. To support this feature, the `tealium_visitor_id` and the value of the custom data layer key are stored locally on the device. 


<blockquote>
IDs are always hashed with the `SHA-256` algorithm. The hashed IDs are only used for comparison purposes. There is no way for personal data to be un-hashed, and the hashed value is never transmitted from the device.
</blockquote>


### Configuration

Visitor Switching is enabled by passing the name of the key that identifies the app user in the data layer to the `TealiumConfig` instance:




```java
config.visitorIdentityKey = "customer_id"
```




```swift
config.visitorIdentityKey = "customer_id"
```




Once the visitor identity key is set, the SDK changes the current `tealium_visitor_id` in the data layer whenever the user's known ID (in this case `customer_id`) changes. If the customer ID already exists, the `tealium_visitor_id` is set to the existing customer ID for this visitor. But if the customer ID does not exist, a new `tealium_visitor_id` is generated.

### Removing Stored Identifiers

In some cases, such as complying with a user's deletion request, it may be necessary to remove all stored identifiers from the user's device. To do this:

```
tealium.clearStoredVisitorIds()
```

If the `visitorIdentityKey` is present in the `TealiumConfig` instance and the `dataLayer` contains the visitor identifier, the visitor ID storage is automatically repopulated with the current identity and the new `tealium_visitor_id`.

After clearing all previously saved identifiers, the `tealium_visitor_id` for the current visitor is reset to a new identifier.


<blockquote>
It is strongly advised that this is only performed when absolutely necessary, because clearing the stored IDs regularly prevents the feature from operating as intended, and could lead to problems with your AudienceStream configuration.
</blockquote>


## Listen for Anonymous ID changes

The Tealium instance offers an observable property that can be subscribed to `onVisitorId`. The subscription is called with the current `tealium_visitor_id` in the following instances:

* At app startup.
* When the `tealium_visitor_id` changes after `resetVisitorId` is called.
* When the SDK automatically detects a change of visitor based on the visitorIdentityKey in the data layer.
