---
title: Moments API module
description: Learn how to install the Tealium Moments API module for Flutter.
url: https://docs.tealium.com/platforms/flutter-v2/moments-api/
---This is the previous version (2.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

Tealium for Flutter lets you use the Tealium mobile libraries (iOS, Android) to install the Moments API Module for the Tealium Flutter plugin.

## How it works

Tealium mobile libraries can be integrated into your Flutter application using one of the following methods:

* Dart package (Recommended)
* Manually with [GitHub](https://github.com/Tealium/tealium-flutter)

## Requirements

* [Flutter](https://flutter.dev/) application development framework
* IDE, such as [Android Studio](https://developer.android.com/studio) or [VS Code](https://code.visualstudio.com/)
* Flutter [plugin](https://github.com/flutter/plugins) installed on the IDE

## Install

To install the Tealium library for Flutter:

1. In your Flutter app project, run the following command:
    ```bash
    dart pub add tealium_moments_api
    ```
1. Import the following Dart code into your project:   
    ```dart
    import &#39;package:tealium_moments_api/common.dart&#39;;
    import &#39;package:tealium_moments_api/tealium_moments_api.dart&#39;;
    ```

## Initialize

Configure the Moments API module before initializing the main Tealium Flutter integration.

Set the Moments API Region as specified in the Moments API interface. The following regions are available:

* `GERMANY`
* `US_EAST`
* `SYDNEY`
* `OREGON`
* `TOKYO`
* `HONG_KONG`

If you are using the [domain allow list](), set the referrer to an allowed domain.

The following example code uses the `US_EAST` region and `example.com` as the referrer to match the allowed domain:

```dart
final config = MomentsApiConfig(
    MomentsApiRegion.US_EAST,   // required
    &#34;https://example.com&#34;);     // optional

// Configure the module
TealiumMomentsApi.configure(config);

// ... Initialize main Tealium plugin
```

## Class: TealiumMomentsApi

After the Moments API Module and the main Tealium Flutter integration have both been initialized, you can retrieve engine data by ID.

### `fetchEngineResponse`

Retrieves the engine response for the given engine ID. 

```dart
TealiumMomentsApi.fetchEngineResponse(
    engineId: &#34;ENGINEID&#34;,
    callback: (response) {
        if (response is EngineResponse) {
            // handle success
            final audiences = response.audiences;
            // do something
        } else if (response is String) {
            // handle error
        }
    }
);
```

#### Parameters

| Parameter | Type | Description |
| ---- | ---- | ---- |
| `engineId` | `String` | The ID of the engine to check |
| `callback` | `Function(dynamic)` | Callback that receives an `EngineResponse` on success or a `String` error message on failure |

### `EngineResponse`

The `EngineResponse` class contains the visitor data returned from the Moments API engine.

| Property | Type | Description |
| ---- | ---- | ---- |
| `audiences` | `List&lt;String&gt;?` | Audience IDs the visitor belongs to |
| `badges` | `List&lt;String&gt;?` | Badges assigned to the visitor |
| `strings` | `Map&lt;String, String&gt;?` | String attributes |
| `booleans` | `Map&lt;String, bool&gt;?` | Boolean attributes |
| `dates` | `Map&lt;String, int&gt;?` | Date attributes (as timestamps) |
| `numbers` | `Map&lt;String, double&gt;?` | Numeric attributes |