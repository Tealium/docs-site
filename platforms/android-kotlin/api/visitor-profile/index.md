---
title: VisitorProfile
description: Reference guide for VisitorProfile class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/visitor-profile/
---
## Class: `VisitorProfile`

The VisitorProfile class contains all data associated with the current visitor profile from the Tealium Customer Data Hub. The following document summarizes the commonly used methods and properties of the `VisitorProfile` module for Kotlin.

| Method/Property | Description |
| ----- | ------ |
| [`arraysOfBooleans`](#arraysofbooleans) | Map of attribute identifiers and `List&lt;Boolean&gt;` values |
| [`arraysOfNumbers`](#arraysofnumbers) | Map of attribute identifiers and `List&lt;Double&gt;` values |
| [`arraysOfStrings`](#arraysofstrings) | Map of attribute identifiers and `List&lt;String&gt;` values  |
| [`audiences`](#audiences) | Map of Audience identifiers and their respective names |
| [`badges`](#badges) | Map of badge identifiers and a boolean signifying whether it is assigned |
| [`booleans`](#booleans) | Map of attribute identifiers and `Boolean` values |
| [`currentVisit`](#currentvisit) | Property containing the visit-scoped Attributes |
| [`dates`](#dates) | Map of attribute identifiers and `Long` values describing the Date/Time |
| [`numbers`](#numbers) | Map of attribute identifiers and `Double` values |
| [`setsOfStrings`](#setofstrings) | Map of attribute identifiers and `Set&lt;String&gt;` values |
| [`strings`](#strings) | Map of attribute identifiers and `String` values |
| [`tallies`](#tallies) | Map of attribute identifiers and `Map&lt;String, Double&gt;` values |
| [`totalEventCount`](#totaleventcount) | Property representing the total event count for this visitor profile |


### `arraysOfBooleans`

Provides access to the array of booleans attributes currently set on the visitor profile. The map&#39;s `key` is the array of booleans attribute identifier, and the `value` is a `List&lt;Boolean&gt;` containing the values.

```java
visitorProfile.arraysOfBooleans?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // take action
    }
}
```

### `arraysOfNumbers`

Provides access to the array of numbers attributes currently set on the visitor Profile. The map&#39;s `key` is the array of numbers attribute identifier, and the `value` is a `List&lt;Double&gt;` containing the values.

```java
visitorProfile.arraysOfNumbers?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // take action
    }
}
```

### `arraysOfStrings`

Provides access to the array of strings attributes currently set on the visitor profile. The map&#39;s `key` is the array of strings attribute identifier, and the `value` is a `List&lt;String&gt;` containing the values.

```java
visitorProfile.arraysOfStrings?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // take action
    }
}
```

### `audiences`

Provides access to the audiences that the visitor is currently in. The map&#39;s `key` is the audience identifier, and the `value` is the audience name.

```java
visitorProfile.audiences?.forEach { entry -&gt;
    Log.d(&#34;VisitorService&#34;, &#34;In audience: ${entry.value}&#34;)
}
```

### `badges`

Provides access to the badges that the visitor currently has assigned. The map&#39;s `key` is the badge attribute identifier, and the `value` is a `Boolean` signifying if the badge is assigned.

```java
visitorProfile.badges?.get(&#34;5120&#34;)?.let {
    if (it) {
        // take action
    }
}
```


### `booleans`

Provides access to the Boolean attributes currently set on the visitor profile. The map&#39;s `key` is the boolean attribute identifier, and the `value` is a `Boolean` value of the attribute.

```java
visitorProfile.booleans?.get(&#34;5120&#34;)?.let {
    if (it) {
        // take action
    }
}
```

### `currentVisit`

Returns a [`CurrentVisit`](/platforms/android-kotlin/api/current-visit/) object containing the up-to-date values for visit-scoped attributes as opposed to visitor-scoped ones available on the `VisitorProfile` object directly.

```java
visitorProfile.currentVisit?.let { visit -&gt;
    if (visit.totalEventCount &gt; 10) {
        // take action
    }
}
```

### `dates`

Provides access to the date attributes currently set on the visitor profile. The Map&#39;s `key` is the date attribute identifier, and the `value` is a `Long` describing a timestamp.

```java
visitorProfile.dates?.get(&#34;5120&#34;)?.let {
    if (it &gt; System.currentTimeMillis()) {
        // take action
    }
}
```


### `numbers`

Provides access to the number attributes currently set on the visitor profile. The map&#39;s `key` is the number attribute identifier, and the `value` is a `Double` value of the attribute.

```java
visitorProfile.numbers?.get(&#34;5120&#34;)?.let {
    if (it &gt; 100.0) {
        // take action
    }
}
```

### `setsOfStrings`

Provides access to the sets of strings attributes currently set on the visitor profile. The map&#39;s `key` is the sets of strings attribute identifier, and the `value` is a `Set&lt;String&gt;` containing the values.

```java
visitorProfile.setsOfStrings?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // take action
    }
}
```

### `strings`

Provides access to the String Attributes currently set on the visitor profile. The map&#39;s `key` is the string attribute identifier, and the `value` is a `String` value of the attribute.

```java
visitorProfile.strings?.get(&#34;5120&#34;)?.let {
    if (it == &#34;Some String Value&#34;) {
        // take action
    }
}
```

### `tallies`

Provides access to the tally attributes currently set on the visitor profile. The map&#39;s `key` is the tally attribute identifier, and the `value` is a `Map&lt;String, Double&gt;` value of the attribute.

```java
visitorProfile.tallies?.get(&#34;5120&#34;)?.let { tallies -&gt;
    val highestTally = tallies.maxBy { it.value }
    // take action
}
```

### `totalEventCount`

Returns an `Int` of the total event count for this visitor.

```java
if (visitorProfile.totalEventCount &gt; 100) {
    // take action
}
```
