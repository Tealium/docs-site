---
title: アトリビューションモジュール
description: 各トラッキングコールにユーザーリセット可能な広告識別子（IDFA）を追加し、オプションでApple Search Ads APIを実装してアトリビューション情報を収集します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/attribution/
---
## 使用法

アトリビューションモジュールは、各トラッキングコールにユーザーリセット可能な広告識別子（IDFA）を追加し、オプションでApple Search Ads APIを実装してアトリビューション情報を収集します。[Apple Search Adsアトリビューションの構成](https://developer.apple.com/documentation/iad/setting_up_apple_search_ads_attribution)について詳しく学びましょう。

バージョン2.1.1以降では、アトリビューションモジュールには`SKAdNetwork`のサポートが含まれており、`ATTransparency.AuthorizationStatus`がディスパッチペイロードに追加されます。

このモジュールの使用はオプションです。その機能について読んで、必要かどうかを判断してください。なぜなら、それは追加の依存関係を導入します。あなたはAppleに対して、なぜIDFAを使用しているのかを説明する必要があります。IDFAの使用を明記しない場合、Appleはあなたのアプリを拒否します。[IDFAの使用と拒否](https://developer.apple.com/app-store/review/rejections/)について詳しく学びましょう。

以下のプラットフォームがサポートされています：

* iOS

## 要件

* UIKit
* AdSupport
* iOS 14以降：AppTrackingTransparency
* iOS 14以降：StoreKit

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してアトリビューションモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールする最も簡単で推奨される方法です：

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`"Up to next major"`が推奨されます。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`Attribution`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットに追加します。**Frameworks and Libraries**の下にあります。

[iOS向けのSwift Package Managerのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)について詳しく学びましょう。

### CocoaPods

CocoaPodsでアトリビューションモジュールをインストールするには、以下のpodをPodfileに追加します：  
```perl
pod 'tealium-swift/Attribution'
```

[iOS向けのCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)について詳しく学びましょう。

### Carthage

Carthageでアトリビューションモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。
1. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```perl
      TealiumAttribution.framework
      ```

[iOS向けのCarthageのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)について詳しく学びましょう。

## 初期化

モジュールを初期化するには、[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに含めます。

```swift
config.collectors = [Collectors.Attribution]
```


<blockquote>
[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを確認し、必要なコレクターを正しく指定する方法を理解してください。
</blockquote>


## iOS 14+でのアトリビューション

iOS 14以降では、アプリはユーザーの許可を得てデバイスの広告識別子（IDFA）にアクセスする必要があります。アプリが初めて起動するときにユーザーに「トラッキングの許可」を求めるプロンプトが表示されます。ユーザーが拒否すると、IDFAはアプリで利用できません。

IDFAが利用できない場合、`SKAdNetwork`は登録された広告ネットワークがアプリのインストールをキャンペーンにアトリビュートするための方法を提供します。これは、Appleから直接署名された信号を受け取ることによって行われます。広告ネットワークは、アプリが正常にインストールされたこと、キャンペーンID、およびオプションのコンバージョン値を受け取ります。

`AppTrackingTransparency`と`SKAdNetwork`フレームワークについては、[Consent and the Apple IDFA (Identifier for Advertisers)](https://docs.tealium.com/ja/platforms/getting-started-mobile/idfa/)で詳しく学びましょう。

### AppTrackingTransparency (ATT)

アトリビューションモジュールが有効になっていると、ユーザーのトラッキング認証ステータスが自動的にディスパッチペイロードに`device_tracking_authorization`として追加され、その値は[`ATTrackingManager.AuthorizationStatus`](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus)列挙型の文字列表現です。

該当する場合は、`ATTrackingManager.requestTrackingAuthorization`を別途呼び出します。[Tealium SDKを有効にするためのトラッキング認証のリクエスト](https://docs.tealium.com/ja/platforms/getting-started-mobile/idfa/)について詳しく学びましょう。

### SKAdNetwork

Tealiumは、`config.skAdAttributionEnabled`が`true`に構成されている場合、起動時に自動的に`SKAdNetwork.registerAppForAdNetworkAttribution()`を呼び出します。これにより、広告ネットワークはアプリのインストールを匿名で検証することができます。`config.skAdConversionKeys`辞書が定義されている場合、指定されたイベントで自動的に`SKAdNetwork.updateConversionValue()`が呼び出され、指定されたコンバージョンキーの値が送信されます。

```swift
config.skAdConversionKeys = ["EVENT_NAME": "DATA_LAYER_VARIABLE"]
```

コンバージョン値は、`0`から`63`までの値を持つ`Int`でなければなりません。コンバージョン値が小数の場合、コンバージョンイベントを呼び出す前に整数に変換する必要があります。

例えば：

```swift
config.skAdConversionKeys = ["purchase": "conversion_value"]
...
tealium?.track("purchase", dataLayer: ["order_subtotal": 456.87, "conversion_value": conversionValue])
```

[`SKAdNetwork`フレームワーク](https://docs.tealium.com/ja/platforms/getting-started-mobile/idfa/)について詳しく学びましょう。 <!-- blog -->

#### プロセス

以下の図は、広告のインストール検証のパスを示しています。App Aは広告を表示するソースアプリで、App Bはユーザーがインストールする広告アプリです。

![](https://docs.tealium.com/images/platforms/ios/skad-custom.png)

ユーザーがアプリ内またはモバイルウェブブラウザ内の広告をクリックすると、App Storeが起動し、ユーザーは広告キャンペーンの製品画面に移動します。iOS 14.5以降では、広告主はカスタムビュースルーアドまたはStoreKitレンダリングアドを表示するかどうかを選択するオプションがあります。ユーザーが広告アプリをインストールすると、デバイスは保留中のインストール検証を保存します。ユーザーがアトリビューションタイムウィンドウ内にアプリを開くと、デバイスはインストール検証のポストバックを広告ネットワークに送信します。

通知はAppleによって署名され、キャンペーンIDを含みますが、ユーザーまたはデバイス固有のデータは除外されます。ポストバックには、Appleが値の提供がAppleのプライバシー閾値を満たすと判断した場合、コンバージョン値とソースアプリのIDが含まれる場合があります。

[広告主導のアプリインストール](https://developer.apple.com/documentation/storekit/skadnetwork)について詳しく学びましょう。

#### Tealiumの役割

Appleの`SKAdNetwork`ソリューションには3つの主要な関係者がいます：

* 広告ネットワーク
* ソースアプリ
* 広告アプリ

Tealiumは`SKAdNetwork`への呼び出しをラップします。`TealiumAttribution`モジュールと構成フラグが有効になっている場合、アプリの起動時に`SKAdNetwork.registerAppForAdNetworkAttribution()`が呼び出されます。

さらに、[`skAdConversionKeys`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#skadconversionkeys)を定義している場合、`SKAdNetwork.updateConversionValue(_:)`メソッドが呼び出され、指定されたコンバージョン値が渡されます。Tealiumは、既に設置しているトラッキングを通じて`SKAdNetwork`への呼び出しを管理することを可能にします。


<blockquote>
ユーザーからトラッキング認証をリクエストし、適切なキーを`.plist`ファイルに追加する必要があるかもしれません。
</blockquote>


次の図は、Tealiumが`SKAdNetwork`とどのように連携するかを示しています：
![](https://docs.tealium.com/images/platforms/ios/skad-tealium-custom.png)

#### 検証

[`SKAdNetwork`](https://developer.apple.com/documentation/storekit/skadnetwork/verifying_an_install_validation_postback)への呼び出しの検証について学びましょう。

## Search Ads API

Apple Search Ads APIを使用するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#tealiumconfig)オブジェクトの[`searchAdsEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#searchadsenabled)プロパティを有効にします。次に、[`AAAttribution`](https://developer.apple.com/documentation/adservices/aaattribution)クラスを使用して、アトリビューションオブジェクトを取得するためのトークンを取得します。Tealiumライブラリはアプリの起動時にこれを行いますが、情報がタイムリーに取得されない可能性があります。Appleから受け取った情報は、通常は起動イベント中にデータレイヤーに追加されます。

場合によっては、起動後にいくつかのイベントが発生することがあります。これらの変数は、アプリのライフタイム中に一度だけAppleのサーバーから取得され、永続的な変数として保存されるため、将来のアプリの起動時に利用可能になります。

### iAdフレームワークからAdServicesフレームワークへ

iOS 14.3以降、Appleは`iAd`フレームワークを非推奨とし、新しい`AdServices`を推奨しています。

* [`iAd`](https://developer.apple.com/documentation/iad)フレームワークは、同じタイプのアトリビューションデータを返しましたが、詳細な情報はATTを通じて同意したユーザーにのみ提供されました。
* 新しい[`AdServices`](https://developer.apple.com/documentation/adservices)フレームワークは詳細度は低いですが、すべてのユーザーにアトリビューションデータを提供します。

TealiumSwift SDKのバージョン2.9.0では、新しいアトリビューションモジュールを含め、iOS 14.3以降では新しい`AdServices`を使用します。

2023年2月7日、Appleは旧`iAd`フレームワークの公式サポートを終了し、近日中にiOSから削除されると発表し、開発者に対してすべてのアプリとSDKから依存関係を削除するよう勧告しました。

TealiumSwift SDKのバージョン2.11.0では、Appleがサポートを終了したため、`iAd`フレームワークを完全に削除しました。今後は新しい`AdServices`フレームワークのみを使用します。

お客様に対するサービスの中断を避けるため、`AdServices`に含まれるすべてのデータは、旧`iAd`フレームワークの同じデータレイヤー変数にマッピングされます。
Appleから返されなくなった`iAd`のアトリビューションキーの一部を非推奨とします。`iAd`フレームワークが最終的にシャットダウンされる前にユーザーがそれらを受け取った場合、そのデータを引き続き受け取ることができますが、新規インストールには適用されません。

### 必要なアクション

お客様に必要なアクションは、TealiumSwift SDKのバージョン2.11.0以降に更新することだけです。このアクションにより、`iAd`フレームワークがアプリから削除され、新規インストールでは非推奨のアトリビューションキーのみをデータレイヤーから使用することが保証されます。非推奨のキーは空になります。

## データレイヤー

モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：


<blockquote>
`ad_`で始まる変数は、[Search Ads](#search-ads-api)が有効になっている場合にのみ構成されます。
</blockquote>


| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `ad_campaign_id` | 対応する広告のキャンペーンID。 | `1234567890` |
| `ad_campaign_name` (非推奨) |  対応する広告のキャンペーン名。 | `CampaignName` |
| `ad_creativeset_id` (非推奨) | 対応する広告が一部であったクリエイティブセットのID。 | `456093` |
| `ad_creativeset_name` (非推奨) | 対応する広告が一部であったクリエイティブセットの名前。| `Beast Images` |
| `ad_group_id` |  対応する広告のキャンペーングループID。| `1234567890` |
| `ad_group_name` (非推奨) |  対応する広告のキャンペーングループ名。| `AdGroupName` |
| `ad_keyword` | `iAd`からのキーワードまたは`AdServices`からのkeywordId。 | `1234567890` |
| `ad_keyword_matchtype` (非推奨) | これはBroad、Exact、またはSearch Matchのいずれかである可能性があります。 | `Exact` |
| `ad_id` |  広告オブジェクトと広告グループの間の割り当て関係を表す識別子（iOS 15.2以降のみ）。 | `AdID` |
| `ad_org_id` |  対応する広告のキャンペーン組織ID。| `OrgID` |
| `ad_org_name` (非推奨) |  対応する広告のキャンペーン組織名。 | `OrgName` |
| `ad_purchase_date` (非推奨) | ユーザーが初めてアプリをダウンロードした日時。`iadconversion-type = "Redownload"`の場合、これは元の購入日を表します。このパラメータはApple Search Adに関連付けられていたかもしれませんし、そうでないかもしれません。| `2016-12-05T17:31:40Z` |
| `ad_region` | このインストールを駆動したキャンペーンに関連する国または地域を識別します。 | `US` |
| `ad_user_clicked_last_30_days` | ユーザーがアプリをダウンロードする30日前にSearch Adsのインプレッションをクリックしたかどうかを示すブール値。 | `true` |
| `ad_user_conversion_type` | アプリの新規ダウンロードまたは再ダウンロードを識別します。| `Download` |
| `ad_user_date_clicked` | ユーザーが対応する広告をクリックした日時。| `2016-12-05T17:31:40Z` |
| `ad_user_date_converted` (非推奨) | ユーザーがアプリをダウンロードした日時。| `2016-12-05T17:31:40Z` |
| `device_tracking_authorization` | iOS 14以降のみ。[`ATTrackingManager.AuthorizationStatus`](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus) | [`notDetermined`, `restricted`,  `denied`, `authorized`] |
| `device_advertising_enabled` | ユーザーが広告トラッキングを許可したかどうかを示すブール値（`false`の場合、広告IDはゼロの文字列として表示されます）。| `true` |
| `device_advertising_id` | ユーザーがリセット可能な広告識別子（IDFA）。| `6D92078A-8246...` |
| `device_advertising_vendor_id` | 同一ベンダーからの同一デバイス上のすべてのアプリで同じであることが保証された一意のID（RDNSバンドル識別子の最初の2部分が同じアプリ。例えば、`com.tealium`または`com.acme`。） | `6D92078A-8246...` |
