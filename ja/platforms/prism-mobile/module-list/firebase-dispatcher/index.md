---
title: Firebase ディスパッチャー
description: Firebase ディスパッチャーモジュールを使用して、iOS および Android で Tealium Prism イベントを Firebase Analytics に送信します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/firebase-dispatcher/
---
Firebase ディスパッチャーは、デバイス上の Firebase Analytics SDK にイベントを転送する Tealium Prism モジュールです。Prism でイベントを一度追跡すると、ディスパッチャーはネイティブの Firebase API を呼び出します。Tealium モバイルプロファイルで、データレイヤーから Firebase イベント、パラメータ、ユーザープロパティ、および同意構成へのマッピングを構成します。

## 要件

Firebase ディスパッチャーには以下が必要です：

| 要件 | iOS | Android |
| :--- | :--- | :--- |
| オペレーティングシステム | iOS 15+, macOS 10.15+, または tvOS 15+ | Android API 23+ |
| Tealium Prism | 0.5.0+ | 0.5.0+ |
| Firebase SDK | Firebase iOS SDK 12.x (FirebaseAnalytics) | Firebase Android BoM 34.6.0+ (firebase-analytics) |
| Firebase プロジェクトファイル | アプリターゲット内の `GoogleService-Info.plist` | アプリモジュールと `com.google.gms.google-services` プラグイン内の `google-services.json` |
| Kotlin | N/A | 2.0+ |

## インストール



まだ追加していない場合は、`settings.gradle.kts` に Tealium Maven リポジトリを追加します：

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

アプリモジュールの `build.gradle.kts` にディスパッチャーと Firebase Analytics を追加します。Firebase SDK バージョンを自分で管理するために `firebase-analytics` を自分で宣言します：

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

`prism-core` は推移的に含まれます。



Swift Package Manager でインストールするには：

1. Xcode で **File > Add Package Dependencies** を選択します。
1. リポジトリ URL を入力します：`https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher`.
1. **Up to next major** を選択し、アプリターゲットに `TealiumPrismFirebase` 製品を追加します。

または `Package.swift` にパッケージを追加します：

```swift
.package(url: "https://github.com/Tealium/tealium-prism-ios-firebase-dispatcher.git", from: "0.2.0")
```

CocoaPods でインストールする場合、Podfile に次の行を追加します：

```ruby
pod 'TealiumPrismFirebase'
```

このパッケージは `TealiumPrismCore` と `FirebaseAnalytics` に依存しています。Firebase SDK を別途追加しないでください。



## 初期化

