---
title: データ管理
description: 永続データと揮発性データの管理方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-java/data-management/
---
## 使用方法

一部の変数は、すべてのイベントで必須です。必須の変数データを各イベントに手動で追加する手間を省くため、データを揮発性データまたは永続データとして保存できます。保存されたデータは、ライフサイクルイベントを含むすべてのイベントに追加されます。

データ管理について詳しくは、[こちら](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)を参照してください。

## 永続データ

永続データの値は、デバイス上に[SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences)として保存され、各イベントにマージされます。これらの値は、アプリを再起動しても保持されます。

[`getPersistentDataSources()`](https://docs.tealium.com/ja/platforms/android-java/api/data-sources/#getpersistentdatasources) メソッドは、次の例に示すように永続データを取得します。

 ```java
SharedPreferences sp = instance.getDataSources().getPersistentDataSources();
sp.edit().putInt("KEY_TEALIUM_INIT_COUNT", sp.getInt("KEY_TEALIUM_INIT_COUNT", 0) + 1).commit();
```

## 揮発性データ

揮発性データの値は、デバイス上に[SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences)として保存され、各イベントにマージされます。これらの値は、アプリを終了して再起動すると破棄されます。

[`getVolatileDataSources()`](https://docs.tealium.com/ja/platforms/android-java/api/data-sources/#getvolatiledatasources) メソッドは、次の例に示すように揮発性データを取得します。

```java
instance.getDataSources().getVolatileDataSources()
   .put("KEY_TEALIUM_INITIALIZED", System.currentTimeMillis());
```