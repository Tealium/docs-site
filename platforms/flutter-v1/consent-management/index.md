---
title: Consent management
description: Learn how to implement consent management for Flutter.
url: https://docs.tealium.com/platforms/flutter-v1/consent-management/
---
<blockquote>
This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Usage

Usage of this module is recommended. [Learn more](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) about consent management.

* [Consent manager for Android](https://docs.tealium.com/platforms/android-kotlin/consent-management/)
* [Consent manager for iOS](https://docs.tealium.com/platforms/ios-swift/consent-management/)

## Enable

The [`initializeWithConsentManager()`](https://docs.tealium.com/platforms/flutter-v1/api/#initializewithconsentmanager) method enables consent management and initializes the Tealium instance, as shown in the following example:

```dart
final teal = Tealium.initializeWithConsentManager("ACCOUNT", "PROFILE", "ENVIRONMENT", null, null);
```
