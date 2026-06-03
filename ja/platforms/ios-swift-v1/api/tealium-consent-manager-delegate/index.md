---
title: TealiumConsentManagerDelegate
description: Tealium Consent Management デリゲートのためのメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-consent-manager-delegate/
---
## クラス: `TealiumConsentManagerDelegate`

以下は、iOS（Swift）の `TealiumInstanceManagerDelegate` クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `consentStatusChanged()` | 同意状態が正常に更新されたときに呼び出されます |
| `userChangedConsentCategories()` | ユーザーが同意カテゴリの構成を更新したときに呼び出されます |
| `userConsentedToTracking()` | 同意状態が `.consented` に変更されたときに呼び出されます |
| `userOptedOutOfTracking()` | ユーザーが同意を拒否/取り消したときに呼び出されます |
| `willDropTrackingCall()` | Consent Managerがトラッキングコールをドロップする予定のときに呼び出されます |
| `willQueueTrackingCall()` | Consent Managerが `&#34;unknown&#34;` 状態にあり、ユーザーが同意を与えるか拒否するまでトラッキングコールがローカルでキューに入れられているときに呼び出されます |
| `willSendTrackingCall()` | ユーザーがトラッキングに同意し、トラッキングコールがConsent Managerをブロックせずに通過する予定のときに呼び出されます |

### `consentStatusChanged()`

同意状態が正常に更新されたときに呼び出されます。

```swift
consentStatusChanged(state)
```

| パラメータ   | タイプ    | 説明                    |
|-------------|---------|--------------------------------|
| `state`  | `TealiumConsentStatus`  | 同意状態 |

### `userChangedConsentCategories()`

ユーザーが同意カテゴリの構成を更新したときに呼び出されます。

```swift
userChangedConsentCategories(categories)
    }
```
| パラメータ   | タイプ    | 説明                    |
|-------------|---------|--------------------------------|
| `categories`  | `[TealiumConsentCategories]`  | 同意カテゴリ |

### `userConsentedToTracking()`

同意状態が `.consented` に変更されたときに呼び出されます。

```swift
userConsentedToTracking()
```

### `userOptedOutOfTracking()`

ユーザーが同意を拒否/取り消したとき（同意状態： `.notConsented`）に呼び出されます。

```swift
userOptedOutOfTracking()
```

### `willDropTrackingCall()`

Consent Managerがトラッキングコールをドロップする予定のときに呼び出されます。例えば、ユーザーがトラッキング同意を拒否したときなどです。

```swift
willDropTrackingCall(request)
```
| パラメータ   | タイプ    | 説明                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium トラックリクエスト |


### `willQueueTrackingCall()`

Consent Managerが `&#34;unknown&#34;` 状態にあり、ユーザーが同意を与えるか拒否するまでトラッキングコールがローカルでキューに入れられているときに呼び出されます。

```swift
willQueueTrackingCall(request)
```
| パラメータ   | タイプ    | 説明                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium トラックリクエスト |


### `willSendTrackingCall()`

ユーザーがトラッキングに同意し、トラッキングコールがConsent Managerをブロックせずに通過する予定のときに呼び出されます。

```swift
willSendTrackingCall(request)
```
| パラメータ   | タイプ    | 説明                    |
|-------------|---------|--------------------------------|
| `request`  | `TealiumTrackRequest`  | Tealium トラックリクエスト |

