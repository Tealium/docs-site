---
title: TealiumConsentManagerDelegate
description: Provides methods for the Tealium consent management delegate.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-consent-manager-delegate/
---
## Class: `TealiumConsentManagerDelegate`

The following summarizes the commonly used methods of the iOS (Swift) `TealiumInstanceManagerDelegate` class.

| Method | Description |
| ----- | ------ |
| `consentStatusChanged()` | Called whenever the consent state has been successfully updated |
| `userChangedConsentCategories()` | Called when the user updates their consent categories preferences |
| `userConsentedToTracking()` | Called when the consent state is changed to `.consented`|
| `userOptedOutOfTracking()` | Called when the user declines/revokes consent |
| `willDropTrackingCall()` | Called when the consent manager is going to drop a tracking call |
| `willQueueTrackingCall()` | Called when the consent manager is in the `&#34;unknown&#34;` state, and tracking calls are being queued locally until the user grants or declines consent |
| `willSendTrackingCall()` | Called when the user has consented to tracking, and a tracking call is about to pass through the consent manager without being blocked |

### `consentStatusChanged()`

Called when the consent state has been successfully updated.

```swift
consentStatusChanged(state)
```

| Parameter   | Type    | Description                    |
|-------------|---------|--------------------------------|
| `state`  | `TealiumConsentStatus`  | Consent state |

### `userChangedConsentCategories()`

Called when the user updates their consent categories preferences.

```swift
userChangedConsentCategories(categories)
    }
```
| Parameter   | Type    | Description                    |
|-------------|---------|--------------------------------|
| `categories`  | `[TealiumConsentCategories]`  | Consent categories |

### `userConsentedToTracking()`

Called when the consent state is changed to `.consented`.

```swift
userConsentedToTracking()
```

### `userOptedOutOfTracking()`

Called when the user declines/revokes consent (consent status: `.notConsented`).

```swift
userOptedOutOfTracking()
```

### `willDropTrackingCall()`

Called when the consent manager is going to drop a tracking call. For example, when the user has declined tracking consent.


```swift
willDropTrackingCall(request)
```
| Parameter   | Type    | Description                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium track request |


### `willQueueTrackingCall()`

Called when the consent manager is in the `&#34;unknown&#34;` state, and tracking calls are being queued locally until the user grants or declines consent.

```swift
willQueueTrackingCall(request)
```
| Parameter   | Type    | Description                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium track request |


### `willSendTrackingCall()`

Called when the user has consented to tracking, and a tracking call is about to pass through the consent manager without being blocked.

```swift
willSendTrackingCall(request)
```
| Parameter   | Type    | Description                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium track request |
