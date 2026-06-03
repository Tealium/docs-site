---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/data-management/
---これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)をご覧ください。

## 使用法

すべてのイベントに必要な変数があります。すべてのイベントに必要な変数データを手動で追加するのを防ぐために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理についてもっと学ぶ](/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 永続的データ

次の例に示すように、[`setPersistentData()`](/ja/platforms/flutter-v1/api/#setpersistentdata) メソッドは永続的データを追加します。

```dart
Tealium.setPersistentData({
     &#34;KEY1&#34;: &#34;VALUE1&#34;,
     &#34;KEY2&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;, &#34;STRING3&#34;]});
```
次の例に示すように、[`getPersistentData()`](/ja/platforms/flutter-v1/api/#getpersistentdata) メソッドは永続的データを取得します。

```dart
Tealium.getPersistentData(&#34;KEY1&#34;);
```

次の例に示すように、[`removePersistentData()`](/ja/platforms/flutter-v1/api/#removepersistentdata) メソッドは永続的データを削除します。

```dart
Tealium.removePersistentData([&#34;KEY1&#34;, &#34;KEY2&#34;]);
```

## 揮発性データ

次の例に示すように、[`setVolatileData()`](/ja/platforms/flutter-v1/api/#setvolatiledata) メソッドは揮発性データを追加します。

```dart
Tealium.setVolatileData({
  &#34;KEY1&#34;: &#34;VALUE1&#34;,
  &#34;KEY2&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;, &#34;STRING3&#34;]
    });
```

次の例に示すように、[`getVolatileData()`](/ja/platforms/flutter-v1/api/#getvolatiledata) メソッドは揮発性データを取得します。

```dart
Tealium.getVolatileData(&#34;KEY1&#34;);
```

次の例に示すように、[`removeVolatileData()`](/ja/platforms/flutter-v1/api/#removevolatiledata) メソッドは揮発性データを削除します。

```dart
Tealium.removeVolatileData([&#34;KEY1&#34;, &#34;KEY2&#34;]);
```