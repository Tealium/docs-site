---
title: 同意管理
description: Flutterでの同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v1/consent-management/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## 使用法

このモジュールの使用を推奨します。同意管理について[詳しくはこちら](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)。

* [Android用同意マネージャー](https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/)
* [iOS用同意マネージャー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/)

## 有効化

以下の例に示すように、[`initializeWithConsentManager()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#initializewithconsentmanager) メソッドを使用して同意管理を有効にし、Tealiumインスタンスを初期化します：

```dart
final teal = Tealium.initializeWithConsentManager("ACCOUNT", "PROFILE", "ENVIRONMENT", null, null);
```