---
title: Install
description: Learn to install Tealium for Flutter.
url: https://docs.tealium.com/platforms/flutter-v2/install/
---
<blockquote>
This is the previous version (2.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


Tealium for Flutter lets you use the Tealium native mobile libraries for [Android](https://docs.tealium.com/platforms/android-kotlin/) or [iOS](https://docs.tealium.com/platforms/ios-swift/) in your Flutter application.

## Requirements

* [Flutter](https://flutter.dev/) application development framework
* IDE such as [Android Studio](https://developer.android.com/studio) or [VS Code](https://code.visualstudio.com/)
* Flutter plugin installed on the IDE


<blockquote>
Tealium for Flutter is not compatible with Flutter web applications. To track Flutter web applications, use [Tealium for JavaScript](https://docs.tealium.com/platforms/javascript/).
</blockquote>


## Sample app

To help to familiarize yourself with our library, the tracking methods, and best practice implementation, explore the Tealium for Flutter [sample app](https://github.com/Tealium/tealium-flutter/tree/master/tealium/example).

## Install

To install the Tealium library for Flutter:

1. In your Flutter app project, update the `pubspec.yaml` file to add the Tealium Flutter plugin dependency as follows:
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: '2.6.3'
      ```

1. To pull the Tealium Flutter plugin dependency in your project, run the following command:
      ```bash
      flutter pub get
      ```

1. Import the Dart code to your project:
      ```dart
      import 'package:tealium/common.dart';
      import 'package:tealium/tealium.dart';
      ```

Use the Tealium APIs in your Flutter project.

## Initialize

Initialize the Tealium instance with the [`initialize()`](https://docs.tealium.com/platforms/flutter-v2/api/tealium/#initialize) method, as shown in the following example:

```dart
final config = TealiumConfig(
    'ACCOUNT',
    'PROFILE',
    TealiumEnvironment.dev,
    [Collectors.AppData, Collectors.Lifecycle],
    [Dispatchers.RemoteCommands, Dispatchers.TagManagement],
    consentPolicy: ConsentPolicy.GDPR,
    useRemoteLibrarySettings: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    consentExpiry: ConsentExpiry(5, TimeUnit.MINUTES)
);

Tealium.initialize(config).then((value) {
    print('Tealium initialized');
});
```

See the [Flutter API](https://docs.tealium.com/platforms/flutter-v2/api/) to learn more about initialization options.
