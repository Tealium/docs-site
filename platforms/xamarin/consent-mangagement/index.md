---
title: Consent management
description: Learn how to implement consent management for Xamarin.
url: https://docs.tealium.com/platforms/xamarin/consent-mangagement/
---
## Usage

Consent management is a recommended feature and is automatically included in the library. To manage consent you must set a consent policy, then track the user's consent status and consent preferences. 

[Learn more about consent management](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/).

## Sample App

Use the Xamarin consent management sample app to familiarize yourself with our library, the tracking methods, and best practices:

[Download Xamarin consent management sample app](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleAppConsentMgr)

## Enable

The consent management feature comes from the native SDKs embedded into the DLLs named `Tealium.Platform.*.dlls`. 

To enable consent management, set the `consentPolicy` parameter when you initialize [`TealiumConfig`](https://docs.tealium.com/platforms/xamarin/api/#consentpolicy):

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

## Consent Status

As with the native SDKs for both Android and iOS, when consent management is enabled, new users are assumed to be in an unknown state. Tracking requests are queued up until the consent status has been opted-in or out, at which point events are sent or purged, respectively.

Use the following methods to manage a user's consent:

* [`SetConsentStatus()`](https://docs.tealium.com/platforms/xamarin/api/#setconsentstatus)
* [`GetConsentStatus()`](https://docs.tealium.com/platforms/xamarin/api/#getconsentstatus)
* [`SetConsentCategories()`](https://docs.tealium.com/platforms/xamarin/api/#setconsentcategories)
* [`GetConsentCategories()`](https://docs.tealium.com/platforms/xamarin/api/#getconsentcategories)
* [`SetConsentExpiryListener()`](https://docs.tealium.com/platforms/xamarin/api/#setconsentexpirylistener)

The `Tealium.Common.dll` provides the following category and status enums to use:

* [`Tealium.ConsentManager.ConsentStatus`](https://docs.tealium.com/platforms/xamarin/api/#consentstatus)
* [`Tealium.ConsentManager.ConsentCategory`](https://docs.tealium.com/platforms/xamarin/api/#consentcategory)
