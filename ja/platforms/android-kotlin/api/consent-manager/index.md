---
title: ConsentManager
description: TealiumがAndroid（Kotlin）向けに提供するConsentManagerクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-manager/
---
## クラス: `ConsentManager`

以下は、Kotlinの`ConsentManager`クラスの一般的に使用されるメソッドをまとめたものです。詳細は[Consent Management](https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/)を参照してください。

| メソッド | 説明 |
| ----- | ------ |
| [`isConsentLoggingEnabled`](#isconsentloggingenabled) | 同意の構成変更をログに記録するかどうかを取得/構成します |
| [`policy`](#policy) | 現在適用されているポリシーを取得します（null可） |
| [`reset()`](#reset) | Consent StatusとCategoriesをデフォルト値にリセットします |
| [`userConsentCategories`](#userconsentcategories) | 現在同意されている`ConsentCategory`のセットを取得/構成します |
| [`userConsentStatus`](#userconsentstatus) | 現在のユーザー`ConsentStatus`を取得/構成します |

### `isConsentLoggingEnabled`

ユーザーの同意構成の変更をログに記録するかどうかを取得または構成します。[TealiumConfig.consentManagerLoggingEnabled](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerloggingenabled)オプションで初期化されます。

```java
tealium.consentManager.isConsentLoggingEnabled // 例: false
```

### `policy`

現在使用中の`ConsentPolicy`を返します。[TealiumConfig.consentManagerPolicy](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy)オプションで初期化され、`null`に構成することも可能です。

```java
val policy = tealium.consentManager.policy // 例: ConsentPolicy.GDPR
```

### `reset()`

提供された`userConsentStatus`と`userConsentCategories`をそれぞれデフォルト値の`ConsentStatus.UNKNOWN`と`null`に戻します。

```java
tealium.consentManager.reset()
```



### `userConsentCategories`

アプリユーザーによって付与された現在のConsent Statusを構成または取得します。[利用可能なオプション](https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-category/)について詳しくはこちらをご覧ください。

```java
tealium.consentManager.userConsentCategories = setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)

val categories = tealium.consentManager.userConsentCategories
// setOf(ConsentCategory.CDP, ConsentCategory.EMAIL)を返します
```

### `userConsentStatus`

アプリユーザーによって付与された現在の同意ステータスを構成または取得します。利用可能なオプションは次のとおりです：`UNKOWN`、`CONSENTED`、`NOT_CONSENTED`

```java
tealium.consentManager.userConsentPreferences = ConsentStatus.CONSENTED

val status = tealium.consentManager.userConsentStatus // ConsentStatus.CONSENTEDを返します
```

## インターフェース: `UserConsentPreferencesUpdatedListener`

`UserConsentPreferencesUpdatedListener`はリスナーインターフェースです。`UserConsentPreferences`と`ConsentPolicy`の最新バージョンの更新を受け取るために登録します。

| メソッド | 説明 |
| ----- | ------ |
| [`onUserConsentPreferencesUpdated()`](#onuserconsentpreferencesupdated) | 同意の構成変更をログに記録するかどうかを取得または構成します |

### `onUserConsentPreferencesUpdated()`

同意の構成変更をログに記録するかどうかを取得または構成します。インターフェースを実装するクラスでメソッドを実装するか、`Tealium`インスタンスを作成した後に匿名オブジェクトを渡します。

```java
onUserConsentPreferencesUpdated(userConsentPreferences:policy:)
```

| パラメータ   | タイプ     | 説明     |
| ------------ | -------- | --------------- |
| `userConsentPreferences` | `UserConsentPreferences` | ユーザーの同意構成  |
| `policy` | `ConsentManagementPolicy` | 同意管理ポリシー |

例:

```java
val tealium = Tealium.create(...) {
    events.subscribe(object : UserConsentPreferencesUpdatedListener {
        override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences,
            policy: ConsentManagementPolicy) {
            Logger.dev(BuildConfig.TAG, "同意構成が更新されました")

            }
        )}
    )
}
```

