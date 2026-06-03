---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter/data-management/
---
## データの追加

永続データレイヤーにデータを追加するには、[`addToDataLayer()`](/ja/platforms/flutter/api/tealium/#addtodatalayer) メソッドを呼び出します。

次の例では、アプリが再起動するまでの[Expiry](/ja/platforms/flutter/api/tealium-config/#expiry)を構成してデータレイヤーにデータを追加します：
```dart
Tealium.addToDataLayer({&#39;PERSISTENT_KEY&#39;: &#39;PERSISTENT_VALUE&#39;},
    Expiry.untilRestart);
```

## データの取得

永続データレイヤーで指定されたキーの値をコールバック関数として取得するには、[`getFromDataLayer()`](/ja/platforms/flutter/api/tealium/#getfromdatalayer) メソッドを呼び出します。

次の例では、指定されたキーの値を取得します：
```dart
Tealium.getFromDataLayer(&#39;PERSISTENT_KEY&#39;)
    .then((value) =&gt; print(&#39;Value From data layer: $value&#39;));
```

## データの削除

データレイヤーからデータを削除するには、[`removeFromDataLayer()`](/ja/platforms/flutter/api/tealium/#removefromdatalayer) メソッドを呼び出します。

次の例では、指定されたキーのキー値ペアをデータレイヤーから削除します：
```dart
Tealium.removeFromDataLayer([&#39;PERSISTENT_KEY&#39;]);
```

## トラックデータの収集

コレクターやデータレイヤーからすべてのデータを収集するには、[`gatherTrackData()`](/ja/platforms/flutter/api/tealium/#gathertrackdata) メソッドを呼び出します。

```dart
Tealium.gatherTrackData()
    .then((data) =&gt; print(&#39;Gather track data: $data&#39;));
```