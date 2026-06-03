---
title: VisitorProfile
description: Tealium for Android (Kotlin)によって提供されるVisitorProfileクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-profile/
---
## クラス: `VisitorProfile`

VisitorProfileクラスは、Tealium Customer Data Hubからの現在の訪問プロファイルに関連するすべてのデータを含んでいます。以下のドキュメントは、Kotlinの`VisitorProfile`モジュールの一般的に使用されるメソッドとプロパティをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`arraysOfBooleans`](#arraysofbooleans) | 属性識別子と`List&lt;Boolean&gt;`値のマップ |
| [`arraysOfNumbers`](#arraysofnumbers) | 属性識別子と`List&lt;Double&gt;`値のマップ |
| [`arraysOfStrings`](#arraysofstrings) | 属性識別子と`List&lt;String&gt;`値のマップ  |
| [`audiences`](#audiences) | オーディエンス識別子とそれぞれの名前のマップ |
| [`badges`](#badges) | バッジ識別子とそれが割り当てられているかどうかを示すブール値のマップ |
| [`booleans`](#booleans) | 属性識別子と`Boolean`値のマップ |
| [`currentVisit`](#currentvisit) | 訪問スコープの属性を含むプロパティ |
| [`dates`](#dates) | 属性識別子と日付/時間を表す`Long`値のマップ |
| [`numbers`](#numbers) | 属性識別子と`Double`値のマップ |
| [`setsOfStrings`](#setofstrings) | 属性識別子と`Set&lt;String&gt;`値のマップ |
| [`strings`](#strings) | 属性識別子と`String`値のマップ |
| [`tallies`](#tallies) | 属性識別子と`Map&lt;String, Double&gt;`値のマップ |
| [`totalEventCount`](#totaleventcount) | この訪問プロファイルの総イベント数を表すプロパティ |


### `arraysOfBooleans`

訪問プロファイルに現在構成されているブール値の配列属性へのアクセスを提供します。マップの`key`はブール値の配列属性識別子で、`value`は値を含む`List&lt;Boolean&gt;`です。

```java
visitorProfile.arraysOfBooleans?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // アクションを実行
    }
}
```

### `arraysOfNumbers`

訪問プロファイルに現在構成されている数値の配列属性へのアクセスを提供します。マップの`key`は数値の配列属性識別子で、`value`は値を含む`List&lt;Double&gt;`です。

```java
visitorProfile.arraysOfNumbers?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // アクションを実行
    }
}
```

### `arraysOfStrings`

訪問プロファイルに現在構成されている文字列の配列属性へのアクセスを提供します。マップの`key`は文字列の配列属性識別子で、`value`は値を含む`List&lt;String&gt;`です。

```java
visitorProfile.arraysOfStrings?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // アクションを実行
    }
}
```

### `audiences`

訪問が現在所属しているオーディエンスへのアクセスを提供します。マップの`key`はオーディエンス識別子で、`value`はオーディエンスの名前です。

```java
visitorProfile.audiences?.forEach { entry -&gt;
    Log.d(&#34;VisitorService&#34;, &#34;In audience: ${entry.value}&#34;)
}
```

### `badges`

訪問に現在割り当てられているバッジへのアクセスを提供します。マップの`key`はバッジ属性識別子で、`value`はバッジが割り当てられているかどうかを示す`Boolean`です。

```java
visitorProfile.badges?.get(&#34;5120&#34;)?.let {
    if (it) {
        // アクションを実行
    }
}
```


### `booleans`

訪問プロファイルに現在構成されているブール属性へのアクセスを提供します。マップの`key`はブール属性識別子で、`value`は属性の`Boolean`値です。

```java
visitorProfile.booleans?.get(&#34;5120&#34;)?.let {
    if (it) {
        // アクションを実行
    }
}
```

### `currentVisit`

訪問スコープの属性の最新の値を含む[`CurrentVisit`](/ja/platforms/android-kotlin/api/current-visit/)オブジェクトを返します。これは、`VisitorProfile`オブジェクト直接に利用可能な訪問スコープのものとは対照的です。

```java
visitorProfile.currentVisit?.let { visit -&gt;
    if (visit.totalEventCount &gt; 10) {
        // アクションを実行
    }
}
```

### `dates`

訪問プロファイルに現在構成されている日付属性へのアクセスを提供します。マップの`key`は日付属性識別子で、`value`はタイムスタンプを表す`Long`です。

```java
visitorProfile.dates?.get(&#34;5120&#34;)?.let {
    if (it &gt; System.currentTimeMillis()) {
        // アクションを実行
    }
}
```


### `numbers`

訪問プロファイルに現在構成されている数値属性へのアクセスを提供します。マップの`key`は数値属性識別子で、`value`は属性の`Double`値です。

```java
visitorProfile.numbers?.get(&#34;5120&#34;)?.let {
    if (it &gt; 100.0) {
        // アクションを実行
    }
}
```

### `setsOfStrings`

訪問プロファイルに現在構成されている文字列のセット属性へのアクセスを提供します。マップの`key`は文字列のセット属性識別子で、`value`は値を含む`Set&lt;String&gt;`です。

```java
visitorProfile.setsOfStrings?.get(&#34;5120&#34;)?.let {
    it.forEach {
        // アクションを実行
    }
}
```

### `strings`

訪問プロファイルに現在構成されている文字列属性へのアクセスを提供します。マップの`key`は文字列属性識別子で、`value`は属性の`String`値です。

```java
visitorProfile.strings?.get(&#34;5120&#34;)?.let {
    if (it == &#34;Some String Value&#34;) {
        // アクションを実行
    }
}
```

### `tallies`

訪問プロファイルに現在構成されている集計属性へのアクセスを提供します。マップの`key`は集計属性識別子で、`value`は属性の`Map&lt;String, Double&gt;`値です。

```java
visitorProfile.tallies?.get(&#34;5120&#34;)?.let { tallies -&gt;
    val highestTally = tallies.maxBy { it.value }
    // アクションを実行
}
```

### `totalEventCount`

この訪問の総イベント数を`Int`で返します。

```java
if (visitorProfile.totalEventCount &gt; 100) {
    // アクションを実行
}
```
