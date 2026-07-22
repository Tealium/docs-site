---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/data-management/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## データの追加

永続データレイヤーにデータを追加するには、[`addToDataLayer()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#addtodatalayer) メソッドを呼び出します。

次の例では、アプリが再起動するまでの[Expiry](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium-config/#expiry)を構成してデータレイヤーにデータを追加します：
```dart
Tealium.addToDataLayer({'PERSISTENT_KEY': 'PERSISTENT_VALUE'},
    Expiry.untilRestart);
```

## データの取得

永続データレイヤーで指定されたキーの値をコールバック関数として取得するには、[`getFromDataLayer()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#getfromdatalayer) メソッドを呼び出します。

次の例では、指定されたキーの値を取得します：
```dart
Tealium.getFromDataLayer('PERSISTENT_KEY')
    .then((value) => print('Value From data layer: $value'));
```

## データの削除

データレイヤーからデータを削除するには、[`removeFromDataLayer()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#removefromdatalayer) メソッドを呼び出します。

次の例では、指定されたキーのキー値ペアをデータレイヤーから削除します：
```dart
Tealium.removeFromDataLayer(['PERSISTENT_KEY']);
```

## トラックデータの収集

コレクターやデータレイヤーからすべてのデータを収集するには、[`gatherTrackData()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#gathertrackdata) メソッドを呼び出します。

```dart
Tealium.gatherTrackData()
    .then((data) => print('Gather track data: $data'));
```