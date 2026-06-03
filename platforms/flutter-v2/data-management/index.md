---
title: Data management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/flutter-v2/data-management/
---This is the previous version (2.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

## Add data

To add data to the persistent data layer, call the [`addToDataLayer()`](/platforms/flutter-v2/api/tealium/#addtodatalayer) method.

The following example adds data to the data layer, with the [Expiry](/platforms/flutter-v2/api/tealium-config/#expiry) set until the app restarts:
```dart
Tealium.addToDataLayer({&#39;PERSISTENT_KEY&#39;: &#39;PERSISTENT_VALUE&#39;},
    Expiry.untilRestart);
```

## Get data

To get the value for a specified key in the persistent data layer as a callback function, call the [`getFromDataLayer()`](/platforms/flutter-v2/api/tealium/#getfromdatalayer) method.

The following example gets the value for the specified key:
```dart
Tealium.getFromDataLayer(&#39;PERSISTENT_KEY&#39;)
    .then((value) =&gt; print(&#39;Value From data layer: $value&#39;));
```

## Remove data

To remove data from the data layer, call the [`removeFromDataLayer()`](/platforms/flutter-v2/api/tealium/#removefromdatalayer) method.

The following example removes the key-value pairs from the data layer for the specified keys:
```dart
Tealium.removeFromDataLayer([&#39;PERSISTENT_KEY&#39;]);
```

## Gather track data

To gather all the data from collectors and datalayer, call the [`gatherTrackData()`](/platforms/flutter-v2/api/tealium/#gathertrackdata) method.

```dart
Tealium.gatherTrackData()
    .then((data) =&gt; print(&#39;Gather track data: $data&#39;));
```