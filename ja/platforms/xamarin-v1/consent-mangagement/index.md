---
title: 同意管理
description: 同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/xamarin-v1/consent-mangagement/
---現在のバージョンについては、[Xamarin 2.x 用 Tealium](/ja/platforms/xamarin/)をご覧ください。

## 使用法

このモジュールの使用は推奨されており、ライブラリに自動的に含まれ、初期化時にネイティブコードで有効になります。AndroidとiOSの両方のプラットフォームがサポートされています。

[同意管理についてもっと学ぶ](/ja/platforms/getting-started-mobile/consent-management/)。

## サンプルアプリ

当社のライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Xamarin 同意管理の[サンプルアプリ](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleAppConsentMgr)をダウンロードしてください。

## 有効化

同意管理機能は、`Tealium.Platform.*.dlls`という名前の二つのネイティブSDKから提供されます。`Tealium.Common.dll`は以下のカテゴリとステータスの列挙型を使用するために提供されます：

*   `Tealium.ConsentManager.ConsentStatus`
*   `Tealium.ConsentManager.ConsentCategory`

同意管理を有効にするには、`TealiumConfig`のコンストラクターにオプションのパラメータを渡すか、次の例に示すようにプロパティとして構成します：

```csharp
TealiumConfig tealConfig = new TealiumConfig(
        TealiumConsts.INSTANCE_ID,
        TealiumConsts.ACCOUNT,
        TealiumConsts.PROFILE,
        TealiumConsts.ENVIRONMENT,
        true,
        commands,
        advConfig,
        false); // オプションの同意管理の有効化

// または後で有効にする:
tealConfig.IsConsentManagerEnabled = true;

// Tealiumインスタンスを初期化します:
var tealium = instanceManager.CreateInstance(tealConfig);
```

## 同意ステータス

AndroidおよびiOSのネイティブSDKと同様に、同意管理が有効になっている場合、新しいユーザーは未知の状態と見なされます。トラッキングリクエストは、同意ステータスがオプトインまたはオプトアウトされるまでキューに入れられ、その時点でイベントが送信されるか、それぞれ破棄されます。

`TealiumConfig`オブジェクトのプロパティを通じて初期ステータスを上書きすることができます。次の例に示すように：

```csharp
// 同意管理を有効にする:
tealConfig.IsConsentManagerEnabled = true;

// ユーザーをデフォルトで同意済みに構成する:
tealConfig.InitialUserConsentStatus = ConsentManager.ConsentStatus.Consented;
// または、ユーザーをデフォルトで未同意に構成する:
tealConfig.InitialUserConsentStatus = ConsentManager.ConsentStatus.NotConsented;

// ユーザーをすべてのカテゴリにオプトインする
tealConfig.InitialUserConsentCategories = ConsentManager.AllCategories;
// またはなし:
tealConfig.InitialUserConsentCategories = ConsentManager.NoCategories;
// または部分的にオプトインする、アナリティクスとモバイルカテゴリのみ。
tealConfig.InitialUserConsentCategories = new ConsentCategory[]{
    ConsentManager.ConsentCategory.Analytics,
        ConsentManager.ConsentCategory.Mobile
};
```

## 同意の選択

`ConsentManager`プロパティを通じてTealiumインスタンスから直接同意管理と対話します。

ユーザーの同意選択を更新する必要がある場合は、`ConsentManager.ConsentCategory`および`ConsentManager.ConsentStatus`で利用可能な列挙値のいずれかを渡します。次の例に示すように：

```csharp
// ユーザーが未知の状態にある場合、次のコードはキューに入れられたイベントがこの後に送信されることをトリガーします:
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
tealium.ConsentManager.UserConsentStatus = ConsentManager.ConsentStatus.Consented;

// これにより、ユーザーはすべてのカテゴリに自動的にオプトインされます。カテゴリが提供されていないためです。
// カテゴリのサブセットに同意してオプトインするには、オーバーロードを使用します:
tealium.ConsentManager.UserConsentStatusWithCategories(ConsentManager.ConsentStatus.Consented, new ConsentCategory[]{
    ConsentManager.ConsentCategory.Analytics
});
```

## リセット

現在選択されている同意構成をリセットする追加オプションが利用可能です。これにより、ユーザーは再び「未知」の状態に戻り、その後のイベントが再びキューに入れられるようになります。

完全に無効にするには、次の例に示すように`TealiumConfig`オブジェクトで無効にします：

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
tealium.ConsentManager.ResetUserConsentPreferences();
```