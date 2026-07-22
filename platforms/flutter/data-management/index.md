---
title: Data management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/flutter/data-management/
---

## Add data

To add data to the persistent data layer, call the [`addToDataLayer()`](https://docs.tealium.com/platforms/flutter/api/tealium/#addtodatalayer) method.

The following example adds data to the data layer, with the [Expiry](https://docs.tealium.com/platforms/flutter/api/tealium-config/#expiry) set until the app restarts:  
```dart
Tealium.addToDataLayer({'PERSISTENT_KEY': 'PERSISTENT_VALUE'},
    Expiry.untilRestart);
```

## Get data

To get the value for a specified key in the persistent data layer as a callback function, call the [`getFromDataLayer()`](https://docs.tealium.com/platforms/flutter/api/tealium/#getfromdatalayer) method.

The following example gets the value for the specified key:  
```dart
Tealium.getFromDataLayer('PERSISTENT_KEY')
    .then((value) => print('Value From data layer: $value'));
```

## Remove data

To remove data from the data layer, call the [`removeFromDataLayer()`](https://docs.tealium.com/platforms/flutter/api/tealium/#removefromdatalayer) method.

The following example removes the key-value pairs from the data layer for the specified keys:
```dart
Tealium.removeFromDataLayer(['PERSISTENT_KEY']);
```

## Gather track data

To gather all the data from collectors and datalayer, call the [`gatherTrackData()`](https://docs.tealium.com/platforms/flutter/api/tealium/#gathertrackdata) method.

```dart
Tealium.gatherTrackData()
    .then((data) => print('Gather track data: $data'));
```
