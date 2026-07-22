---
title: 同意管理
description: モバイル向けの同意管理機能について学びましょう。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/
---
Tealiumの同意管理は、モバイルアプリに同意とデータプライバシーのサポートを追加します。また、ユーザーに同意を求め、その選択を保持し、トラッキングの動作全体でその選択を尊重する機能も追加します。

同意マネージャの動作は、アプリユーザーの地域に基づいた同意ポリシーによって制御されます。

## 同意ポリシー

Tealiumの同意マネージャは、複数の規制要件をサポートするように設計されており、新たに出現するものに対応することも可能です。これらのポリシーは、初期化時に`TealiumConfig`の`consentPolicy`プロパティを構成することで構成されます。

### GDPR

Tealium iQタグ管理とEventStreamは、デフォルトのポリシーとして一般データ保護規則（GDPR）をサポートしています。

| 同意ステータス |  説明 |
| :-- | :-- |
| **未構成** (デフォルト)| 同意ステータスが構成されるまで、トラッキングコールはローカルにキューイングされます。 |
| **同意** | トラッキングコールが送信されます。<br>すべてのトラッキングコールに同意カテゴリが含まれます。<br>同意ログが有効になっている場合、`grant_consent`イベントが送信されます。 |
| **拒否**  | トラッキングコールは送信されません。<br>同意ログが有効になっている場合、`decline_consent`イベントが送信されます。 |

### CCPA

Tealium iQタグ管理は、カリフォルニア消費者プライバシー法（CCPA）ポリシーをサポートしています。

| 同意ステータス |  説明 |
| :-- | :-- |
| **未構成** (デフォルト)| トラッキングコールが送信されます。<br>[`do_not_sell`](#data-layer)フラグは`false`に構成されます。<br>タグは影響を受けません。 |
| **同意** | トラッキングコールが送信されます。<br>[`do_not_sell`](#data-layer)フラグは`false`に構成されます。<br>タグは影響を受けません。 |
| **拒否**  | トラッキングコールが送信されます。<br>[`do_not_sell`](#data-layer)フラグは`true`に構成されます。<br>[CCPA同意マネージャ](https://docs.tealium.com/ja/iq-tag-management/consent-management/privacy-banner-and-popup/manage/)の「影響を受けるタグ」セクションで構成されたタグはトリガーされません。 |

## 利用可能なアクション

以下のアクションは、同意管理モジュールで利用可能です。

 * 同意ステータスの構成
 * ユーザーの同意カテゴリの構成
 * ユーザーの同意構成のリセット
 * 同意ログの有効化の構成
 * 同意ポリシーの構成
 * 同意ポリシーの取得

## サポートされているプラットフォーム

以下のライブラリに対するサポートが提供されています：

* [Android (Java)](https://docs.tealium.com/ja/platforms/android-java/consent-management/) - ライブラリに含まれ、初期化時にネイティブコードで有効化されます。
* [Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/) - ライブラリに含まれ、初期化時にネイティブコードで有効化されます。
* [Cordova](https://docs.tealium.com/ja/platforms/cordova/)
* [iOS (Objective-C)](https://docs.tealium.com/ja/platforms/ios-objective-c/consent-management/) - CocoaPodsフレームワークビルドに含まれています。
* [iOS (Swift)](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/) - `ConsentManager`モジュールがPodfileに追加されたときに、CarthageとCocoaPodsフレームワークビルドで含まれ、有効化されます。
* [React Native](https://docs.tealium.com/ja/platforms/react-native/)
* [Xamarin](https://docs.tealium.com/ja/platforms/xamarin/consent-mangagement/)

全機能の比較については、[モバイル機能比較](https://docs.tealium.com/mobile-feature-comparison/)を参照してください。

## データレイヤー

同意管理モジュールを使用しているときに、各トラッキングコールに含まれるデータレイヤー変数は以下の通りです：

| 変数名 | 説明 | 例  |
| --- | --- | --- |
| `policy` | 同意が収集されたポリシー（デフォルト：`gdpr`） | `gdpr`または`ccpa` |
| `consent_status` | ユーザーの現在の同意ステータス | `consented`または`notConsented` |
| `consent_categories` | ユーザーが選択した同意カテゴリの配列 | `["analytics", "cdp"]` |
| `do_not_sell` | CCPA同意ポリシーがアクティブな場合のみ構成 | `true`または`false` |

