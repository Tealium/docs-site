---
title: Adobe visitor service module
description: This document explains how to install the Tealium Adobe Visitor Service Module for Flutter.
url: https://docs.tealium.com/platforms/flutter/adobe-visitor-service/
---
Tealium for Flutter lets you use the Tealium mobile libraries (iOS, Android) to install the Adobe Visitor Service Module for the Tealium Flutter plugin.

## How it works

Tealium mobile libraries are integrated into your Flutter application using one of the following methods:

*   Dart package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-flutter)

## Requirements

* [Flutter](https://flutter.dev/) application development framework
* IDE such as [Android Studio](https://developer.android.com/studio) or [VS Code](https://code.visualstudio.com/)
* Flutter [plugin](https://github.com/flutter/plugins) installed on the IDE

## Install

To install the Tealium library for Flutter:

1. In your Flutter app project, run
    ```bash
    dart pub add tealium_adobevisitor
    ```
1. Import the Dart code to your project:
      ```dart
      import &#39;package:tealium_adobevisitor/common.dart&#39;;
      ```

## Initialize

Configure the Adobe Visitor Service module prior to initializing the main Tealium Flutter integration.

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;EXISTING-ECID&#34;,  // optional
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

Set the `adobeVisitorCustomVisitorId`, `adobeVisitorDataProviderId`, and `adobeVisitorAuthState` properties only if all three values are known at the start of the app session. Set `adobeVisitorAuthState` only when you also set `adobeVisitorCustomVisitorId`. If the visitor&#39;s ID is not known at initialization (for example, before login), omit these properties and call [`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierknownid-adobedataproviderid-authstate) once the ID becomes available.

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;EXISTING-ECID&#34;,
    adobeVisitorDataProviderId: &#34;DATA-PROVIDER-ID&#34;,
    adobeVisitorCustomVisitorId: &#34;CUSTOM-VISITOR-ID&#34;,
    adobeVisitorAuthState: AuthState.authenticated,
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

## API reference

After the Adobe Visitor Service Module and the main Tealium Flutter integration have both been initialized, you can link an existing Adobe visitor.

### `linkEcidToKnownIdentifier(knownId, adobeDataProviderId, authState)`

Links existing Experience Cloud ID (ECID) to known identifier.

```dart
final visitor = await TealiumAdobeVisitor.linkEcidToKnownIdentifier(&#34;myidentifier&#34;, &#34;123456&#34;, AuthState.unknown);
```

### `getAdobeVisitor()`

Get the current Adobe visitor information.

```dart
TealiumAdobeVisitor.getAdobeVisitor()
        .then((visitor) =&gt; print(visitor));
```

### `decorateUrl(url)`

Decorates the URL with ECID visitor data.

```dart
String? decoratedUrl = await TealiumAdobeVisitor.decorateUrl(&#34;https://example.com&#34;);
```

### `getUrlParameters()`

Retrieves URL parameters containing the Adobe Visitor ID to be manually appended to a URL.

```dart
TealiumAdobeVisitor.getUrlParameters().then(
                            (value) =&gt;
                            value?.forEach((key, value) {
                                print(&#34;Retrieved URL Parameters: $key = $value&#34;);
                            })
                    );
```

### `resetVisitor()`

Reset current visitor.

```dart
TealiumAdobeVisitor.resetVisitor();
```