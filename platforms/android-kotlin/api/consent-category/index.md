---
title: ConsentCategory
description: Reference guide for ConsentCategory class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/consent-category/
---
## Class: `ConsentCategory`

The following summarizes the commonly used methods of the `ConsentCategory` class for Kotlin.

| Method | Description |
| ----- | ------ |
| [`ALL`](#all) | Returns the complete list of supported consent categories |
| [`consentCategory(String)`](#consentcategory-string) | Returns the ConsentCategory relating to the given String; else null |
| [`consentCategories(Set<String>)`](#consentcategories-set-string) | Returns the Set of `ConsentCategory` objects relating to the given Strings; invalid entries are ignored. |


### `ALL`

Returns the full set of all available `ConsentCategory` items.

```java
ConsentCategory.ALL
```

The following is the entire set of available categories:

```java
setOf(
    AFFILIATES,
    ANALYTICS,
    BIG_DATA,
    CDP,
    COOKIEMATCH,
    CRM,
    DISPLAY_ADS,
    EMAIL,
    ENGAGEMENT,
    MOBILE,
    MONITORING,
    PERSONALIZATION,
    SEARCH,
    SOCIAL,
    MISC
)
```

### `consentCategory(String)`

Returns the relevant `ConsentCategory` for the given String. The parameter is case-insensitive.

```java
ConsentCategory.consentCategory("cdp") // returns ConsentCategory.CDP
```

### `consentCategories(Set<String>)`

Returns the set of relevant `ConsentCategory` object for the given Strings. The parameters are case-insensitive.

```java
ConsentCategory.consentCategories(setOf("cdp", "invalid", "email"))
// returns setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)
```
