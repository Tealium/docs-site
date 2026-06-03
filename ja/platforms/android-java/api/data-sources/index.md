---
title: DataSources
description: Tealium for Androidで提供されているDataSourcesクラスおよびメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/data-sources/
---
## クラス：`DataSources`

以下は、一般的に使用される`DataSources`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `getPersistentDataSources()` | 永続性データソースを取得します|  
|` getVolatileDataSources()`| 揮発性データソースを取得します|
| `getVisitorId()` | Tealiumライブラリによって生成される訪問IDを取得します|

### `getPersistentDataSources()`

永続性データソースを取得します。永続性データの値はデバイスで[SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences)として保存され、各イベントにマージされ、アプリを終了し、再度起動しても保持されます。

```java
getPersistentDataSources();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| Persistent data sources | `SharedPreferences` |

### `getVolatileDataSources()`

揮発性データソースを取得します。揮発性データの値は各イベントにマージされますが、アプリを終了して再起動すると破棄されます。

```java
getVolatileDataSources();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| Volatile data sources | `Map` |

### `getVisitorId() `

Tealiumライブラリによって生成される訪問IDを取得します。

```java
getVisitorId();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| Visitor ID | `String` |
