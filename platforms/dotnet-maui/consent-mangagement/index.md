---
title: Consent management
description: Learn how to implement consent management for .NET MAUI.
url: https://docs.tealium.com/platforms/dotnet-maui/consent-mangagement/
---
## Usage

Consent management is a recommended feature and is automatically included in the library. To manage consent, you must set a consent policy, and then track the user&#39;s consent status and consent preferences. 

To learn more, see [consent management](/platforms/getting-started-mobile/consent-management/).

## Sample App

Use the .NET MAUI consent management sample app to familiarize yourself with our library, the tracking methods, and best practices:

[Download .NET MAUI consent management sample app](https://github.com/Tealium/tealium-dotnet-maui/tree/master/Samples/ExampleAppConsentMgr)

## Enable

The consent management feature comes from the native SDKs embedded into the DLLs named `Tealium.Platform.*.dlls`. 

To enable consent management, set the `consentPolicy` parameter when you initialize [`TealiumConfig`](/platforms/dotnet-maui/api/#consentpolicy):

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

## Consent Status

As with the native SDKs for both Android and iOS, when consent management is enabled, new users are assumed to be in an unknown state. Tracking requests are queued up until the consent status has been opted-in or out, at which point events are sent or purged, respectively.

Use the following methods to manage a user&#39;s consent:

* [`SetConsentStatus()`](/platforms/dotnet-maui/api/#setconsentstatus)
* [`GetConsentStatus()`](/platforms/dotnet-maui/api/#getconsentstatus)
* [`SetConsentCategories()`](/platforms/dotnet-maui/api/#setconsentcategories)
* [`GetConsentCategories()`](/platforms/dotnet-maui/api/#getconsentcategories)
* [`SetConsentExpiryListener()`](/platforms/dotnet-maui/api/#setconsentexpirylistener)

The `Tealium.Common.dll` provides the following category and status enums to use:

* [`Tealium.ConsentManager.ConsentStatus`](/platforms/dotnet-maui/api/#consentstatus)
* [`Tealium.ConsentManager.ConsentCategory`](/platforms/dotnet-maui/api/#consentcategory)
