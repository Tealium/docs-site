---
title: VisitorProfile
description: TealiumのFlutter用VisitorProfileクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/visitor-profile/
---これはTealiumのFlutter用の以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)をご覧ください。

## クラス: `VisitorProfile`

`VisitorProfile` クラスは、Tealium Customer Data Hubからの現在の訪問プロファイルに関連するすべてのデータを含んでいます。以下のドキュメントは、Flutter用の `VisitorProfile` モジュールの一般的に使用されるメソッドとプロパティをまとめたものです。

**属性のタイプ**

| パラメータ         | プロパティ                                                                                                                | 値                                                                                                                             |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                              | `id: &#34;5129&#34;, value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                               | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                               | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]`                                                              |
| `audiences`        | id: String, value: String                                                                                                 | `id: &#34;tealiummobile_demo_103&#34;, value: &#34;iOS Users&#34;`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                                | `id: &#34;2815&#34;, value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                                | `id: &#34;4868&#34;, value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問のすべての属性 `visitorProfile` オブジェクト。現在の訪問プロファイルにはオーディエンスやバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `dates`            | id: String, value: Number                                                                                                 | `id: &#34;22&#34;, value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                                 | `id: &#34;5728&#34;, value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set(String)                                                                                            | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`                                                                |
| `strings`          | id: String, value: String                                                                                                 | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                                 | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Number                                                                                                 | `[&#34;category 1&#34;: 2.0]`                                                                                                             |