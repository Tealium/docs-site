---
title: Firebase dispatcher
description: Send Tealium Prism events to Firebase Analytics on iOS and Android with the Firebase dispatcher module.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/firebase-dispatcher/
---
The Firebase dispatcher is a Tealium Prism module that forwards events to the Firebase Analytics SDK on the device. You track an event once with Prism and the dispatcher calls the native Firebase API. You configure mappings from your data layer to Firebase events, parameters, user properties, and consent settings in your Tealium mobile profile.

## Requirements

The Firebase dispatcher requires the following:

| Requirement | iOS | Android |
| :--- | :--- | :--- |
| Operating system | iOS 15+, macOS 10.15+, or tvOS 15+ | Android API 23+ |
| Tealium Prism | 0.7.0+ | 0.7.0+ |
| Firebase SDK | Firebase iOS SDK 12.x (FirebaseAnalytics) | Firebase Android BoM 34.6.0+ (firebase-analytics) |
| Firebase project files | `GoogleService-Info.plist` in the app target | `google-services.json` in the app module and the `com.google.gms.google-services` plugin |
| Kotlin | N/A | 2.0+ |

## Add the module

1. In your Tealium mobile profile, go to **Modules**, and add the **Firebase** module.
1. Set the module settings. Each is optional. If omitted, Firebase applies its own default.
1. Add mappings from your data layer variables to Firebase destinations. See [Data mappings](#data-mappings).
1. Optionally restrict the module with load rules. For more information, see [Rules](https://docs.tealium.com/platforms/prism-mobile/rules/).
1. Save and publish the mobile settings. The SDK fetches the published file at startup and on each remote settings refresh. See [publish mobile settings](https://docs.tealium.com/publish-mobile-settings/).

### Settings

| Setting | Settings key | Type | Description |
| :--- | :--- | :--- | :--- |
| Session timeout | `session_timeout_seconds` | Number | Firebase session timeout in seconds. |
| Analytics collection enabled | `analytics_collection_enabled` | Boolean | Turns Firebase Analytics collection on or off. |
| Log level | `log_level` | String | (iOS only) One of `min`, `error`, `warning`, `notice`, `info`, `debug`, `max`. |

`session_timeout_seconds` and `analytics_collection_enabled` are also available as commands. Module settings apply when the module starts and again whenever the SDK fetches updated settings. The matching command applies at event time.

## Data mappings

A mapping copies a data layer variable to a destination in the Firebase command payload. The following mapping runs `logevent` when `tealium_event` is `purchase`, uses the event name as the Firebase event name, and sends `order_total` as the Firebase `value` parameter:

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

The available mappings are:

### Firebase Config

| Destination | Type  |
|:---------|:-----|
| `session_timeout_seconds` | Integer as String |
| `analytics_collection_enabled` | Boolean as String |


### Standard

| Destination | Type/Values | Description |
|:---------|:-----|:------------|
| `parameters.achievement_id` | `String` | Achievement ID |
| `parameters.aclid` | `String` | Ad Network Click ID |
| `parameters.affiliation` | `String` | Affiliation |
| `parameters.cp1` | `String` | CP1 |
| `parameters.campaign` | `String` | Campaign |
| `parameters.character` | `String` | Character |
| `parameters.content` | `String` | Content |
| `parameters.content_type` | `String` | Content Type |
| `parameters.coupon` | `String` | Coupon |
| `parameters.creative_name` | `String` | Creative Name |
| `parameters.creative_slot` | `String` | Creative Slot |
| `parameters.currency` | `String` | Currency |
| `parameters.destination` | `String` | Destination |
| `parameters.end_date` | `String` | End Date |
| `parameters.flight_number` | `String` | Flight Number |
| `parameters.group_id` | `String` | Group ID |
| `parameters.index` | `Long` | Index |
| `parameters.item_brand` | `String` | Item Brand |
| `parameters.item_category` | `String` | Item Category |
| `parameters.item_id` | `String` | Item ID |
| `parameters.item_name` | `String` | Item Name |
| `parameters.item_variant` | `String` | Item Variant |
| `parameters.level` | `Long` | Level |
| `parameters.location` | `String` | Location |
| `parameters.medium` | `String` | Medium |
| `parameters.number_of_nights` | `Long` | Number Of Nights |
| `parameters.number_of_passengers` | `Long` | Number Of Passengers |
| `parameters.number_of_rooms` | `Long` | Number Of Rooms |
| `parameters.origin` | `String` | Origin |
| `parameters.price` | `Double` | Price |
| `parameters.quantity` | `Long` | Quantity |
| `parameters.screen_name` | `String` | Screen Name |
| `parameters.screen_class` | `String` | Screen Class |
| `parameters.score` | `Long` | Score |
| `parameters.search_term` | `String` | Search Term |
| `parameters.shipping` | `Double` | Shipping |
| `parameters.method` | `String` | Method |
| `parameters.source` | `String` | Source |
| `parameters.travel_class` | `String` | Travel Class |
| `parameters.virtual_currency_name` | `String` | Virtual Currency Name |
| `parameters.start_date` | `String` | Start Date |
| `parameters.term` | `String` | Term |
| `parameters.tax` | `Double` | Tax |
| `parameters.transaction_id` | `String` | Transaction ID |
| `parameters.value` | `Long or Double` | Value |
| `parameters.level_name` | `String` | Level Name |
| `parameters.success` | `Long` | Success |
| `parameters.ad_format` | `String` | Ad Format |
| `parameters.ad_platform` | `String` | Ad Platform |
| `parameters.ad_source` | `String` | Ad Source |
| `parameters.ad_unit_name` | `String` | Ad Unit Name |
| `parameters.campaign_id` | `String` | Campaign ID |
| `parameters.creative_format` | `String` | Creative Format |
| `parameters.discount` | `Double` | Discount |
| `parameters.extend_session` | `String` | Extend Session |
| `parameters.item_category2` | `String` | Item Category2 |
| `parameters.item_category3` | `String` | Item Category3 |
| `parameters.item_category4` | `String` | Item Category4 |
| `parameters.item_category5` | `String` | Item Category5 |
| `parameters.item_list_id` | `String` | Item List ID |
| `parameters.item_list_name` | `String` | Item List Name |
| `parameters.items` | `Array` | Items |
| `parameters.location_id` | `String` | Location ID |
| `parameters.marketing_tactic` | `String` | Marketing Tactic |
| `parameters.payment_type` | `String` | Payment Type |
| `parameters.promotion_id` | `String` | Promotion ID |
| `parameters.promotion_name` | `String` | Promotion Name |
| `parameters.shipping_tier` | `String` | Shipping Tier |
| `parameters.source_platform` | `String` | Source Platform |
| `email_address` | `String` | Email Address |
| `phone_number` | `String` | Phone Number |
| `hashed_email_address` | `String` | Hashed Email Address |
| `hashed_phone_number` | `String` | Hashed Phone Number |


### E-Commerce

| Destination | Type/Values | Description |
|:---------|:-----|:------------|
| `parameters.transaction_id` | `String` | Order ID |
| `parameters.value` | `Long or Double` | Order Total |
| `parameters.shipping` | `Double` | Shipping Amount |
| `parameters.tax` | `Double` | Tax Amount |
| `parameters.currency` | `String` | Currency |
| `parameters.coupon` | `String` | Promo Code |
| `parameters.items.item_id` | `Array` | List of Product IDs |
| `parameters.items.item_name` | `Array` | List of Names |
| `parameters.items.item_brand` | `Array` | List of Brands |
| `parameters.items.item_category` | `Array` | List of Categories |
| `parameters.items.quantity` | `Array` | List of Quantities |
| `parameters.items.price` | `Array` | List of Prices |
| `parameters.items.item_list_name` | `Array` | List of Presentation Lists |
| `parameters.items.item_variant` | `Array` | List of Variants |
| `parameters.items.index` | `Array` | List of Indexes |


### Consent settings

| Destination | Type/Values | Description |
|:---------|:-----|:------------|
| `consent_settings.ad_storage` | `String` | Ad Storage |
| `consent_settings.analytics_storage` | `String` | Analytics Storage |
| `consent_settings.ad_user_data` | `String` | Ad User Data |
| `consent_settings.ad_personalization` | `String` | Ad Personalization |


## Install in code


<blockquote>
If you add the Firebase module in your mobile profile, skip the install and initialize steps. For more information, see [Add the module](#add-the-module).
</blockquote>




Add the Tealium Maven repository to `settings.gradle.kts` if you have not already:

```kotlin
pluginManagement {
    repositories {
        google()
        gradlePluginPortal()
        mavenCentral()
    }
}

dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://maven.tealiumiq.com/android/releases/") }
    }
}
```

Add the dispatcher and Firebase Analytics to your app module's `build.gradle.kts`. Declare `firebase-analytics` yourself to keep the Firebase SDK version under your control:

```kotlin
plugins {
    id("com.google.gms.google-services") version "4.4.2"
}

dependencies {
    implementation("com.tealium.prism:firebase:0.2.0")
    implementation(platform("com.google.firebase:firebase-bom:34.6.0"))
    implementation("com.google.firebase:firebase-analytics")
}
```

`prism-core` is included transitively.



To install with Swift Package Manager:

1. In Xcode, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher`.
1. Select **Up to next major** and add the `TealiumPrismFirebase` product to your app target.

Or add the package to `Package.swift`:

```swift
.package(url: "https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher.git", from: "0.2.0")
```

To install with CocoaPods, add the following line to your Podfile:

```ruby
pod 'TealiumPrismFirebase'
```

The package depends on `TealiumPrismCore` and `FirebaseAnalytics`. Do not add the Firebase SDK separately.



## Initialize in code


<blockquote>
If you add the Firebase module in your mobile profile, skip the install and initialize steps. For more information, see [Add the module](#add-the-module).
</blockquote>


The dispatcher initializes Firebase for you. When the device is offline, the Firebase SDK queues events and delivers them when connectivity is restored.

If your app configures modules in code, add the module to the `modules` list in `TealiumConfig`:



The `firebase-analytics` content provider initializes Firebase at startup.

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig
import com.tealium.prism.core.api.Modules
import com.tealium.prism.core.api.misc.Environment
import com.tealium.prism.firebase.firebase

val config = TealiumConfig.Builder(
    application = this,
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.collect(),
        Modules.firebase()
    )
)
    .setSettingsUrl("https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
    .build()
val tealium = Tealium.create(config)
```



The dispatcher calls `FirebaseApp.configure()` on first use and skips it if your app already did.

```swift
import TealiumPrismCore
import TealiumPrismFirebase

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.collect(),
                            Modules.firebaseDispatcher()
                           ],
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
let tealium = Tealium.create(config: config)
```



To lock a setting so that remote changes cannot override it, pass a builder closure. For more information, see [Advanced configuration](https://docs.tealium.com/about-prism-mobile/#advanced-configuration).



```kotlin
Modules.firebase { builder ->
    builder.setAnalyticsEnabled(true)
}
```


```swift
Modules.firebaseDispatcher { builder in
    builder.setAnalyticsEnabled(true)
}
```



## Events

To trigger Firebase events, use data mappings in the Firebase module in your mobile profile to map the values of `tealium_event` to their matching Firebase event names. For example, in this mapping, when `tealium_event="purchase"` it triggers the Firebase events for `purchase` and `logEvent`:

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

### `initiateconversionmeasurement`

| | |
| :--- | :--- |
| iOS method | `initiateOnDeviceConversionMeasurement()` |
| Android method | N/A |
| Destinations | `hashed_email_address`, `hashed_phone_number`, `email_address`, `phone_number` |
| Notes | iOS only. At least one destination is required. If more than one is mapped, only the first in the order listed is used. |
{class="dt--pivot"}

### `logevent`

| | |
| :--- | :--- |
| iOS method | `logEvent()` |
| Android method | `logEvent()` |
| Destinations | `event_name`, `parameters`, `parameters.<param>`, `parameters.items.<param>` |
| Notes | `event_name` is required. All other destinations are optional. To map items, use parallel arrays (for example `product_id` and `product_price`) or an array of objects with `parameters.items.<param>`. A scalar counts as a single-element array. When you use parallel arrays, every array under `items` must be the same length. If the lengths differ, the command fails with `arrayLengthMismatch`. Null values are dropped from an item, and an item left with no values is dropped entirely. |
{class="dt--pivot"}

### `resetdata`

| | |
| :--- | :--- |
| iOS method | `resetAnalyticsData()` |
| Android method | `resetAnalyticsData()` |
| Destinations | None |
| Notes | Clears analytics data and resets the app instance ID. |
{class="dt--pivot"}

### `setanalyticscollectionenabled`

| | |
| :--- | :--- |
| iOS method | `setAnalyticsCollectionEnabled()` |
| Android method | `setAnalyticsCollectionEnabled()` |
| Destinations | `analytics_collection_enabled` |
| Notes | Previously collected data is retained. |
{class="dt--pivot"}

### `setconsent`

| | |
| :--- | :--- |
| iOS method | `setConsent()` |
| Android method | `setConsent()` |
| Destinations | `consent_settings`, `consent_settings.ad_storage`, `consent_settings.analytics_storage`, `consent_settings.ad_user_data`, `consent_settings.ad_personalization` |
| Notes | Each value must be `granted` or `denied`. Only the types present in the payload are updated. The rest keep their previous status. |
{class="dt--pivot"}

### `setdefaultparameters`

| | |
| :--- | :--- |
| iOS method | `setDefaultEventParameters()` |
| Android method | `setDefaultEventParameters()` |
| Destinations | `parameters`, `parameters.<param>` |
| Notes | Parameters are merged into the existing defaults, replacing any with the same name. Omit `parameters` entirely to clear all defaults. An empty `parameters` object is a no-op and leaves the current defaults in place. |
{class="dt--pivot"}

### `setsessiontimeout`

| | |
| :--- | :--- |
| iOS method | `setSessionTimeoutInterval()` |
| Android method | `setSessionTimeoutDuration()` |
| Destinations | `session_timeout_seconds` |
| Notes | Always mapped in seconds. Android converts to milliseconds internally. |
{class="dt--pivot"}

### `setuserid`

| | |
| :--- | :--- |
| iOS method | `setUserID()` |
| Android method | `setUserId()` |
| Destinations | `user_id` |
| Notes | An empty string clears the user ID. |
{class="dt--pivot"}

### `setuserproperty`

| | |
| :--- | :--- |
| iOS method | `setUserProperty()` |
| Android method | `setUserProperty()` |
| Destinations | `property_name`, `property_value` |
| Notes | Both destinations accept a string or an array of strings. Arrays must be the same length. An empty value removes the property. |
{class="dt--pivot"}

## Verify

Enable Firebase debug mode on your test device, then track an event that maps to `logevent`. The event appears in **DebugView** within seconds with the mapped parameters.

* [View events in Xcode debug console](https://firebase.google.com/docs/analytics/ios/events#view-events-in-xcode-debug-console) (iOS)
* [View events in debug log](https://firebase.google.com/docs/analytics/android/events#view-events-in-debug-log) (Android)

If the event does not appear, use [Trace](https://docs.tealium.com/platforms/prism-mobile/trace/) to confirm the event reached Prism with the expected data layer values.

## Troubleshooting

| Symptom | Cause | Fix |
| :--- | :--- | :--- |
| No events in DebugView | The remote or local settings have no `FirebaseDispatcher` entry. | Add the Firebase module to your mobile profile and publish, or check your local settings file. |
| Event reaches Prism but not Firebase | No mapping sets `command_name` for that `tealium_event`. | Add a `command_name` mapping with a filter on the event name. |
| Settings do not apply | The module ID differs between local, remote, and programmatic settings. | Use the same key under `modules` in every source. |
| Firebase logs are silent on Android | `log_level` is iOS only. | Run `adb shell setprop log.tag.FA VERBOSE`. |
| Consent command fails with `invalidParameterType` | A consent type or status is not one of the accepted values. | Map only `ad_storage`, `analytics_storage`, `ad_user_data`, `ad_personalization` to `granted` or `denied` (case-insensitive). Any other value fails the whole command. |

### Command errors

When a command fails, the dispatcher logs a warning, skips that command, and continues. Other commands you mapped on the same event still run, and the event still reaches your other dispatchers. Search the device log for `Command '<name>' failed:`. The message wording differs slightly between iOS and Android. The error types are the same on both.

| Error | Cause | Fix |
| :--- | :--- | :--- |
| `missingParameter` | A destination the command requires has no mapping. | Map it. Required: `event_name` for `logevent`, `user_id` for `setuserid`, `property_name` and `property_value` for `setuserproperty`, `consent_settings` for `setconsent`, `session_timeout_seconds` for `setsessiontimeout`, `analytics_collection_enabled` for `setanalyticscollectionenabled`. |
| `invalidParameterType` | A mapped value has the wrong type, names an unknown consent type or status, or is a `hashed_*` value that is not valid Base64. | Check the type against the commands table. For consent, map only the four supported types to `granted` or `denied`. |
| `arrayLengthMismatch` | Parallel arrays have different lengths, either under `parameters.items` or `property_name` against `property_value`. | Make the arrays the same length, or switch `items` to the array-of-objects format. |
| `commandNotFound` | The value in `map_to` is not a supported command name. | Check it against the commands table. Matching is case-insensitive and ignores surrounding whitespace, but the name must contain no separators, for example `setuserid` or `SetUserID`, not `set_user_id`. |

The less common errors `emptyParameter`, `emptyArray`, and `noValidParameters` occur when a mapped value is empty or when no supported destination is mapped for the command.

## Limitations

* `initiateconversionmeasurement` and `log_level` are iOS only.
* Only one Firebase dispatcher can be active in an app.

## Reference

* [Prism iOS Firebase API reference](https://docs.tealium.com/tealium-prism-ios-firebase-dispatcher/)
* [Prism Android Firebase API reference](https://docs.tealium.com/tealium-prism-android-firebase-dispatcher/)
