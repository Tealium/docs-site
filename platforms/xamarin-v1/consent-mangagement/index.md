---
title: Consent management
description: Learn how to implement consent management.
url: https://docs.tealium.com/platforms/xamarin-v1/consent-mangagement/
---
<blockquote>
For the current version, see [Tealium for Xamarin 2.x](https://docs.tealium.com/platforms/xamarin/).
</blockquote>


## Usage

Usage of this module is recommended, as it is automatically included in the library and enabled in the native code upon initialization. Android and iOS are both supported platforms.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) about consent management.

## Sample App

To help to familiarize yourself with our library, the tracking methods, and best practice implementation, download the Xamarin consent management [sample app](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleAppConsentMgr).

## Enable

The consent management feature comes from the two native SDKs embedded into the DLLs named `Tealium.Platform.*.dlls`. The `Tealium.Common.dll` provides the following category and status enums to use:

*   `Tealium.ConsentManager.ConsentStatus`
*   `Tealium.ConsentManager.ConsentCategory`

To enable consent management, simply pass the optional parameter in the constructor of `TealiumConfig`, or set it as a property as shown in the following example:

```csharp
TealiumConfig tealConfig = new TealiumConfig(
        TealiumConsts.INSTANCE_ID,
        TealiumConsts.ACCOUNT,
        TealiumConsts.PROFILE,
        TealiumConsts.ENVIRONMENT,
        true,
        commands,
        advConfig,
        false); // optional Consent Manager Enablement

// or subsequently enable it:
tealConfig.IsConsentManagerEnabled = true;

// initialise your Tealium Instance:
var tealium = instanceManager.CreateInstance(tealConfig);
```

## Consent Status

As with the native SDKs for both Android and iOS, when consent management is enabled, new users are assumed to be in an unknown state. Tracking requests are queued up until the consent status has been opted-in or out, at which point events are sent or purged, respectively.

Override the initial status through properties on the `TealiumConfig` object, as shown in the following example:

```csharp
// enable Consent Manager:
tealConfig.IsConsentManagerEnabled = true;

// Set Users to be Consented by default:
tealConfig.InitialUserConsentStatus = ConsentManager.ConsentStatus.Consented;
// Or set Users to be Not Consented by default:
tealConfig.InitialUserConsentStatus = ConsentManager.ConsentStatus.NotConsented;

// Opt users into All Categories
tealConfig.InitialUserConsentCategories = ConsentManager.AllCategories;
// or none:
tealConfig.InitialUserConsentCategories = ConsentManager.NoCategories;
// or partial opt-in, only to Analytics and Mobile categories.
tealConfig.InitialUserConsentCategories = new ConsentCategory[]{
    ConsentManager.ConsentCategory.Analytics,
        ConsentManager.ConsentCategory.Mobile
};
```

## Consent Selection

Interact directly with consent management from the Tealium instance, through the `ConsentManager` property.

If you need to update a user's consent selection, pass one of enum values available in the `ConsentManager.ConsentCategory` and `ConsentManager.ConsentStatus`, as shown in the following example:

```csharp
// if the user is in an Unknown state, then the following code triggers any queued events are sent after this:
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
tealium.ConsentManager.UserConsentStatus = ConsentManager.ConsentStatus.Consented;

// The previous inherently opts the user into all categories as none have been provide.
// To grant consent and opt into a subset of categories, use the overload:
tealium.ConsentManager.UserConsentStatusWithCategories(ConsentManager.ConsentStatus.Consented, new ConsentCategory[]{
    ConsentManager.ConsentCategory.Analytics
});
```

## Resetting

Additional options are available to reset the currently selected consent preferences. This reverts the user back to an `Unknown` status so that subsequent events begin being queued again.

To completely disable, disable it on the `TealiumConfig` object, as shown in the following example:

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
tealium.ConsentManager.ResetUserConsentPreferences();
```
