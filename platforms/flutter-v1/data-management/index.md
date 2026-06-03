---
title: Data management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/flutter-v1/data-management/
---This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent data

The [`setPersistentData()`](/platforms/flutter-v1/api/#setpersistentdata) method adds persistent data, as shown in the following example:   

```dart
Tealium.setPersistentData({
     &#34;KEY1&#34;: &#34;VALUE1&#34;,
     &#34;KEY2&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;, &#34;STRING3&#34;]});
```
The [`getPersistentData()`](/platforms/flutter-v1/api/#getpersistentdata) method gets persistent data, as shown in the following example:   

```dart
Tealium.getPersistentData(&#34;KEY1&#34;);
```

The [`removePersistentData()`](/platforms/flutter-v1/api/#removepersistentdata) method removes persistent data, as shown in the following example:

```dart
Tealium.removePersistentData([&#34;KEY1&#34;, &#34;KEY2&#34;]);
```


## Volatile data

The [`setVolatileData()`](/platforms/flutter-v1/api/#setvolatiledata) method adds volatile data, as shown in the following example:   

```dart
Tealium.setVolatileData({
  &#34;KEY1&#34;: &#34;VALUE1&#34;,
  &#34;KEY2&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;, &#34;STRING3&#34;]
    });
```


The [`getVolatileData()`](/platforms/flutter-v1/api/#getvolatiledata) method gets volatile data, as shown in the following example:

```dart
Tealium.getVolatileData(&#34;KEY1&#34;);
```


The [`removeVolatileData()`](/platforms/flutter-v1/api/#removevolatiledata) method removes volatile data, as shown in the following example:     

```dart
Tealium.removeVolatileData([&#34;KEY1&#34;, &#34;KEY2&#34;]);
```
