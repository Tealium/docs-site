---
title: TealiumConsentManager
description: Tealium Consent Managementのためのメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/
---
## クラス: `TealiumConsentManager`

以下は、iOS（Swift）の`TealiumConsentManager`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`onConsentExpiration`](#onconsentexpiration) | 同意選択が期限切れになったときに実行するコールバック |
| [`resetUserConsentPreferences()`](#resetuserconsentpreferences) | メモリと永続保存に現在保存されているすべての同意構成をクリアします |
| [`userConsentStatus`](#userconsentstatus) | ユーザーの同意ステータスを取得または構成します |
| [`userConsentCategories`](#userconsentcategories) | ユーザーの同意カテゴリを取得または構成します |

### `onConsentExpiration`

同意選択が期限切れになったときに実行するコールバック。

```swift
config.onConsentExpiration = {
   // 同意モーダルを表示
}
```

### `userConsentStatus`

現在の同意ステータスを取得または構成します。

```swift
let categories = tealium.consentManager?.userConsentStatus
tealium.consentManager?.userConsentStatus = .consented
```

| パラメータタイプ | 説明 |
| --- | --- |
| `TealiumConsentStatus` | 現在の同意ステータス |

### `resetUserConsentPreferences()`

メモリと永続保存に現在保存されているすべての同意構成をクリアします。カテゴリなしの`&#34;unknown&#34;`同意状態に戻ります。

```swift
resetUserConsentPreferences()
```

### `userConsentCategories`

現在のすべての同意カテゴリを取得または構成します。

```swift
let categories = tealium.consentManager?.userConsentCategories
tealium.consentManager?.userConsentCategories = [.cdp]
```

| パラメータタイプ | 説明 |
| --- | --- |
| `TealiumConsentCategories` | 現在のTealium同意カテゴリ |

