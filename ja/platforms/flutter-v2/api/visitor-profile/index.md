---
title: VisitorProfile
description: TealiumのFlutter用VisitorProfileクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/visitor-profile/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## クラス: `VisitorProfile`

`VisitorProfile` クラスは、Tealium Customer Data Hubからの現在の訪問プロファイルに関連するすべてのデータを含んでいます。以下のドキュメントは、Flutter用の `VisitorProfile` モジュールの一般的に使用されるメソッドとプロパティをまとめたものです。

**属性のタイプ**

| パラメータ         | プロパティ                                                                                                                | 値                                                                                                                             |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                              | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                                 | `id: "tealiummobile_demo_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                                | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                                | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問のすべての属性 `visitorProfile` オブジェクト。現在の訪問プロファイルにはオーディエンスやバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Number                                                                                                 | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                                 | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set(String)                                                                                            | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                                 | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                                 | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Number                                                                                                 | `["category 1": 2.0]`                                                                                                             |