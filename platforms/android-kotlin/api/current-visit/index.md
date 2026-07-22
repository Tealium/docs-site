---
title: CurrentVisit
description: Reference guide for CurrentVisit class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/current-visit/
---
## Class: `CurrentVisit`

The `CurrentVisit` contains all data associated with the current visitor profile from the Tealium Customer Data Hub. It has the same API as the [`VisitorProfile`](https://docs.tealium.com/platforms/android-kotlin/api/visitor-profile/) with one additional property: [`createdAt`](#createdat).

### `createdAt`

Returns the timestamp describing the time at which this Current Visit object was created.

```java
visitorProfile.currentVisit?.let { visit ->
    Log.d("VisitorService", "Visit created at ${visit.createdAt}")
}
```
