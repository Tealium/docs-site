---
title: データレイヤー
description: 各モジュールによって提供されるデータレイヤー変数の完全なリスト。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/data-layer/
---
<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[Tealium for iOS (Swift) 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)を参照してください。
</blockquote>


## AppData

以下の変数は[`AppData`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/appdata/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `app_build` | アプリのマイナービルドバージョン | `2213` |
| `app_name` | アプリの名前（通常はApp Storeの名前）| `Digital Velocity` |
| `app_rdns` | アプリバンドルの完全修飾名| `com.tealium.digitalvelocity` |
| `app_uuid` | ランダムな`uuid`。アプリのインストール期間中、永続的な保存モジュールのいずれかが有効になっている限り、持続します。アプリがアンインストールされるとリセットされます。| `t3aL...1uM` |
| `app_version` | アプリバンドルのバージョン | `1.0` |
| `tealium_vid` | 永続的なTealium訪問ID| `t3aL...1uM` |
| `tealium_visitor_id` | `tealium_vid`と同じで、遺産的な理由から含まれています| `t3aL...1uM` |

## Attribution

以下の変数は[`Attribution`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/attribution/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `ad_campaign_id` | 対応する広告のキャンペーンID | `1234567890` |
| `ad_campaign_name` | 対応する広告のキャンペーン名 | `CampaignName` |
| `ad_creativeset_id` | 対応する広告が属するクリエイティブセットのID | `456093` |
| `ad_creativeset_name` | 対応する広告が属するクリエイティブセットの名前| `Beast Images` |
| `ad_group_id` | 対応する広告のキャンペーングループID | `1234567890` |
| `ad_group_name` | 対応する広告のキャンペーングループ名| `AdGroupName` |
| `ad_keyword` | 広告のインプレッションを引き起こしたキーワード| `Keyword` |
| `ad_keyword_matchtype` | ブロード、エグザクト、またはサーチマッチのいずれか。 | `Exact` |
| `ad_org_id` | 対応する広告のキャンペーン組織ID | `OrgID` |
| `ad_org_name` | 対応する広告のキャンペーン組織名 | `OrgName` |
| `ad_purchase_date` | ユーザーが初めてアプリをダウンロードした日時。`iadconversion-type = "Redownload"`の場合、これは元の購入日を表します。これはApple Search Adと関連しているかもしれませんし、そうでないかもしれません。| `2016-12-05T17:31:40Z` |
| `ad_region` | このインストールを引き起こしたキャンペーンに関連する国または地域を識別します。 | `US` |
| `ad_user_clicked_last_30_days` | ユーザーがアプリのダウンロードの30日前にSearch Adsのインプレッションをクリックしたかどうかを示すブール値 | [`true`, `false`] |
| `ad_user_conversion _type` | アプリの新規ダウンロードまたは再ダウンロードを識別します| `Download` |
| `ad_user_date_clicked` | ユーザーが対応する広告をクリックした日時| `2016-12-05T17:31:40Z` |
| `ad_user_date_converted` | ユーザーがアプリをダウンロードした日時| `2016-12-05T17:31:40Z` |
| `device_advertising_enabled` | ユーザーが広告トラッキングを許可したかどうかを示すブール値（`false`の場合、広告IDはゼロの文字列として表示されます）| [`true`, `false`] |
| `device_advertising_id` | ユーザーがリセット可能な広告識別子（IDFA）| `6D92078A-8246...` |
| `device_advertising_vendor_id` | 同じデバイス上の同じベンダーからのすべてのアプリで同じであることが保証される一意のID（例：com.tealiumまたはcom.acmeの最初の2部分のRDNSバンドル識別子）| `6D92078A-8246...` |

## Autotracking

以下の変数は[`Autotracking`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/autotracking/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `autotracked` | trueに構成され、各自動追跡トラッキングコールに追加されます| [`true`, `false`] |

## ConsentManager

以下の変数は[`ConsentManager`](https://docs.tealium.com/ja/platforms/ios-swift-v1/consent-management/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `consent_categories` | ユーザーが選択した同意カテゴリの配列| [`"analytics"`, `"cdp"`] |
| `consent_status` | ユーザーの現在の同意状態| [`consented`, `notConsented`] |
| `policy` | 同意ポリシー| `"gdpr"` |

## Connectivity

以下の変数は[`Connectivity`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/connectivity/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `queue_reason` | トラッキングリクエストが接続不足のためにキューに入れられた場合、トラックコールに追加されます。キューに入れられたイベントにのみ存在し、他のすべてのイベントには存在しません| `connectivity` |
| `was_queued` | トラッキングコールが接続不足のためにキューに入れられたかどうかを示します。キューに入れられたイベントにのみ存在し、他のすべてのイベントには存在しません| [`true`, `false`] |

##  Core

以下の変数は`Core`モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- |  --- |
| `enabled_modules` | 現在有効になっているすべてのモジュールのリスト| `["tagmanagement", "collect"]` |
| `screen_title` | trackViewコールに渡された画面タイトル| `"homescreen" `|
| `tealium_datasource` | すべてのディスパッチに追加されるデータソース名を指定します| `"a1b2c3"` |
| `tealium_event` | トラッキングされているイベントの名前| `"checkout"` |


##  Crash Reporter

以下の変数は[`CrashReporter`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `app_memory_usage` | クラッシュ時のデバイス上のアプリによって使用されている現在のメモリ| `143.57MB` |
| `crash_cause` | クラッシュの原因| `Crash Reason` |
| `crash_name` | 利用可能な場合、クラッシュのフレンドリー名| `Crash Name` |
| `crash_libraries` | クラッシュ時にロードされていたライブラリのリスト| `[{ "baseAddress": "0xa3e0000", "codeType": { "arch": 64, "typeEncoding": "Mach"}, "imageName": "/Applications/Xcode9.3.app/ Contents/Developer/Platforms/ iPhoneOS.platform/Developer/ Library/CoreSimulator/Profiles/ Runtimes/iOS.simruntime/ Contents/Resources/ RuntimeRoot/usr/lib/dyld_sim", "imageSize": 212992, "imageUuid": "4015e9b70bde" }]` |
| `crash_process_id` | クラッシュ時のアプリのPID| `84351` |
| `crash_process_path` | アプリが実行されていたパス| `/DemoApp.app/DemoApp` |
| `crash_parent_process` | アプリを起動した親プロセス| `launchd_sim` |
| `crash_parent_process_id`| 親プロセスのPID | `83183` |
| `crash_signal_address` | クラッシュのシグナルアドレス| `4572945982` |
| `crash_signal_code` | クラッシュを引き起こしたシグナルコード| `#0` |
| `crash_signal_name` | クラッシュを引き起こしたシグナル名| `SIGABRT` |
| `crash_threads` | クラッシュ時のすべてのアクティブスレッドを返します| `{"crashed": 1,"registers": {"cs": "0x07"},"stack": {"instructionPointer": 4572945982,"symbolInfo": {"symbolName": "","symbolStartAddr": 0},"threadId": ""}}` |
| `crash_uuid` | この特定のクラッシュのための一意の識別子| `CC2DA0E9-E544-429A-AC5E-A268FC62F02A` |
| `device_memory_usage` | クラッシュ時のデバイス上のアプリによって使用されている現在のメモリ| `143.57MB` |
| `device_memory_available` | クラッシュ時のデバイス上の空きメモリ| `1068.88MB` |
| `device_os_build` | 現在のOSビルド番号| `15E217` |
| `memory_free` | クラッシュ時のデバイス上の空きメモリ| `1068.88MB` |
## DeviceData

以下の変数は、[`DeviceData`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/device-data/) モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明  | 例 |
|---|---| --- |
| `app_memory_usage`   | 現在のプロセス/アプリが使用しているメモリ（メガバイト単位）| `35.75MB`          |
| `app_orientation`    | アプリの向き（statusBarOrientationから; アプリが特定の向きにロックされている場合、デバイスの向きと異なる場合があります）| `Portrait`       |
| `app_orientation_extended` | アプリの拡張向き（statusBarOrientationから; アプリが特定の向きにロックされている場合、デバイスの向きと異なる場合があります）| `Portrait Upside Down` |
| `carrier`                    | モバイルネットワークキャリア名| `EE`|
| `carrier_iso`                | モバイルキャリアISO| `gb`|
| `carrier_mcc`                | [キャリアモバイル国コード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `carrier_mnc`                | キャリアモバイルネットワークコード| `34`|
| `cpu_architecture`           | CPUアーキテクチャ| `64`|
| `cpu_type`                   | CPUタイプ| `ARM64v8`|
| `device`                     | 消費者デバイス名| `iPhone 7 Plus`|
| `device_architecture`        | デバイスアーキテクチャ| `64`|
| `device_battery_percent`     | トラックコール時の現在のバッテリーの割合| `58`|
| `device_cputype`             | デバイスCPUタイプ| `Intel`|
| `device_ischarging`          | トラックコール時にデバイスが充電中であるかどうかを示すブール値| [`true`, `false`]|
| `device_language`            | 現在のデバイス言語| `en`|
| `device_orientation`         | シンプルな向き| [`Portrait`, `Landscape`]|
| `device_orientation_extended`| 完全な向き| `Face Up`|
| `device_os_version`          | オペレーティングシステムのバージョン| `11.1`|
| `device_resolution`          | 画面解像度| `1080x1920`|
| `device_type`            | Apple内部デバイス識別子| `iPhone8,4`|
| `memory_active*`             | デバイス上のアクティブメモリの合計| `997.78MB`|
| `memory_compressed*`         | デバイス上の圧縮メモリの合計| `153.39MB`|
| `memory_free*`               | デバイス上の空きメモリの合計| `120.81MB`|
| `memory_inactive*`           | デバイス上の非アクティブメモリの合計| `441.83MB`|
| `memory_physical*`           | デバイス上の物理メモリ（RAM）の合計（メガバイト単位）| `2013.50MB`|
| `memory_wired*`              | デバイス上のワイヤードメモリの合計| `207.12MB`|
| `model_name`                 | モデル名| `iPhone 7 Plus`|
| `model_variant`              | モデルバリアント（デバイスに利用可能な無線技術を示すことが一般的です）| [`CDMA`, `GSM`, `WiFi`, `Cellular`]|
| `network_connection_type`    | 現在の接続タイプ| [`wifi`, `cellular`]|
| `_connection_type`           | 現在の接続タイプ| [`wifi`, `cellular`]|
| `network_iso_country_code`   | モバイルネットワークISO国コード| `gb`|
| `network_mcc`                | [ネットワークモバイル国コード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `network_mnc`                | [ネットワークモバイルネットワークコード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `network_name`               | モバイルネットワークキャリア名| `EE`|
| `os_build`                   | オペレーティングシステムビルドバージョン| `15J580`|
| `os_name`                    | オペレーティングシステム名| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `os_version`                 | オペレーティングシステムのバージョン| `11.1`|
| `platform`                   | オペレーティングシステム名| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `user_locale`                | 現在のデバイス言語| `en`|

## DispatchQueue

以下の変数は、[`DispatchQueue`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/dispatch-queue/) モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `queue_reason` | トラッキングリクエストがイベントバッチ処理のためにキューに追加された場合にトラックコールに追加されます。キューに入れられたイベントにのみ存在し、他のすべてのイベントには存在しません| `batching_enabled` |
| `was_queued` | イベントバッチ処理がないためにトラッキングコールがキューに入れられたかどうかを示します。キューに入れられたイベントにのみ存在し、他のすべてのイベントには存在しません| [`true`, `false`] |

## Lifecycle

以下の変数は、[`Lifecycle`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/lifecycle/) モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `lifecycle_dayofweek_local` | コールが行われた地元の曜日、例えば1=日曜日、2=月曜日| `4` |
| `lifecycle_dayssincelastwake` | 最後に検出された起動からの日数（整数で増加）| `1` |
| `lifecycle_dayssincelaunch` | 最初の起動からの日数（整数で増加）| `23` |
| `lifecycle_dayssinceupdate` | 最後に検出されたアプリバージョン更新からの日数（整数で増加）| `46` |
| `lifecycle_diddetect_crash` | この起動/起床イベント中にクラッシュが検出されたか（`true`の場合のみ記入）| [`true`, `false`] |
| `lifecycle_firstlaunchdate` | 最初に検出された起動/起床のGMTタイムスタンプ（UTCからのISO 8601形式）| `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | MM/DD/YYYY形式のGMTタイムスタンプ| `01/17/2012 `|
| `lifecycle_hourofday_local` | コールが行われた地元の時間（24時間形式）| [`true`, `false`] |
| `lifecycle_isfirstlaunch` | コールが最初の起動/起床コールである場合のみ存在します| [`true`, `false`] |
| `lifecycle_isfirstlaunchupdate` | コールが検出された更新後の最初の起動/起床である場合のみ存在します| [`true`, `false`] |
| `lifecycle_isfirstwakemonth` | コールが月の最初の起動/起床である場合のみ存在します| [`true`, `false`] |
| `lifecycle_isfirstwaketoday` | コールがその日の最初の起動/起床である場合のみ存在します| [`true`, `false`] |
| `lifecycle_launchcount` | アプリのこのバージョンの起動回数（最後の更新以降）| `3` |
| `lifecycle_priorsecondsawake` | 最後の起動以来のアプリが起きていた全秒数。すべての起床の合計が送信されます。`lifecycle_type:launch`コールでのみ送信されます。| `126` |
| `lifecycle_secondsawake` | 最も最近の起床/起動以来のアプリが起きていた全秒数| `30` |
| `lifecycle_sleepcount` | アプリがスリープ状態になった回数の合計（更新されるとリセットされます）| `5` |
| `lifecycle_totalcrashcount` | インストール以来カウントされたクラッシュの総数（アプリが削除されない限りリセットされません）| `21` |
| `lifecycle_totallaunchcount` | インストール以来の起動回数の合計（アプリが削除されない限りリセットされません）| `3` |
| `lifecycle_totalsecondsawake` | アプリがインストールされてから起きている/アクティブ状態にある総秒数（アプリが削除されない限りリセットされません）| `36` |
| `lifecycle_totalsleepcount` | アプリがインストールされてからバックグラウンドに入った回数の合計（アプリが削除されない限りリセットされません）| `"400"` |
| `lifecycle_totalwakecount` | インストール以来の起動+起床の合計回数（アプリが削除されない限りリセットされません）| `"563"` |
| `lifecycle_type` | ライフサイクルコールのタイプ。| [`"launch"`, `"wake"`, `"sleep"` ]|
| `lifecycle_updatelaunchdate` | バージョン更新が検出された後の最初の起床/起動のGMTタイムスタンプ| `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount` | アプリのこのバージョンの起動+起床の合計回数（更新されるとリセットされます）| `"29"` |

## Location

以下の変数は、[`Location`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/location/) モジュールによってデータレイヤーに追加されます。

| 変数名                     | 説明| 例              |
|------------------------------------|---------|----------------------|
| `geofence_name`     | ジオフェンス領域の名前| `"Tealium_San_Diego"`|
| `geofence_transition_type` | ジオフェンス遷移イベントのタイプ| `"entered"` または `"exited"`|
| `latitude`          | ユーザーの最も最近記録された位置の緯度| `"32.906119"`|
| `location_timestamp` | ユーザーがジオフェンス領域に入った/出た時の記録された日時（GMT）| `"2020-01-28 16:29:46 +0000"`|
| `longitude`        | ユーザーの最も最近記録された位置の経度| `"-117.23791632509666"`|
| `movement_speed` | デバイスの瞬間速度、メートル毎秒で測定| `"1.0"`|
## タグ管理

以下の変数は、[`TagManagement`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/) モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `dispatch_service` | トラッキングコールがどのモジュールから来たかを示す静的文字列 | `collect/tagmanagement` |

## 揮発性データ

以下の変数は、[`VolatileData`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/volatile-data/) モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `event_timestamp_iso` | ISO 8601 UTC形式のイベントタイムスタンプ | `2017-11-20T14:48:00Z` |
| `event_timestamp_local_iso` | ISO 8601 ローカルタイムゾーン形式のイベントタイムスタンプ | `2017-11-20T06:48:00` |
| `event_timestamp_offset_hours` | UTCからの現在のオフセット時間 | `-8` |
| `event_timestamp_unix` | 現在のUnixタイムスタンプ（1970年エポック）秒単位 | `1511189280` |
| `event_timestamp_unix_millis` | 現在のUnixタイムスタンプ（1970年エポック）ミリ秒単位 | `1511189280337` |
| `tealium_account` | 現在のTealiumアカウント（TealiumConfigオブジェクトから）| `tealium` |
| `tealium_environment` | 現在のTealium環境（TealiumConfigオブジェクトから）| `dev` |
| `tealium_library_name` | Tealiumライブラリ名 | `swift` |
| `tealium_library_version` | Tealiumライブラリバージョン | `1.8.0` |
| `tealium_profile` | 現在のTealiumプロファイル（TealiumConfigオブジェクトから）| `mobile` |
| `tealium_random` | ランダム数値 | `8449989974958830` |
| `tealium_session_id` | TealiumセッションID | `1511262829677` |
| `tealium_timestamp_epoch` | 現在のUnixタイムスタンプ（1970年エポック）秒単位 | `1511262829` |
| `timestamp` | ISO 8601 UTC形式のイベントタイムスタンプ | `2017-11-20T14:48:00Z` |
| `timestamp_local` | ISO 8601 ローカルタイムゾーン形式のイベントタイムスタンプ | `2017-11-20T06:48:00` |
| `timestamp_offset` | UTCからの現在のオフセット時間 | `-8` |
| `timestamp_unix` | 現在のUnixタイムスタンプ（1970年エポック）秒単位 | `1511189280` |
| `timestamp_unix_milliseconds` | 現在のUnixタイムスタンプ（1970年エポック）ミリ秒単位 | `1511189280337` |