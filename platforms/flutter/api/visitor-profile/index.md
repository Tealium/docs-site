---
title: VisitorProfile
description: Reference guide for VisitorProfile class and methods provided by Tealium for Flutter.
url: https://docs.tealium.com/platforms/flutter/api/visitor-profile/
---

## Class: `VisitorProfile`

The `VisitorProfile` class contains all data associated with the current visitor profile from the Tealium Customer Data Hub. The following document summarizes the commonly used methods and properties of the `VisitorProfile` module for Flutter.

**Attribute Types**

| Parameters         | Properties                                                                                                                | Value                                                                                                                             |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                              | `id: &#34;5129&#34;, value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                               | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                               | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]`                                                              |
| `audiences`        | id: String, value: String                                                                                                 | `id: &#34;tealiummobile_demo_103&#34;, value: &#34;iOS Users&#34;`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                                | `id: &#34;2815&#34;, value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                                | `id: &#34;4868&#34;, value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit `visitorProfile` object. The current visit profile does not contain audiences or badges. | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `dates`            | id: String, value: Number                                                                                                 | `id: &#34;22&#34;, value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                                 | `id: &#34;5728&#34;, value: 4.82125`                                                                                                      |
| `setsOfStrings`    | id: String, value: Set(String)                                                                                            | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`                                                                |
| `strings`          | id: String, value: String                                                                                                 | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                                 | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                                                                                 |
