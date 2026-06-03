---
title: Consent management
description: Learn how to implement consent management for Flutter.
url: https://docs.tealium.com/platforms/flutter/consent-management/
---

## Usage

Usage of this module is recommended. [Learn more](/platforms/getting-started-mobile/consent-management/) about consent management.

* [Consent manager for Android](/platforms/android-kotlin/consent-management/)
* [Consent manager for iOS](/platforms/ios-swift/consent-management/)

## Consent status


To get the consent status of a user as a callback function, call the [`getConsentStatus()`](/platforms/flutter/api/tealium/#getconsentstatus) method.

The following example gets the consent status:    
```dart
Tealium.getConsentStatus()
  .then((status) =&gt; print(&#39;Consent Status: $status&#39;));
```


To set the consent status of a user, call the [`setConsentStatus()`](/platforms/flutter/api/tealium/#setconsentstatus) method.

The following example grants consent:    
```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```


## Consent categories

To get the consent categories of a user, call the [`getConsentCategories()`](/platforms/flutter/api/tealium/#getconsentcategories) method.

The following example gets the consent categories for a user:    
```dart
Tealium.getConsentCategories()
  .then((categories) =&gt;
      print(&#39;Consent Categories: &#39; &#43; categories.join(&#34;,&#34;)));
```


To set the consent categories of a user, call the [`setConsentCategories()`](/platforms/flutter/api/tealium/#setconsentcategories) method, passing a list of consent categories.

The following example sets the consent categories:    
```dart
Tealium.setConsentCategories([ConsentCategories.analytics,
    ConsentCategories.email]);
```
