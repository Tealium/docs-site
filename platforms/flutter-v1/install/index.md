---
title: Install
description: Learn to install Tealium for Flutter.
url: https://docs.tealium.com/platforms/flutter-v1/install/
---This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

Tealium for Flutter lets you use the Tealium native mobile libraries for [Android](/platforms/android-java/) or [iOS](/platforms/ios-swift/) in your Flutter application.

## Requirements

* [Flutter](https://flutter.dev/) application development framework
* IDE such as [Android Studio](https://developer.android.com/studio) or [VS Code](https://code.visualstudio.com/)
* Flutter plugin installed on the IDE

 Tealium for Flutter is not compatible with Flutter web applications. To track Flutter web applications, use [Tealium for JavaScript](/platforms/javascript/).

## Install

To install the Tealium library for Flutter:

1. In your Flutter app project, update the `pubspec.yaml` file to add the Tealium Flutter plugin dependency as follows:
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: &#39;1.0.0&#39;
      ```

1. To pull the Tealium Flutter plugin dependency in your project, run the following command:
      ```bash
      flutter pub get
      ```

1. Import the Dart code to your project:   
      ```dart
      import &#39;package:tealium/tealium.dart&#39;;
      ```

Use the Tealium APIs in your Flutter project.

## Initialize

Initialize the Tealium instance with the [`initialize()`](/platforms/flutter-v1/api/#initialize) method, as shown in the following example:

```dart
final teal = Tealium.initialize(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null);
```

The [`initializeCustom()`](/platforms/flutter-v1/api/#initializecustom) method initializes the Tealium instance with all initialization options, as shown in the following example:


```dart
final teal = Tealium.initializeCustom(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null,
      &#34;INSTANCE&#34;, true, null, null, null, true);
```

See the [Flutter API](/platforms/flutter-v1/api/) to learn more about initialization options.
