---
title: 同意管理
description: Flutterで同意管理を実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/consent-management/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## 使用法

このモジュールの使用を推奨します。同意管理について[詳しくはこちら](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)。

* [Android用同意マネージャー](https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/)
* [iOS用同意マネージャー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/)

## 同意状態

ユーザーの同意状態をコールバック関数として取得するには、[`getConsentStatus()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#getconsentstatus)メソッドを呼び出します。

以下の例では同意状態を取得します：
```dart
Tealium.getConsentStatus()
  .then((status) => print('同意状態: $status'));
```

ユーザーの同意状態を構成するには、[`setConsentStatus()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#setconsentstatus)メソッドを呼び出します。

以下の例では同意を付与します：
```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

## 同意カテゴリ

ユーザーの同意カテゴリを取得するには、[`getConsentCategories()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#getconsentcategories)メソッドを呼び出します。

以下の例ではユーザーの同意カテゴリを取得します：
```dart
Tealium.getConsentCategories()
  .then((categories) =>
      print('同意カテゴリ: ' + categories.join(",")));
```

ユーザーの同意カテゴリを構成するには、[`setConsentCategories()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#setconsentcategories)メソッドを呼び出し、同意カテゴリのリストを渡します。

以下の例では同意カテゴリを構成します：
```dart
Tealium.setConsentCategories([ConsentCategories.analytics,
    ConsentCategories.email]);
```