---
title: Firebaseディスパッチャー
description: Firebaseディスパッチャーモジュールを使用して、Tealium PrismイベントをiOSおよびAndroidのFirebase Analyticsに送信します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/firebase-dispatcher/
---
Firebaseディスパッチャーは、イベントをデバイス上のFirebase Analytics SDKに転送するTealium Prismモジュールです。Prismでイベントを一度トラッキングすると、ディスパッチャーがネイティブのFirebase APIを呼び出します。データレイヤーからFirebaseのイベント、パラメータ、ユーザープロパティ、同意構成へのマッピングは、Tealiumモバイルプロファイルで構成します。

## 要件

Firebaseディスパッチャーには、以下が必要です。

| 要件 | iOS | Android |
| :--- | :--- | :--- |
| オペレーティングシステム | iOS 15以降、macOS 10.15以降、またはtvOS 15以降 | Android API 23以降 |
| Tealium Prism | 0.7.0以降 | 0.7.0以降 |
| Firebase SDK | Firebase iOS SDK 12.x（FirebaseAnalytics） | Firebase Android BoM 34.6.0以降（firebase-analytics） |
| Firebaseプロジェクトファイル | アプリターゲット内の`GoogleService-Info.plist` | アプリモジュール内の`google-services.json`および`com.google.gms.google-services`プラグイン |
| Kotlin | 該当なし | 2.0以降 |

## モジュールの追加

