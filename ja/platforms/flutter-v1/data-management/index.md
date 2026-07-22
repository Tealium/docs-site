---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/data-management/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## 使用法

すべてのイベントに必要な変数があります。すべてのイベントに必要な変数データを手動で追加するのを防ぐために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理についてもっと学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 永続的データ

次の例に示すように、[`setPersistentData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#setpersistentdata) メソッドは永続的データを追加します。

```dart
Tealium.setPersistentData({
     "KEY1": "VALUE1",
     "KEY2": ["STRING1", "STRING2", "STRING3"]});
```
次の例に示すように、[`getPersistentData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#getpersistentdata) メソッドは永続的データを取得します。

```dart
Tealium.getPersistentData("KEY1");
```

次の例に示すように、[`removePersistentData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#removepersistentdata) メソッドは永続的データを削除します。

```dart
Tealium.removePersistentData(["KEY1", "KEY2"]);
```

## 揮発性データ

次の例に示すように、[`setVolatileData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#setvolatiledata) メソッドは揮発性データを追加します。

```dart
Tealium.setVolatileData({
  "KEY1": "VALUE1",
  "KEY2": ["STRING1", "STRING2", "STRING3"]
    });
```

次の例に示すように、[`getVolatileData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#getvolatiledata) メソッドは揮発性データを取得します。

```dart
Tealium.getVolatileData("KEY1");
```

次の例に示すように、[`removeVolatileData()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#removevolatiledata) メソッドは揮発性データを削除します。

```dart
Tealium.removeVolatileData(["KEY1", "KEY2"]);
```