Firebase モジュールを含むリモートまたはローカル構成がある場合、コードは必要ありません。ディスパッチャーはアプリの起動時に自動的に登録され、構成が存在するまで非アクティブのままです。詳細については、[リモートおよびローカル構成](https://docs.tealium.com/platforms/prism-mobile/install/#remote-and-local-settings)を参照してください。

ディスパッチャーは Firebase を自動的に初期化します。iOS では、ディスパッチャーは最初の使用時に `FirebaseApp.configure()` を呼び出し、アプリが既に行っている場合はスキップします。Android では、`firebase-analytics` コンテンツプロバイダーが起動時に Firebase を初期化します。


<blockquote>
デバイスがオフラインの場合、Firebase SDK はイベントをキューに入れ、接続が復旧したときに配信します。
</blockquote>


コードでモジュールを構成する場合、`TealiumConfig` の `modules` リストにモジュールを追加します：



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



リモート変更がそれを上書きできないように構成をロックするには、ビルダークロージャを渡します。詳細については、[高度な構成](https://docs.tealium.com/about-prism-mobile/#advanced-configuration)を参照してください。



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



## モジュールの構成

1. Tealium モバイルプロファイルで **Modules** に移動し、**Firebase** モジュールを追加します。
1. モジュール構成を構成します。各構成はオプションです。省略された場合、Firebase は独自のデフォルトを適用します。
1. データレイヤー変数から Firebase の宛先へのマッピングを追加します。[データマッピング](#data-mappings)を参照してください。
1. 必要に応じて、ロードルールでモジュールを制限します。詳細については、[ルール](https://docs.tealium.com/ja/platforms/prism-mobile/rules/)を参照してください。
1. モバイル構成を保存して公開します。SDK は起動時および各リモート構成の更新時に公開されたファイルを取得します。[モバイル構成の公開](https://docs.tealium.com/publish-mobile-settings/)を参照してください。

| 構成 | 構成キー | タイプ | 説明 |
| :--- | :--- | :--- | :--- |
| セッションタイムアウト | `session_timeout_seconds` | 数値 | Firebase のセッションタイムアウト（秒）。 |
| 分析収集有効 | `analytics_collection_enabled` | ブール値 | Firebase Analytics の収集をオンまたはオフにします。 |
| ログレベル | `log_level` | 文字列 | (iOS のみ) `min`, `error`, `warning`, `notice`, `info`, `debug`, `max` のいずれか。 |

`session_timeout_seconds` と `analytics_collection_enabled` はコマンドとしても利用可能です。モジュール構成はモジュールの開始時および SDK が更新された構成を取得するたびに適用されます。対応するコマンドはイベント時に適用されます。

## データマッピング

マッピングはデータレイヤー変数を Firebase コマンドペイロードの宛先にコピーします。次のマッピングは、`tealium_event` が `purchase` の場合に `logevent` を実行し、イベント名を Firebase イベント名として使用し、`order_total` を Firebase の `value` パラメータとして送信します：

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

利用可能なマッピングは以下の通りです：

### Firebase 構成

| 変数 | タイプ  |
|:---------|:-----|
| `firebase_session_timeout_seconds` | 文字列としての整数 |
| `firebase_analytics_collection_enabled` | 文字列としてのブール値 |
| `firebase_log_level` | 文字列 |




### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `param_achievement_id` | `String` | 実績ID |
| `param_ad_network_click_id` | `String` | 広告ネットワーククリックID |
| `param_affiliation` | `String` | 所属 |
| `param_cp1` | `String` | CP1 |
| `param_campaign` | `String` | キャンペーン |
| `param_character` | `String` | キャラクター |
| `param_content` | `String` | コンテンツ |
| `param_content_type` | `String` | コンテンツタイプ |
| `param_coupon` | `String` | クーポン |
| `param_creative_name` | `String` | クリエイティブ名 |
| `param_creative_slot` | `String` | クリエイティブスロット |
| `param_currency` | `String` | 通貨 |
| `param_destination` | `String` | 目的地 |
| `param_end_date` | `String` | 終了日 |
| `param_flight_number` | `String` | フライト番号 |
| `param_group_id` | `String` | グループID |
| `param_index` | `String` | インデックス |
| `param_item_brand` | `String` | アイテムブランド |
| `param_item_category` | `String` | アイテムカテゴリ |
| `param_item_id` | `String` | アイテムID |
| `param_item_list` | `String` | アイテムリスト |
| `param_item_name` | `String` | アイテム名 |
| `param_item_variant` | `String` | アイテムバリアント |
| `param_level` | `Long` | レベル |
| `param_location` | `Long` | 位置 |
| `param_medium` | `String` | ミディアム |
| `param_number_nights` | `Long` | 宿泊数 |
| `param_number_pax` | `Long` | 乗客数 |
| `param_number_rooms` | `Long` | 部屋数 |
| `param_origin` | `String` | 発地 |
| `param_price` | `Double` | 価格 |
| `param_quantity` | `Long` | 数量 |
| `param_screen_name` | `String` | 画面名 |
| `param_screen_class` | `String` | 画面クラス |
| `param_score` | `Long` | スコア |
| `param_search_term` | `String` | 検索語 |
| `param_shipping` | `Double` | 配送料 |
| `param_method` | `String` | 方法 |
| `param_source` | `String` | ソース |
| `param_travel_class` | `String` | 旅行クラス |
| `param_virtual_currency_name` | `String` | 仮想通貨名 |
| `param_start_date` | `String` | 開始日 |
| `param_term` | `String` | 期間 |
| `param_tax` | `Double` | 税金 |
| `param_transaction_id` | `String` | トランザクションID |
| `param_value` | `Long or Double` | 値 |
| `param_level_name` | `String` | レベル名 |
| `param_success` | `String` | 成功 |
| `param_ad_format` | `String` | 広告フォーマット |
| `param_ad_platform` | `String` | 広告プラットフォーム |
| `param_ad_source` | `String` | 広告ソース |
| `param_ad_unit_name` | `String` | 広告ユニット名 |
| `param_campaign_id` | `String` | キャンペーンID |
| `param_creative_format` | `String` | クリエイティブフォーマット |
| `param_discount` | `String` | 割引 |
| `param_extend_session` | `String` | セッション延長 |
| `param_item_category2` | `String` | アイテムカテゴリ2 |
| `param_item_category3` | `String` | アイテムカテゴリ3 |
| `param_item_category4` | `String` | アイテムカテゴリ4 |
| `param_item_category5` | `String` | アイテムカテゴリ5 |
| `param_item_list_id` | `String` | アイテムリストID |
| `param_item_list_name` | `String` | アイテムリスト名 |
| `param_items` | `Array` | アイテム |
| `param_location_id` | `String` | 位置ID |
| `param_marketing_tactic` | `String` | マーケティング戦術 |
| `param_payment_type` | `String` | 支払いタイプ |
| `param_promotion_id` | `String` | プロモーションID |
| `param_promotion_name` | `String` | プロモーション名 |
| `param_shipping_tier` | `String` | 配送層 |
| `param_source_platform` | `String` | ソースプラットフォーム |
| `param_user_signup_method` | `String` | ユーザー登録方法 |
| `param_user_allow_ad_personalization_signals` | `String` | ユーザー広告パーソナライゼーション信号許可 |
| `param_email_address` | `String` | メールアドレス |
| `param_phone_number` | `String` | 電話番号 |
| `param_hashed_email_address` | `String` | ハッシュ化されたメールアドレス |
| `param_hashed_phone_number` | `String` | ハッシュ化された電話番号 |

### E-コマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文ID |
| `order_total` | `Long or Double` | 注文合計 |
| `order_shipping` | `Double` | 配送料 |
| `order_tax` | `Double` | 税金 |
| `order_currency` | `String` | 通貨 |
| `order_coupon_code` | `String` | プロモーションコード |
| `product_id` | `Array` | 商品IDリスト |
| `product_name` | `Array` | 商品名リスト |
| `product_brand` | `Array` | ブランドリスト |
| `product_category` | `Array` | カテゴリリスト |
| `product_quantity` | `Array` | 数量リスト |
| `product_unit_price` | `Array` | 単価リスト |
| `param_item_list` | `Array` | プレゼンテーションリスト |
| `param_item_variant` | `Array` | バリアントリスト |
| `param_index` | `Array` | インデックスリスト |

### 同意構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `ad_storage` | `String` | 広告保存 |
| `analytics_storage` | `String` | 分析保存 |
| `ad_user_data` | `String` | 広告ユーザーデータ |
| `ad_personalization` | `String` | 広告パーソナライゼーション |

## イベント

Firebaseイベントをトリガーするには、モバイルプロファイルのFirebaseモジュールで`tealium_event`の値を対応するFirebaseイベント名にマッピングします。たとえば、このマッピングでは`tealium_event="purchase"`が`purchase`および`logEvent`のFirebaseイベントをトリガーします。

![](https://docs.tealium.com/images/platforms/prism/prism-modules-firebase-mappings.png)

### `initiateconversionmeasurement`

| | |
| :--- | :--- |
| iOSメソッド | `initiateOnDeviceConversionMeasurement()` |
| Androidメソッド | N/A |
| 宛先 | `hashed_email_address`, `hashed_phone_number`, `email_address`, `phone_number` |
| 注意 | iOSのみ。少なくとも1つの宛先が必要です。複数の宛先がマッピングされている場合、リストされた順番で最初のもののみが使用されます。 |
{class="dt--pivot"}

### `logevent`

| | |
| :--- | :--- |
| iOSメソッド | `logEvent()` |
| Androidメソッド | `logEvent()` |
| 宛先 | `event_name`, `parameters`, `parameters.<param>`, `parameters.items.<param>` |
| 注意 | `event_name`は必須です。他のすべての宛先はオプションです。アイテムをマッピングするには、並列配列（例：`product_id`と`product_price`）または`parameters.items.<param>`を持つオブジェクトの配列を使用します。スカラーは単一要素の配列としてカウントされます。並列配列を使用する場合、`items`の下のすべての配列は同じ長さでなければなりません。長さが異なる場合、コマンドは`arrayLengthMismatch`で失敗します。null値はアイテムから削除され、値がないアイテムは削除されます。 |
{class="dt--pivot"}

### `resetdata`

| | |
| :--- | :--- |
| iOSメソッド | `resetAnalyticsData()` |
| Androidメソッド | `resetAnalyticsData()` |
| 宛先 | なし |
| 注意 | 分析データをクリアし、アプリインスタンスIDをリセットします。 |
{class="dt--pivot"}

### `setanalyticscollectionenabled`

| | |
| :--- | :--- |
| iOSメソッド | `setAnalyticsCollectionEnabled()` |
| Androidメソッド | `setAnalyticsCollectionEnabled()` |
| 宛先 | `analytics_collection_enabled` |
| 注意 | 以前に収集されたデータは保持されます。 |
{class="dt--pivot"}

### `setconsent`

| | |
| :--- | :--- |
| iOSメソッド | `setConsent()` |
| Androidメソッド | `setConsent()` |
| 宛先 | `consent_settings`, `consent_settings.ad_storage`, `consent_settings.analytics_storage`, `consent_settings.ad_user_data`, `consent_settings.ad_personalization` |
| 注意 | 各値は`granted`または`denied`でなければなりません。ペイロードに存在するタイプのみが更新されます。残りは以前の状態を維持します。 |
{class="dt--pivot"}

### `setdefaultparameters`

| | |
| :--- | :--- |
| iOSメソッド | `setDefaultEventParameters()` |
| Androidメソッド | `setDefaultEventParameters()` |
| 宛先 | `parameters`, `parameters.<param>` |
| 注意 | パラメータは既存のデフォルトにマージされ、同じ名前のものは置き換えられます。`parameters`を完全に省略すると、すべてのデフォルトがクリアされます。空の`parameters`オブジェクトは何も操作せず、現在のデフォルトをそのままにします。 |
{class="dt--pivot"}

### `setsessiontimeout`

| | |
| :--- | :--- |
| iOSメソッド | `setSessionTimeoutInterval()` |
| Androidメソッド | `setSessionTimeoutDuration()` |
| 宛先 | `session_timeout_seconds` |
| 注意 | 常に秒単位でマッピングされます。Androidは内部的にミリ秒に変換します。 |
{class="dt--pivot"}
### `setuserid`

| | |
| :--- | :--- |
| iOSメソッド | `setUserID()` |
| Androidメソッド | `setUserId()` |
| 宛先 | `user_id` |
| 備考 | 空の文字列はユーザーIDをクリアします。 |
{class="dt--pivot"}

### `setuserproperty`

| | |
| :--- | :--- |
| iOSメソッド | `setUserProperty()` |
| Androidメソッド | `setUserProperty()` |
| 宛先 | `property_name`, `property_value` |
| 備考 | 両方の宛先は文字列または文字列の配列を受け入れます。配列は同じ長さでなければなりません。値が空の場合はプロパティが削除されます。 |
{class="dt--pivot"}

## 検証

テストデバイスでFirebaseデバッグモードを有効にし、`logevent`にマッピングされるイベントを追跡します。イベントは数秒以内に**DebugView**にマッピングされたパラメータと共に表示されます。

* [Xcodeデバッグコンソールでイベントを表示する](https://firebase.google.com/docs/analytics/ios/events#view-events-in-xcode-debug-console)（iOS）
* [デバッグログでイベントを表示する](https://firebase.google.com/docs/analytics/android/events#view-events-in-debug-log)（Android）

イベントが表示されない場合は、[Trace](https://docs.tealium.com/platforms/prism-mobile/trace/)を使用して、期待されるデータレイヤー値でPrismにイベントが到達したことを確認してください。

## トラブルシューティング

| 症状 | 原因 | 対処法 |
| :--- | :--- | :--- |
| DebugViewにイベントが表示されない | リモートまたはローカルの構成に`FirebaseDispatcher`のエントリがありません。 | モバイルプロファイルにFirebaseモジュールを追加して公開するか、ローカル構成ファイルを確認してください。 |
| イベントがPrismに到達するがFirebaseには到達しない | その`tealium_event`に対して`command_name`のマッピングが構成されていません。 | イベント名にフィルターをかけた`command_name`マッピングを追加してください。 |
| 構成が適用されない | ローカル、リモート、プログラムによる構成でモジュールIDが異なります。 | すべてのソースで`modules`の下で同じキーを使用してください。 |
| AndroidでFirebaseログが無音 | `log_level`はiOS専用です。 | `adb shell setprop log.tag.FA VERBOSE`を実行してください。 |
| `invalidParameterType`で同意コマンドが失敗 | 同意のタイプまたはステータスが受け入れられる値のいずれかではありません。 | `ad_storage`, `analytics_storage`, `ad_user_data`, `ad_personalization`のみを`granted`または`denied`（大文字小文字を区別しない）にマッピングしてください。他の値はコマンド全体が失敗します。 |

### コマンドエラー

コマンドが失敗すると、ディスパッチャーは警告をログに記録し、そのコマンドをスキップして続行します。同じイベントにマップされた他のコマンドは実行され、イベントは他のディスパッチャーにも到達します。デバイスログで`Command '<name>' failed:`を検索してください。メッセージの言い回しはiOSとAndroidでわずかに異なりますが、エラータイプは両方で同じです。

| エラー | 原因 | 対処法 |
| :--- | :--- | :--- |
| `missingParameter` | コマンドが必要とする宛先にマッピングがありません。 | マッピングしてください。必要なもの：`logevent`の`event_name`, `setuserid`の`user_id`, `setuserproperty`の`property_name`と`property_value`, `setconsent`の`consent_settings`, `setsessiontimeout`の`session_timeout_seconds`, `setanalyticscollectionenabled`の`analytics_collection_enabled`. |
| `invalidParameterType` | マッピングされた値が正しいタイプではない、未知の同意タイプまたはステータスを指名している、または`hashed_*`の値が有効なBase64ではありません。 | コマンドテーブルに対してタイプを確認してください。同意については、サポートされている4つのタイプのみを`granted`または`denied`にマッピングしてください。 |
| `arrayLengthMismatch` | `parameters.items`の下または`property_name`に対する`property_value`で、並列配列の長さが異なります。 | 配列を同じ長さにするか、`items`をオブジェクトの配列形式に切り替えてください。 |
| `commandNotFound` | `map_to`の値がサポートされているコマンド名ではありません。 | コマンドテーブルに対して確認してください。一致は大文字小文字を区別せず、周囲の空白を無視しますが、名前には区切り文字が含まれていてはなりません。例えば`setuserid`や`SetUserID`はOKですが、`set_user_id`はNGです。 |

より一般的でないエラー`emptyParameter`, `emptyArray`, `noValidParameters`は、マッピングされた値が空である場合や、コマンドに対してサポートされている宛先がマッピングされていない場合に発生します。

## 制限事項

* `initiateconversionmeasurement`と`log_level`はiOS専用です。
* アプリ内でアクティブにできるFirebaseディスパッチャーは1つだけです。

## 参考文献

* [Prism iOS Firebase API参照](https://docs.tealium.com/tealium-prism-ios-firebase-dispatcher/)
* [Prism Android Firebase API参照](https://docs.tealium.com/tealium-prism-android-firebase-dispatcher/)