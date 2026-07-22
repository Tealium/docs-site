---
title: Consent management
description: Learn how to implement consent management for Flutter.
url: https://docs.tealium.com/platforms/flutter-v2/consent-management/
---
<blockquote>
This is the previous version (2.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Usage

Usage of this module is recommended. [Learn more](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) about consent management.

* [Consent manager for Android](https://docs.tealium.com/platforms/android-kotlin/consent-management/)
* [Consent manager for iOS](https://docs.tealium.com/platforms/ios-swift/consent-management/)

## Consent status

To get the consent status of a user as a callback function, call the [`getConsentStatus()`](https://docs.tealium.com/platforms/flutter-v2/api/tealium/#getconsentstatus) method.

The following example gets the consent status:
```dart
Tealium.getConsentStatus()
  .then((status) => print('Consent Status: $status'));
```

To set the consent status of a user, call the [`setConsentStatus()`](https://docs.tealium.com/platforms/flutter-v2/api/tealium/#setconsentstatus) method.

The following example grants consent:
```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

## Consent categories

To get the consent categories of a user, call the [`getConsentCategories()`](https://docs.tealium.com/platforms/flutter-v2/api/tealium/#getconsentcategories) method.

The following example gets the consent categories for a user:
```dart
Tealium.getConsentCategories()
  .then((categories) =>
      print('Consent Categories: ' + categories.join(",")));
```

To set the consent categories of a user, call the [`setConsentCategories()`](https://docs.tealium.com/platforms/flutter-v2/api/tealium/#setconsentcategories) method, passing a list of consent categories.

The following example sets the consent categories:
```dart
Tealium.setConsentCategories([ConsentCategories.analytics,
    ConsentCategories.email]);
```
