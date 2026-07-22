---
title: TealiumConsentManager
description: Tealium Consent Managementのためのメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-consent-manager/
---
## クラス: `TealiumConsentManager`

以下は、iOS（Swift）の`TealiumInstanceManager`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `addConsentDelegate()` | `TealiumConsentDelegate`プロトコルに準拠した特定のクラスを登録します |
| `getUserConsentCategories()` | 現在のすべての同意カテゴリを返します |
| `getUserConsentPreferences()` | 現在のすべての同意構成を返します|
| `getUserConsentStatus()` |現在の同意ステータスを返します |
| `removeAllConsentDelegates()` | すべての同意デリゲートを削除します |
| `resetUserConsentPreferences()` | メモリと永続保存に現在保存されているすべての同意構成をクリアします |
| `setUserConsentCategories()` | ユーザーの同意カテゴリを構成します |
| `setUserConsentStatus()` | ユーザーの同意ステータスを構成します |
| `setUserConsentStatusWithCategories()` | 同意ステータスとカテゴリを構成します |

### `addConsentDelegate()`

`TealiumConsentDelegate`プロトコルに準拠した特定のクラスを登録します。

```swift
addConsentDelegate(delegate)
```

| パラメータ | タイプ  | 説明 |
| --- | --- | --- |
| `delegate` | `TealiumConsentManagerDelegate` | `TealiumConsentDelegate`に準拠したクラス |

### `getUserConsentCategories()`

現在のすべての同意カテゴリを返します。

```swift
getUserConsentCategories()
```

| 戻り値のタイプ | 説明 |
| --- | --- |
| `TealiumConsentCategories` | 現在のTealium同意カテゴリ |

### `getUserConsentPreferences()`

現在のすべての同意構成を返します。

```swift
getUserConsentPreferences()
```

| 戻り値のタイプ | 説明 |
| --- | --- |
| `TealiumConsentUserPreferences` | 現在のすべての同意構成 |


### `getUserConsentStatus()`

現在の同意ステータスを返します。

```swift
getUserConsentStatus()
```

| 戻り値のタイプ | 説明 |
| --- | --- |
| `TealiumConsentStatus` | 現在の同意ステータス |


### `removeAllConsentDelegates()`

すべての同意デリゲートを削除します。`TealiumConsentManagerModule`クラスによって作成された組み込みデリゲートは保持されます。

```swift
removeAllConsentDelegates()
```

### `resetUserConsentPreferences()`

メモリと永続保存に現在保存されているすべての同意構成をクリアします。同意状態を"unknown"に戻し、カテゴリはありません。

```swift
resetUserConsentPreferences()
```


### `setUserConsentCategories()`

ユーザーの同意カテゴリを構成します。アプリの同意管理構成画面から呼び出すことを想定しています。同意ステータスを`.consented`に構成します。

```swift
setUserConsentCategories(categories)
```

| パラメータ | タイプの説明 | 例 |
| --- | --- | --- |
| `categories` | TealiumConsentCategories enumからの値の配列 | `[.analytics,.bigData]` |

以下の例は、ユーザーの同意カテゴリを`[.analytics,.bigData]`に構成する方法を示しています：

```swift
tealium?.consentManager()?.setUserConsentCategories([.analytics,.bigData])
```


### `setUserConsentStatus()`

ユーザーの同意ステータスを構成します。ユーザーがトラッキングを有効または無効にするときに、アプリの同意管理構成画面から呼び出すことを想定しています。

ステータスが`.consented`の場合、利用可能なすべての同意カテゴリを含むように同意カテゴリのリストを構成します。カテゴリを選択的に構成することはできません。

```swift
setUserConsentStatus(status)
```

| パラメータ | タイプ |  説明 | 例 |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus` | 構成する同意ステータス| [`.unknown`, `.consented`, `.notConsented`] |

以下の例は、ユーザーの同意ステータスを`.consented`に構成する方法を示しています：

```swift
tealium?.consentManager()?.setUserConsentStatus(.consented)
```

以下は、`TealiumConsentStatus` enumからのTealium同意ステータスの異なるタイプを定義しています。

**.unknown**  
`unknown`ステータスは、Consent Managerのデフォルト構成です。この状態では、Consent Managerは、肯定的な`consented`/`notConsented`ステータスが提供されるまで、イベントをローカルにキューに入れます。

**.consented**  
`consented`ステータスは、ユーザーがトラッキングに同意したときに構成されます。この状態では、Consent Managerはすべてのトラッキング呼び出しを通常通りに許可します。

**.notConsented**  
`notConsented`ステータスは、ユーザーがトラッキングを拒否したときに構成されます。この状態では、Consent Managerはすべてのトラッキング呼び出しをドロップし、SDKによるさらなる処理を停止します。



### `setUserConsentStatusWithCategories()`

同意ステータスとカテゴリを構成します。

```swift
setUserConsentStatusWithCategories(status, categories)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus?` | 構成する同意ステータス| [`.unknown`, `.consented`, `.notConsented`] |
| `categories` | `[TealiumConsentCategories]?` | 構成する同意カテゴリ | `[.analytics]` |

以下の例は、ユーザーの同意ステータスを`.consented`に構成し、カテゴリを`.analytics`に構成する方法を示しています：

```swift
tealium?.consentManager()?.setUserConsentStatusWithCategories(status: .consented, categories: [.analytics])
```

