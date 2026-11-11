---
title: 同意管理
description: モバイル向けの同意管理機能について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/
---

Tealiumの同意管理は、モバイルアプリに同意およびデータプライバシーのサポートを追加します。また、ユーザーに同意を求め、選択内容を保持し、トラッキング動作全体でその選択を尊重する機能も追加します。

同意マネージャーの動作は、アプリユーザーの地域に基づく同意ポリシーによって制御されます。

## 同意ポリシー

Tealium同意マネージャーは、複数の規制要件をサポートするように設計されており、新たな要件が登場した場合にも対応できるようになっています。これらのポリシーは、初期化時に`TealiumConfig`の`consentPolicy`プロパティを構成することで構成します。

### GDPR

タグ管理およびイベントストリーミングでは、デフォルトポリシーとして一般データ保護規則（GDPR）をサポートしています。

| 同意ステータス | 説明 |
| :-- | :-- |
| **未構成**（デフォルト）| 同意ステータスが構成されるまで、トラッキング呼び出しはローカルでキューに追加されます。 |
| **同意済み** | トラッキング呼び出しが送信されます。<br>すべてのトラッキング呼び出しに同意カテゴリが含まれます。<br>同意ログが有効な場合、`grant_consent`イベントが送信されます。 |
| **拒否済み** | トラッキング呼び出しは送信されません。<br>同意ログが有効な場合、`decline_consent`イベントが送信されます。 |

### CCPA

タグ管理では、カリフォルニア州消費者プライバシー法（CCPA）ポリシーをサポートしています。

| 同意ステータス | 説明 |
| :-- | :-- |
| **未構成**（デフォルト）| トラッキング呼び出しが送信されます。<br>[`do_not_sell`](#data-layer)フラグが`false`に構成されます。<br>タグには影響しません。 |
| **同意済み** | トラッキング呼び出しが送信されます。<br>[`do_not_sell`](#data-layer)フラグが`false`に構成されます。<br>タグには影響しません。 |
| **拒否済み** | トラッキング呼び出しが送信されます。<br>[`do_not_sell`](#data-layer)フラグが`true`に構成されます。<br>[CCPA同意マネージャー](https://docs.tealium.com/ja/consent/client-side/consent-management/privacy-banner-and-popup/manage/)の「影響を受けるタグ」セクションで構成されたタグはトリガーされません。 |

## 使用可能なアクション

同意管理モジュールでは、以下のアクションを使用できます。

* 同意ステータスの構成
* ユーザーの同意カテゴリの構成
* ユーザーの同意構成のリセット
* 同意ログの有効化構成
* 同意ポリシーの構成
* 同意ポリシーの取得

## サポート対象プラットフォーム

以下のライブラリがサポートされています。

* [Android（Java）](https://docs.tealium.com/ja/platforms/android-java/consent-management/) - ライブラリに含まれており、初期化時にネイティブコードで有効になります。
* [Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/) - ライブラリに含まれており、初期化時にネイティブコードで有効になります。
* [Cordova](https://docs.tealium.com/ja/platforms/cordova/)
* [iOS（Objective-C）](https://docs.tealium.com/ja/platforms/ios-objective-c/consent-management/) - CocoaPodsフレームワークのビルドに含まれています。
* [iOS（Swift）](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/) - `ConsentManager`モジュールをPodfileに追加すると、CarthageおよびCocoaPodsフレームワークのビルドに含まれ、有効になります。
* [React Native](https://docs.tealium.com/ja/platforms/react-native/)
* [Xamarin](https://docs.tealium.com/ja/platforms/xamarin/consent-mangagement/)

機能の詳細な比較については、[モバイル機能の比較](https://docs.tealium.com/mobile-feature-comparison/)を参照してください。

## データレイヤー

同意管理モジュールの使用時には、トラッキング呼び出しごとに以下のデータレイヤー変数が含まれます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `policy` | 同意の収集に適用されたポリシー（デフォルト：`gdpr`） | `gdpr`または`ccpa` |
| `consent_status` | ユーザーの現在の同意ステータス | `consented`または`notConsented` |
| `consent_categories` | ユーザーが選択した同意カテゴリの配列 | `["analytics", "cdp"]` |
| `do_not_sell` | CCPA同意ポリシーが有効な場合にのみ構成されます | `true`または`false` |