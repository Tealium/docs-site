---
title: CurrentVisit
description: Tealium for Android（Kotlin）によって提供されるCurrentVisitクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/current-visit/
---
## クラス: `CurrentVisit`

`CurrentVisit`は、Tealium Customer Data Hubからの現在の訪問プロファイルに関連するすべてのデータを含んでいます。[`VisitorProfile`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-profile/)と同じAPIを持ち、追加のプロパティ[`createdAt`](#createdat)があります。

### `createdAt`

このCurrent Visitオブジェクトが作成された時刻を記述するタイムスタンプを返します。

```java
visitorProfile.currentVisit?.let { visit ->
    Log.d("VisitorService", "Visit created at ${visit.createdAt}")
}
```
