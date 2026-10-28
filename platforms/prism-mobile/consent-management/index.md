---
title: Consent
description: Pass consent data from the Tealium Prism SDK and enforce consent server-side.
url: https://docs.tealium.com/platforms/prism-mobile/consent-management/
---
Consent management is not currently available in Tealium Prism. The SDK does not hold, block, or filter events based on consent. If your local or remote settings contain a consent section, the SDK logs a message and ignores it.

## Recommended approach

1. Pass the consent choices from your consent management platform (CMP) into the Prism data layer, so every event carries them.
1. Enforce consent server-side with [consent orchestration](https://docs.tealium.com/about-consent-orchestration/).

Update the data layer each time the user changes their choices. The attribute name is up to you. These examples use `consent_categories`.



```kotlin
val consentCategories = DataList.create {
    add("analytics")
    add("marketing")
}

tealium.dataLayer.put("consent_categories", consentCategories, Expiry.FOREVER)
```


```swift
tealium.dataLayer.put(key: "consent_categories", converting: ["analytics", "marketing"], expiry: .forever)
```


```javascript
await tealium.dataLayer.put("consent_categories", ["analytics", "marketing"], "forever");
```



Server-side enforcement applies to events that reach Tealium. On-device dispatchers, such as Firebase, send data directly to the vendor. Use the vendor's own consent controls for those dispatchers.
