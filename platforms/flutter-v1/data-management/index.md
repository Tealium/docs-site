---
title: Data management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/flutter-v1/data-management/
---
<blockquote>
This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent data

The [`setPersistentData()`](https://docs.tealium.com/platforms/flutter-v1/api/#setpersistentdata) method adds persistent data, as shown in the following example:   

```dart
Tealium.setPersistentData({
     "KEY1": "VALUE1",
     "KEY2": ["STRING1", "STRING2", "STRING3"]});
```
The [`getPersistentData()`](https://docs.tealium.com/platforms/flutter-v1/api/#getpersistentdata) method gets persistent data, as shown in the following example:   

```dart
Tealium.getPersistentData("KEY1");
```

The [`removePersistentData()`](https://docs.tealium.com/platforms/flutter-v1/api/#removepersistentdata) method removes persistent data, as shown in the following example:

```dart
Tealium.removePersistentData(["KEY1", "KEY2"]);
```


## Volatile data

The [`setVolatileData()`](https://docs.tealium.com/platforms/flutter-v1/api/#setvolatiledata) method adds volatile data, as shown in the following example:   

```dart
Tealium.setVolatileData({
  "KEY1": "VALUE1",
  "KEY2": ["STRING1", "STRING2", "STRING3"]
    });
```


The [`getVolatileData()`](https://docs.tealium.com/platforms/flutter-v1/api/#getvolatiledata) method gets volatile data, as shown in the following example:

```dart
Tealium.getVolatileData("KEY1");
```


The [`removeVolatileData()`](https://docs.tealium.com/platforms/flutter-v1/api/#removevolatiledata) method removes volatile data, as shown in the following example:     

```dart
Tealium.removeVolatileData(["KEY1", "KEY2"]);
```
