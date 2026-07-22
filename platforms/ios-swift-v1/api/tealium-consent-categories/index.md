---
title: TealiumConsentCategories
description: Provides methods for Tealium consent categories.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-consent-categories/
---
## Class: `TealiumConsentCategories`

The following summarizes the commonly used methods of the iOS (Swift) `TealiumConsentCategories` class.

| Method | Description |
| ----- | ------ |
| `all()` | Returns the complete list of supported consent categories |
| `consentCategoriesStringArrayToEnum()` | Returns consented categories as an enum, converted from a string array of consented categories |

### `all()`

Returns the complete list of supported consent categories.

```swift
TealiumConsentCategories.all()
```

| Return Type | Description |
| --- | --- |
| `[TealiumConsentCategories]` | All currently-implemented consent categories |

The following lists all currently-implemented consent categories from `[TealiumConsentCategories]`:

```swift
[.analytics
.affiliates
.displayAds
.email
.personalization
.search
.social
.bigData
.mobile
.engagement
.monitoring
.cdm
.cdp
.cookiematch
.misc]
```

### `consentCategoriesStringArrayToEnum()`

Returns consented categories as an enum, converted from a string array of consented categories. Invalid string values are omitted from the resulting array.

```swift
consentCategoriesStringArrayToEnum(categories)
```

| Parameters | Type |  Description | Example |
| --- | --- | --- | --- |
| `categories` | `[String]` | An array of strings to convert into an array of TealiumConsentCategories | `["analytics", "bigData"]` |
