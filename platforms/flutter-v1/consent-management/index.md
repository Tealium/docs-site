---
title: Consent management
description: Learn how to implement consent management for Flutter.
url: https://docs.tealium.com/platforms/flutter-v1/consent-management/
---This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

## Usage

Usage of this module is recommended. [Learn more](/platforms/getting-started-mobile/consent-management/) about consent management.

* [Consent manager for Android](/platforms/android-kotlin/consent-management/)
* [Consent manager for iOS](/platforms/ios-swift/consent-management/)

## Enable

The [`initializeWithConsentManager()`](/platforms/flutter-v1/api/#initializewithconsentmanager) method enables consent management and initializes the Tealium instance, as shown in the following example:

```dart
final teal = Tealium.initializeWithConsentManager(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null);
```
