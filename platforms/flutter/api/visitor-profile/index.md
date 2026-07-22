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
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                              | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                                 | `id: "tealiummobile_demo_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                                | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                                | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit `visitorProfile` object. The current visit profile does not contain audiences or badges. | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Number                                                                                                 | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                                 | `id: "5728", value: 4.82125`                                                                                                      |
| `setsOfStrings`    | id: String, value: Set(String)                                                                                            | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                                 | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                                 | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
