---
title: 同意管理
description: Xamarinの同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/xamarin/consent-mangagement/
---
## 使用法

同意管理は推奨される機能であり、ライブラリに自動的に含まれています。同意を管理するには、同意ポリシーを構成し、ユーザーの同意ステータスと同意の構成を追跡する必要があります。

[同意管理について詳しく学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/).

## サンプルアプリ

Xamarin Consent Managementのサンプルアプリを使用して、ライブラリ、追跡方法、およびベストプラクティスに慣れてください：

[Xamarin Consent Management Sample Appをダウンロード](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleAppConsentMgr)

## 有効化

同意管理機能は、`Tealium.Platform.*.dlls`という名前のDLLに組み込まれたネイティブSDKから来ています。

同意管理を有効にするには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/xamarin/api/#consentpolicy)を初期化するときに`consentPolicy`パラメータを構成します：

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

## 同意ステータス

AndroidとiOSの両方のネイティブSDKと同様に、同意管理が有効になると、新規ユーザーは未知の状態であると想定されます。追跡リクエストは、同意ステータスがオプトインまたはオプトアウトになるまでキューに入れられ、その時点でイベントが送信されるか、それぞれパージされます。

以下の方法を使用してユーザーの同意を管理します：

* [`SetConsentStatus()`](https://docs.tealium.com/ja/platforms/xamarin/api/#setconsentstatus)
* [`GetConsentStatus()`](https://docs.tealium.com/ja/platforms/xamarin/api/#getconsentstatus)
* [`SetConsentCategories()`](https://docs.tealium.com/ja/platforms/xamarin/api/#setconsentcategories)
* [`GetConsentCategories()`](https://docs.tealium.com/ja/platforms/xamarin/api/#getconsentcategories)
* [`SetConsentExpiryListener()`](https://docs.tealium.com/ja/platforms/xamarin/api/#setconsentexpirylistener)

`Tealium.Common.dll`は以下のカテゴリとステータスの列挙を提供します：

* [`Tealium.ConsentManager.ConsentStatus`](https://docs.tealium.com/ja/platforms/xamarin/api/#consentstatus)
* [`Tealium.ConsentManager.ConsentCategory`](https://docs.tealium.com/ja/platforms/xamarin/api/#consentcategory)