1. Tealiumモバイルプロファイルで、**モジュール**に移動し、**Firebase**モジュールを追加します。
1. モジュール構成を指定します。各構成は省略可能です。省略した場合は、Firebase独自のデフォルトが適用されます。
1. データレイヤー変数からFirebaseの送信先へのマッピングを追加します。[データマッピング](#data-mappings)を参照してください。
1. 必要に応じて、ロードルールを使用してモジュールを制限します。詳しくは、[ルール](https://docs.tealium.com/ja/platforms/prism-mobile/rules/)を参照してください。
1. モバイル構成を保存してパブリッシュします。SDKは起動時およびリモート構成が更新されるたびに、パブリッシュ済みファイルを取得します。[モバイル構成のパブリッシュ](https://docs.tealium.com/publish-mobile-settings/)を参照してください。

### 構成

| 構成 | 構成キー | 型 | 説明 |
| :--- | :--- | :--- | :--- |
| セッションタイムアウト | `session_timeout_seconds` | 数値 | Firebaseのセッションタイムアウト（秒）。 |
| Analytics収集の有効化 | `analytics_collection_enabled` | ブール値 | Firebase Analyticsによる収集をオンまたはオフにします。 |
| ログレベル | `log_level` | 文字列 | （iOSのみ）`min`、`error`、`warning`、`notice`、`info`、`debug`、`max`のいずれか。 |

`session_timeout_seconds`と`analytics_collection_enabled`はコマンドとしても使用できます。モジュール構成は、モジュールの起動時、およびSDKが更新された構成を取得するたびに適用されます。対応するコマンドは、イベント発生時に適用されます。

## データマッピング

マッピングは、データレイヤー変数をFirebaseコマンドペイロード内の送信先にコピーします。次のマッピングでは、`tealium_event`が`purchase`の場合に`logevent`を実行し、イベント名をFirebaseイベント名として使用し、`order_total`をFirebaseの`value`パラメータとして送信します。

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

使用可能なマッピングは次のとおりです。

### Firebase構成

| 送信先 | 型 |
|:---------|:-----|
| `session_timeout_seconds` | 文字列形式の整数 |
| `analytics_collection_enabled` | 文字列形式のブール値 |

### 標準

| 送信先 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `parameters.achievement_id` | `String` | 実績ID |
| `parameters.aclid` | `String` | 広告ネットワーククリックID |
| `parameters.affiliation` | `String` | 提携先 |
| `parameters.cp1` | `String` | CP1 |
| `parameters.campaign` | `String` | キャンペーン |
| `parameters.character` | `String` | キャラクター |
| `parameters.content` | `String` | コンテンツ |
| `parameters.content_type` | `String` | コンテンツタイプ |
| `parameters.coupon` | `String` | クーポン |
| `parameters.creative_name` | `String` | クリエイティブ名 |
| `parameters.creative_slot` | `String` | クリエイティブスロット |
| `parameters.currency` | `String` | 通貨 |
| `parameters.destination` | `String` | 目的地 |
| `parameters.end_date` | `String` | 終了日 |
| `parameters.flight_number` | `String` | フライト番号 |
| `parameters.group_id` | `String` | グループID |
| `parameters.index` | `Long` | インデックス |
| `parameters.item_brand` | `String` | アイテムのブランド |
| `parameters.item_category` | `String` | アイテムのカテゴリー |
| `parameters.item_id` | `String` | アイテムID |
| `parameters.item_name` | `String` | アイテム名 |
| `parameters.item_variant` | `String` | アイテムのバリエーション |
| `parameters.level` | `Long` | レベル |
| `parameters.location` | `String` | 場所 |
| `parameters.medium` | `String` | メディア |
| `parameters.number_of_nights` | `Long` | 宿泊数 |
| `parameters.number_of_passengers` | `Long` | 乗客数 |
| `parameters.number_of_rooms` | `Long` | 部屋数 |
| `parameters.origin` | `String` | 出発地 |
| `parameters.price` | `Double` | 価格 |
| `parameters.quantity` | `Long` | 数量 |
| `parameters.screen_name` | `String` | 画面名 |
| `parameters.screen_class` | `String` | 画面クラス |
| `parameters.score` | `Long` | スコア |
| `parameters.search_term` | `String` | 検索語句 |
| `parameters.shipping` | `Double` | 送料 |
| `parameters.method` | `String` | 方法 |
| `parameters.source` | `String` | ソース |
| `parameters.travel_class` | `String` | 座席クラス |
| `parameters.virtual_currency_name` | `String` | 仮想通貨名 |
| `parameters.start_date` | `String` | 開始日 |
| `parameters.term` | `String` | キーワード |
| `parameters.tax` | `Double` | 税額 |
| `parameters.transaction_id` | `String` | トランザクションID |
| `parameters.value` | `Long or Double` | 値 |
| `parameters.level_name` | `String` | レベル名 |
| `parameters.success` | `Long` | 成功 |
| `parameters.ad_format` | `String` | 広告フォーマット |
| `parameters.ad_platform` | `String` | 広告プラットフォーム |
| `parameters.ad_source` | `String` | 広告ソース |
| `parameters.ad_unit_name` | `String` | 広告ユニット名 |
| `parameters.campaign_id` | `String` | キャンペーンID |
| `parameters.creative_format` | `String` | クリエイティブフォーマット |
| `parameters.discount` | `Double` | 割引額 |
| `parameters.extend_session` | `String` | セッション延長 |
| `parameters.item_category2` | `String` | アイテムカテゴリー2 |
| `parameters.item_category3` | `String` | アイテムカテゴリー3 |
| `parameters.item_category4` | `String` | アイテムカテゴリー4 |
| `parameters.item_category5` | `String` | アイテムカテゴリー5 |
| `parameters.item_list_id` | `String` | アイテムリストID |
| `parameters.item_list_name` | `String` | アイテムリスト名 |
| `parameters.items` | `Array` | アイテム |
| `parameters.location_id` | `String` | 場所ID |
| `parameters.marketing_tactic` | `String` | マーケティング施策 |
| `parameters.payment_type` | `String` | 支払い方法 |
| `parameters.promotion_id` | `String` | プロモーションID |
| `parameters.promotion_name` | `String` | プロモーション名 |
| `parameters.shipping_tier` | `String` | 配送区分 |
| `parameters.source_platform` | `String` | ソースプラットフォーム |
| `email_address` | `String` | メールアドレス |
| `phone_number` | `String` | 電話番号 |
| `hashed_email_address` | `String` | ハッシュ化されたメールアドレス |
| `hashed_phone_number` | `String` | ハッシュ化された電話番号 |

### Eコマース

| 送信先 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `parameters.transaction_id` | `String` | 注文ID |
| `parameters.value` | `Long or Double` | 注文合計 |
| `parameters.shipping` | `Double` | 送料 |
| `parameters.tax` | `Double` | 税額 |
| `parameters.currency` | `String` | 通貨 |
| `parameters.coupon` | `String` | プロモーションコード |
| `parameters.items.item_id` | `Array` | 製品IDのリスト |
| `parameters.items.item_name` | `Array` | 名前のリスト |
| `parameters.items.item_brand` | `Array` | ブランドのリスト |
| `parameters.items.item_category` | `Array` | カテゴリーのリスト |
| `parameters.items.quantity` | `Array` | 数量のリスト |
| `parameters.items.price` | `Array` | 価格のリスト |
| `parameters.items.item_list_name` | `Array` | 表示リストの一覧 |
| `parameters.items.item_variant` | `Array` | バリエーションのリスト |
| `parameters.items.index` | `Array` | インデックスのリスト |
### 同意構成

| 送信先 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `consent_settings.ad_storage` | `String` | 広告保存 |
| `consent_settings.analytics_storage` | `String` | アナリティクス保存 |
| `consent_settings.ad_user_data` | `String` | 広告ユーザーデータ |
| `consent_settings.ad_personalization` | `String` | 広告のパーソナライゼーション |


## コードでのインストール


<blockquote>
モバイルプロファイルに Firebase モジュールを追加する場合は、インストールと初期化の手順を省略してください。詳細については、[モジュールの追加](#add-the-module)を参照してください。
</blockquote>




まだ追加していない場合は、Tealium Maven リポジトリを `settings.gradle.kts` に追加します。

```kotlin
pluginManagement {
    repositories {
        google()
        gradlePluginPortal()
        mavenCentral()
    }
}

dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://maven.tealiumiq.com/android/releases/") }
    }
}
```

ディスパッチャーと Firebase Analytics をアプリモジュールの `build.gradle.kts` に追加します。Firebase SDK のバージョンを管理できるように、`firebase-analytics` は明示的に宣言してください。

```kotlin
plugins {
    id("com.google.gms.google-services") version "4.4.2"
}

dependencies {
    implementation("com.tealium.prism:firebase:0.2.0")
    implementation(platform("com.google.firebase:firebase-bom:34.6.0"))
    implementation("com.google.firebase:firebase-analytics")
}
```

`prism-core` は推移的依存関係として含まれます。



Swift Package Manager を使用してインストールするには、次の手順を実行します。

1. Xcode で、**File > Add Package Dependencies** を選択します。
1. リポジトリ URL として `https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher` を入力します。
1. **Up to next major** を選択し、`TealiumPrismFirebase` プロダクトをアプリターゲットに追加します。

または、パッケージを `Package.swift` に追加します。

```swift
.package(url: "https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher.git", from: "0.2.0")
```

CocoaPods を使用してインストールするには、Podfile に次の行を追加します。

```ruby
pod 'TealiumPrismFirebase'
```

このパッケージは `TealiumPrismCore` と `FirebaseAnalytics` に依存しています。Firebase SDK を別途追加しないでください。



## コードでの初期化


<blockquote>
モバイルプロファイルに Firebase モジュールを追加する場合は、インストールと初期化の手順を省略してください。詳細については、[モジュールの追加](#add-the-module)を参照してください。
</blockquote>


ディスパッチャーが Firebase を初期化します。デバイスがオフラインの場合、Firebase SDK はイベントをキューに格納し、接続が復旧したときに送信します。

アプリでコードによってモジュールを構成する場合は、`TealiumConfig` の `modules` リストにモジュールを追加します。



`firebase-analytics` コンテンツプロバイダーは、起動時に Firebase を初期化します。

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig
import com.tealium.prism.core.api.Modules
import com.tealium.prism.core.api.misc.Environment
import com.tealium.prism.firebase.firebase

val config = TealiumConfig.Builder(
    application = this,
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.collect(),
        Modules.firebase()
    )
)
    .setSettingsUrl("https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
    .build()
val tealium = Tealium.create(config)
```



ディスパッチャーは初回使用時に `FirebaseApp.configure()` を呼び出します。アプリですでに呼び出している場合は、この処理を省略します。

```swift
import TealiumPrismCore
import TealiumPrismFirebase

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.collect(),
                            Modules.firebaseDispatcher()
                           ],
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
let tealium = Tealium.create(config: config)
```



リモートからの変更で上書きされないように構成を固定するには、ビルダークロージャを渡します。詳細については、[詳細構成](https://docs.tealium.com/about-prism-mobile/#advanced-configuration)を参照してください。



```kotlin
Modules.firebase { builder ->
    builder.setAnalyticsEnabled(true)
}
```


```swift
Modules.firebaseDispatcher { builder in
    builder.setAnalyticsEnabled(true)
}
```



## イベント

Firebase イベントをトリガーするには、モバイルプロファイルの Firebase モジュールでデータマッピングを使用し、`tealium_event` の値を対応する Firebase イベント名にマッピングします。たとえば、次のマッピングでは、`tealium_event="purchase"` の場合に `purchase` と `logEvent` の Firebase イベントがトリガーされます。

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

### `initiateconversionmeasurement`

| | |
| :--- | :--- |
| iOS メソッド | `initiateOnDeviceConversionMeasurement()` |
| Android メソッド | 該当なし |
| 送信先 | `hashed_email_address`, `hashed_phone_number`, `email_address`, `phone_number` |
| 注記 | iOS のみ。少なくとも 1 つの送信先が必要です。複数がマッピングされている場合、記載順で最初の送信先のみが使用されます。 |
{class="dt--pivot"}

### `logevent`

| | |
| :--- | :--- |
| iOS メソッド | `logEvent()` |
| Android メソッド | `logEvent()` |
| 送信先 | `event_name`, `parameters`, `parameters.<param>`, `parameters.items.<param>` |
| 注記 | `event_name` は必須です。その他の送信先はすべて任意です。項目をマッピングするには、並列配列（たとえば `product_id` と `product_price`）または `parameters.items.<param>` を持つオブジェクトの配列を使用します。スカラーは単一要素の配列として扱われます。並列配列を使用する場合、`items` 配下のすべての配列は同じ長さである必要があります。長さが異なる場合、コマンドは `arrayLengthMismatch` で失敗します。項目内の null 値は削除され、値が一つも残らなかった項目は項目全体が削除されます。 |
{class="dt--pivot"}

### `resetdata`

| | |
| :--- | :--- |
| iOS メソッド | `resetAnalyticsData()` |
| Android メソッド | `resetAnalyticsData()` |
| 送信先 | なし |
| 注記 | アナリティクスデータを消去し、アプリインスタンス ID をリセットします。 |
{class="dt--pivot"}

### `setanalyticscollectionenabled`

| | |
| :--- | :--- |
| iOS メソッド | `setAnalyticsCollectionEnabled()` |
| Android メソッド | `setAnalyticsCollectionEnabled()` |
| 送信先 | `analytics_collection_enabled` |
| 注記 | 以前に収集されたデータは保持されます。 |
{class="dt--pivot"}

### `setconsent`

| | |
| :--- | :--- |
| iOS メソッド | `setConsent()` |
| Android メソッド | `setConsent()` |
| 送信先 | `consent_settings`, `consent_settings.ad_storage`, `consent_settings.analytics_storage`, `consent_settings.ad_user_data`, `consent_settings.ad_personalization` |
| 注記 | 各値は `granted` または `denied` である必要があります。ペイロードに含まれるタイプのみが更新されます。その他のタイプは以前のステータスを維持します。 |
{class="dt--pivot"}

### `setdefaultparameters`

| | |
| :--- | :--- |
| iOS メソッド | `setDefaultEventParameters()` |
| Android メソッド | `setDefaultEventParameters()` |
| 送信先 | `parameters`, `parameters.<param>` |
| 注記 | パラメータは既存のデフォルト値にマージされ、同じ名前のパラメータは置き換えられます。すべてのデフォルト値を消去するには、`parameters` 全体を省略します。空の `parameters` オブジェクトでは何も実行されず、現在のデフォルト値がそのまま維持されます。 |
{class="dt--pivot"}

### `setsessiontimeout`

| | |
| :--- | :--- |
| iOS メソッド | `setSessionTimeoutInterval()` |
| Android メソッド | `setSessionTimeoutDuration()` |
| 送信先 | `session_timeout_seconds` |
| 注記 | 常に秒単位でマッピングされます。Android では内部的にミリ秒へ変換されます。 |
{class="dt--pivot"}

### `setuserid`

| | |
| :--- | :--- |
| iOS メソッド | `setUserID()` |
| Android メソッド | `setUserId()` |
| 送信先 | `user_id` |
| 注記 | 空の文字列を指定すると、ユーザー ID が消去されます。 |
{class="dt--pivot"}
### `setuserproperty`

| | |
| :--- | :--- |
| iOSメソッド | `setUserProperty()` |
| Androidメソッド | `setUserProperty()` |
| 送信先 | `property_name`、`property_value` |
| 注記 | どちらの送信先も、文字列または文字列の配列を受け入れます。配列の長さは同じでなければなりません。空の値を指定するとプロパティが削除されます。 |
{class="dt--pivot"}

## 検証

テストデバイスでFirebaseのデバッグモードを有効にしてから、`logevent`にマッピングされるイベントをトラッキングします。イベントは、マッピングされたパラメータとともに数秒以内に**DebugView**に表示されます。

* [Xcodeのデバッグコンソールでイベントを表示する](https://firebase.google.com/docs/analytics/ios/events#view-events-in-xcode-debug-console)（iOS）
* [デバッグログでイベントを表示する](https://firebase.google.com/docs/analytics/android/events#view-events-in-debug-log)（Android）

イベントが表示されない場合は、[Trace](https://docs.tealium.com/platforms/prism-mobile/trace/)を使用して、想定されるデータレイヤー値を伴ってイベントがPrismに到達したことを確認します。

## トラブルシューティング

| 症状 | 原因 | 解決方法 |
| :--- | :--- | :--- |
| DebugViewにイベントが表示されない | リモート構成またはローカル構成に`FirebaseDispatcher`エントリがありません。 | モバイルプロファイルにFirebaseモジュールを追加して公開するか、ローカル構成ファイルを確認します。 |
| イベントはPrismに到達するがFirebaseには到達しない | その`tealium_event`に対して`command_name`を構成するマッピングがありません。 | イベント名のフィルターを指定した`command_name`マッピングを追加します。 |
| 構成が適用されない | ローカル構成、リモート構成、およびプログラムによる構成の間でモジュールIDが異なります。 | すべてのソースの`modules`で同じキーを使用します。 |
| AndroidでFirebaseログが出力されない | `log_level`はiOSでのみ使用できます。 | `adb shell setprop log.tag.FA VERBOSE`を実行します。 |
| 同意コマンドが`invalidParameterType`で失敗する | 同意タイプまたはステータスが許容値のいずれかではありません。 | `ad_storage`、`analytics_storage`、`ad_user_data`、`ad_personalization`のみを`granted`または`denied`にマッピングします（大文字と小文字は区別されません）。それ以外の値があると、コマンド全体が失敗します。 |

### コマンドエラー

コマンドが失敗すると、ディスパッチャーは警告をログに記録し、そのコマンドをスキップして処理を続行します。同じイベントにマッピングした他のコマンドは引き続き実行され、イベントも他のディスパッチャーに到達します。デバイスログで`Command '<name>' failed:`を検索してください。メッセージの文言はiOSとAndroidで若干異なりますが、エラータイプは両方で同じです。

| エラー | 原因 | 解決方法 |
| :--- | :--- | :--- |
| `missingParameter` | コマンドに必要な送信先がマッピングされていません。 | マッピングを追加します。必須項目は、`logevent`では`event_name`、`setuserid`では`user_id`、`setuserproperty`では`property_name`と`property_value`、`setconsent`では`consent_settings`、`setsessiontimeout`では`session_timeout_seconds`、`setanalyticscollectionenabled`では`analytics_collection_enabled`です。 |
| `invalidParameterType` | マッピングされた値の型が正しくない、不明な同意タイプまたはステータスが指定されている、あるいは有効なBase64ではない`hashed_*`値が指定されています。 | コマンド表で型を確認します。同意については、サポートされる4つのタイプのみを`granted`または`denied`にマッピングします。 |
| `arrayLengthMismatch` | `parameters.items`内、または`property_name`と`property_value`の間で、並列配列の長さが異なります。 | 配列の長さを同じにするか、`items`をオブジェクト配列形式に切り替えます。 |
| `commandNotFound` | `map_to`の値がサポートされているコマンド名ではありません。 | コマンド表で確認します。照合では大文字と小文字が区別されず、前後の空白も無視されますが、名前に区切り文字を含めることはできません。たとえば、`set_user_id`ではなく`setuserid`または`SetUserID`を使用します。 |

あまり一般的でないエラーである`emptyParameter`、`emptyArray`、`noValidParameters`は、マッピングされた値が空の場合、またはコマンドでサポートされている送信先が1つもマッピングされていない場合に発生します。

## 制限事項

* `initiateconversionmeasurement`と`log_level`はiOSでのみ使用できます。
* アプリ内で同時に有効にできるFirebaseディスパッチャーは1つだけです。

## リファレンス

* [Prism iOS Firebase APIリファレンス](https://docs.tealium.com/tealium-prism-ios-firebase-dispatcher/)
* [Prism Android Firebase APIリファレンス](https://docs.tealium.com/tealium-prism-android-firebase-dispatcher/)