---
title: Data Management
description: Learn to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/android-java/data-management/
---
## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent Data

Persistent data values are stored on the device as [SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences) and are merged into each event. They are preserved between launches of the app.

The [`getPersistentDataSources()`](https://docs.tealium.com/platforms/android-java/api/data-sources/#getpersistentdatasources) method gets persistent data, as shown in the following example:

 ```java
SharedPreferences sp = instance.getDataSources().getPersistentDataSources();
sp.edit().putInt("KEY_TEALIUM_INIT_COUNT", sp.getInt("KEY_TEALIUM_INIT_COUNT", 0) + 1).commit();
```

## Volatile Data

Volatile data values are stored on the device as [SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences) and are merged into to each event. They are discarded upon closing the app and restarting.

The [`getVolatileDataSources()`](https://docs.tealium.com/platforms/android-java/api/data-sources/#getvolatiledatasources) method gets volatile data, as shown in the following example:

```java
instance.getDataSources().getVolatileDataSources()
   .put("KEY_TEALIUM_INITIALIZED", System.currentTimeMillis());
```
