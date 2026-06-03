---
title: 同意管理
description: Flutterでの同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/consent-management/
---これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)をご覧ください。

## 使用法

このモジュールの使用を推奨します。同意管理について[詳しくはこちら](/ja/platforms/getting-started-mobile/consent-management/)。

* [Android用同意マネージャー](/ja/platforms/android-kotlin/consent-management/)
* [iOS用同意マネージャー](/ja/platforms/ios-swift/consent-management/)

## 有効化

以下の例に示すように、[`initializeWithConsentManager()`](/ja/platforms/flutter-v1/api/#initializewithconsentmanager) メソッドを使用して同意管理を有効にし、Tealiumインスタンスを初期化します：

```dart
final teal = Tealium.initializeWithConsentManager(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null);
```