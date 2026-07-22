---
title: VisitorProfile
description: Reference guide for VisitorProfile class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/visitor-profile/
---
## Class: `VisitorProfile`

The VisitorProfile class contains all data associated with the current visitor profile from the Tealium Customer Data Hub. The following document summarizes the commonly used methods and properties of the `VisitorProfile` module for Kotlin.

| Method/Property | Description |
| ----- | ------ |
| [`arraysOfBooleans`](#arraysofbooleans) | Map of attribute identifiers and `List<Boolean>` values |
| [`arraysOfNumbers`](#arraysofnumbers) | Map of attribute identifiers and `List<Double>` values |
| [`arraysOfStrings`](#arraysofstrings) | Map of attribute identifiers and `List<String>` values  |
| [`audiences`](#audiences) | Map of Audience identifiers and their respective names |
| [`badges`](#badges) | Map of badge identifiers and a boolean signifying whether it is assigned |
| [`booleans`](#booleans) | Map of attribute identifiers and `Boolean` values |
| [`currentVisit`](#currentvisit) | Property containing the visit-scoped Attributes |
| [`dates`](#dates) | Map of attribute identifiers and `Long` values describing the Date/Time |
| [`numbers`](#numbers) | Map of attribute identifiers and `Double` values |
| [`setsOfStrings`](#setofstrings) | Map of attribute identifiers and `Set<String>` values |
| [`strings`](#strings) | Map of attribute identifiers and `String` values |
| [`tallies`](#tallies) | Map of attribute identifiers and `Map<String, Double>` values |
| [`totalEventCount`](#totaleventcount) | Property representing the total event count for this visitor profile |


### `arraysOfBooleans`

Provides access to the array of booleans attributes currently set on the visitor profile. The map's `key` is the array of booleans attribute identifier, and the `value` is a `List<Boolean>` containing the values.

```java
visitorProfile.arraysOfBooleans?.get("5120")?.let {
    it.forEach {
        // take action
    }
}
```

### `arraysOfNumbers`

Provides access to the array of numbers attributes currently set on the visitor Profile. The map's `key` is the array of numbers attribute identifier, and the `value` is a `List<Double>` containing the values.

```java
visitorProfile.arraysOfNumbers?.get("5120")?.let {
    it.forEach {
        // take action
    }
}
```

### `arraysOfStrings`

Provides access to the array of strings attributes currently set on the visitor profile. The map's `key` is the array of strings attribute identifier, and the `value` is a `List<String>` containing the values.

```java
visitorProfile.arraysOfStrings?.get("5120")?.let {
    it.forEach {
        // take action
    }
}
```

### `audiences`

Provides access to the audiences that the visitor is currently in. The map's `key` is the audience identifier, and the `value` is the audience name.

```java
visitorProfile.audiences?.forEach { entry ->
    Log.d("VisitorService", "In audience: ${entry.value}")
}
```

### `badges`

Provides access to the badges that the visitor currently has assigned. The map's `key` is the badge attribute identifier, and the `value` is a `Boolean` signifying if the badge is assigned.

```java
visitorProfile.badges?.get("5120")?.let {
    if (it) {
        // take action
    }
}
```


### `booleans`

Provides access to the Boolean attributes currently set on the visitor profile. The map's `key` is the boolean attribute identifier, and the `value` is a `Boolean` value of the attribute.

```java
visitorProfile.booleans?.get("5120")?.let {
    if (it) {
        // take action
    }
}
```

### `currentVisit`

Returns a [`CurrentVisit`](https://docs.tealium.com/platforms/android-kotlin/api/current-visit/) object containing the up-to-date values for visit-scoped attributes as opposed to visitor-scoped ones available on the `VisitorProfile` object directly.

```java
visitorProfile.currentVisit?.let { visit ->
    if (visit.totalEventCount > 10) {
        // take action
    }
}
```

### `dates`

Provides access to the date attributes currently set on the visitor profile. The Map's `key` is the date attribute identifier, and the `value` is a `Long` describing a timestamp.

```java
visitorProfile.dates?.get("5120")?.let {
    if (it > System.currentTimeMillis()) {
        // take action
    }
}
```


### `numbers`

Provides access to the number attributes currently set on the visitor profile. The map's `key` is the number attribute identifier, and the `value` is a `Double` value of the attribute.

```java
visitorProfile.numbers?.get("5120")?.let {
    if (it > 100.0) {
        // take action
    }
}
```

### `setsOfStrings`

Provides access to the sets of strings attributes currently set on the visitor profile. The map's `key` is the sets of strings attribute identifier, and the `value` is a `Set<String>` containing the values.

```java
visitorProfile.setsOfStrings?.get("5120")?.let {
    it.forEach {
        // take action
    }
}
```

### `strings`

Provides access to the String Attributes currently set on the visitor profile. The map's `key` is the string attribute identifier, and the `value` is a `String` value of the attribute.

```java
visitorProfile.strings?.get("5120")?.let {
    if (it == "Some String Value") {
        // take action
    }
}
```

### `tallies`

Provides access to the tally attributes currently set on the visitor profile. The map's `key` is the tally attribute identifier, and the `value` is a `Map<String, Double>` value of the attribute.

```java
visitorProfile.tallies?.get("5120")?.let { tallies ->
    val highestTally = tallies.maxBy { it.value }
    // take action
}
```

### `totalEventCount`

Returns an `Int` of the total event count for this visitor.

```java
if (visitorProfile.totalEventCount > 100) {
    // take action
}
```
