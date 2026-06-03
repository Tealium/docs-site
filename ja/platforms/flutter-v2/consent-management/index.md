---
title: 同意管理
description: Flutterで同意管理を実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/consent-management/
---これはTealiumのFlutter用の以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)をご覧ください。

## 使用法

このモジュールの使用を推奨します。同意管理について[詳しくはこちら](/ja/platforms/getting-started-mobile/consent-management/)。

* [Android用同意マネージャー](/ja/platforms/android-kotlin/consent-management/)
* [iOS用同意マネージャー](/ja/platforms/ios-swift/consent-management/)

## 同意状態

ユーザーの同意状態をコールバック関数として取得するには、[`getConsentStatus()`](/ja/platforms/flutter-v2/api/tealium/#getconsentstatus)メソッドを呼び出します。

以下の例では同意状態を取得します：
```dart
Tealium.getConsentStatus()
  .then((status) =&gt; print(&#39;同意状態: $status&#39;));
```

ユーザーの同意状態を構成するには、[`setConsentStatus()`](/ja/platforms/flutter-v2/api/tealium/#setconsentstatus)メソッドを呼び出します。

以下の例では同意を付与します：
```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

## 同意カテゴリ

ユーザーの同意カテゴリを取得するには、[`getConsentCategories()`](/ja/platforms/flutter-v2/api/tealium/#getconsentcategories)メソッドを呼び出します。

以下の例ではユーザーの同意カテゴリを取得します：
```dart
Tealium.getConsentCategories()
  .then((categories) =&gt;
      print(&#39;同意カテゴリ: &#39; &#43; categories.join(&#34;,&#34;)));
```

ユーザーの同意カテゴリを構成するには、[`setConsentCategories()`](/ja/platforms/flutter-v2/api/tealium/#setconsentcategories)メソッドを呼び出し、同意カテゴリのリストを渡します。

以下の例では同意カテゴリを構成します：
```dart
Tealium.setConsentCategories([ConsentCategories.analytics,
    ConsentCategories.email]);
```