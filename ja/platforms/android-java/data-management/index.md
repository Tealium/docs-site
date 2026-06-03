---
title: データ管理
description: 永続性データと揮発性データの管理について説明します。
url: https://docs.tealium.com/ja/platforms/android-java/data-management/
---
## 使用方法

一部の変数はイベントごとに構成する必要があります。必要な変数データをすべてのイベントに手動で追加する手間を省くため、データを揮発性または永続性のいずれかとして保存するオプションがあります。データは保存されると、各イベント（ライフサイクルイベントを含む）に追加されます。

データ管理の詳細については、[こちら](/ja/platforms/getting-started/mobile-concepts/#data-management)を参照してください。

## 永続性データ

永続性データの値はデバイスで[SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences)として保存され、各イベントにマージされます。これらの値は、アプリを終了し、再度起動しても保持されます。

[`getPersistentDataSources()`](/ja/platforms/android-java/api/data-sources/#getpersistentdatasources) メソッドは、次の例に示すように永続性データを取得します。

 ```java
SharedPreferences sp = instance.getDataSources().getPersistentDataSources();
sp.edit().putInt(&#34;KEY_TEALIUM_INIT_COUNT&#34;, sp.getInt(&#34;KEY_TEALIUM_INIT_COUNT&#34;, 0) &#43; 1).commit();
```

## 揮発性データ

揮発性データの値はデバイスで[SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences)として保存され、各イベントにマージされます。これらの値は、アプリを終了して再起動すると破棄されます。

[`getVolatileDataSources()`](/ja/platforms/android-java/api/data-sources/#getvolatiledatasources) メソッドは、次の例に示すように揮発性データを取得します。

```java
instance.getDataSources().getVolatileDataSources()
   .put(&#34;KEY_TEALIUM_INITIALIZED&#34;, System.currentTimeMillis());
```
