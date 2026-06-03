---
title: データレイヤー
description: 各モジュールが提供する共通のデータレイヤーの値とデータの管理方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift/data-layer/
---
## カスタムデータ

すべてのイベントで一般的なデータレイヤーの値が必要な場合がよくあります。これらの値をすべてのトラッキングコールに追加する必要がないようにするために、`tealium.dataLayer`メソッドを使用して、すべてのトラッキングコールに適用されるデータレイヤーの値を永続化します。値が保存されると、自動的にすべてのトラッキングイベントに含まれます。

### データの有効期限

データレイヤーの値には有効期限があり、有効期限が切れるとデータレイヤーから削除されます。カスタムデータレイヤーの値を構成する際に、値の有効期限をオプションで構成することができます。デフォルトの有効期間は現在のセッションです。

次の有効期限のタイプが利用可能です：

| タイプ                                     | 値           | 説明               |
|:-----------------------------------------|:----------------|:--------------------------|
| [セッション](#session-data) (デフォルト)       | `.session`      | 現在のセッションの終了時に有効期限が切れます |
| [再起動](#restart-data)                 | `.untilRestart` | アプリが閉じられるか再起動されると有効期限が切れます |
| [永久](#forever-data)                 | `.forever`      | 有効期限が切れることはありません             |
| [カスタム日付](#custom-date-data)         | `.after`        | 指定した日付で有効期限が切れます |
| [カスタム期間](#custom-duration-data) | `.afterCustom`  | 指定した期間で有効期限が切れます。期間は次の時間単位で指定します：`.minutes`, `.hours`, `.days`, `.months`, `.years` |

有効期限のタイプに基づいて、[add()](/ja/platforms/ios-swift/api/tealium-data-layer/#add)を使用してデータをデータレイヤーに保存します。

#### セッションデータ

セッションデータの値はセッションの間永続化されます。セッションは、一定の時間枠内でのユーザーのアクティビティによって決まります。セッションは、ユーザーの非アクティビティが30分続いた後に終了します。

セッションの後に有効期限が切れるデータレイヤーの値を永続化するには、次のようにします：  
```swift
tealium?.dataLayer.add(key: &#34;mysessionvar&#34;, value: &#34;hello&#34;, expiry: .session)
```

すべてのセッションデータを取得するには：  
```swift
let sessionData = tealium?.dataLayer.allSessionData
```

#### 再起動データ

再起動データの値は、各イベントの間永続化されます。アプリが閉じられるか再起動されると、データは削除されます。

次のアプリの再起動までデータレイヤーの値を永続化するには：  
```swift
tealium?.dataLayer.add(key: &#34;myrestartvar&#34;, value: &#34;foo&#34;, expiry: .untilRestart)
```

#### 永久データ

永久データの値は、現在のアプリのバージョンの寿命の間永続化されます。アプリがアンインストールされるか更新されると、データはデータレイヤーから削除されます。

永久データを永続化するには：  
```swift
tealium?.dataLayer.add(key: &#34;myforevervar&#34;, value: &#34;world&#34;, expiry: .forever)
```

#### カスタム日付データ

カスタム日付データの値は、指定した日付で永続化されます。

カスタム日付の有効期限を持つデータレイヤーの値を永続化するには：  
```swift
tealium?.dataLayer.add(key: &#34;customdate&#34;, value: &#34;bar&#34;, expiry: .after(yourDate))
```

#### カスタム期間データ

カスタム期間データの値は、指定した期間の後に永続化されます。

1日後に有効期限が切れるデータレイヤーの値を永続化するには：  
```swift
tealium?.dataLayer.add(key: &#34;lengthoftime&#34;, value: &#34;days&#34;, expiry: .afterCustom((.days, 1)))
```

1ヶ月後に有効期限が切れるデータレイヤーの値を永続化するには：  
```swift
tealium?.dataLayer.add(key: &#34;lengthoftime&#34;, value: &#34;months&#34;, expiry: .afterCustom((.months, 1)))
```

### すべてのデータの取得

データレイヤーに現在保存されているすべてのデータを取得するには、[all()](/ja/platforms/ios-swift/api/tealium-data-layer/#all)メソッドを使用します：  

```swift
let data: [String: Any] = tealium?.dataLayer.all
```

また、[`Tealium.gatherTrackData()`](/ja/platforms/ios-swift/api/tealium/#gathertrackdata)も参照してください。

### データのクリア

特定のキーのデータをクリアするには、[delete()](/ja/platforms/ios-swift/api/tealium-data-layer/#delete)メソッドを使用します：

- 複数のキー：`dataLayer.delete(forKeys:)`
- 単一のキー：`dataLayer.delete(forKey:)`

すべてのデータをクリアするには、[`deleteAll()`](/ja/platforms/ios-swift/api/tealium-data-layer/#delete)メソッドを使用します。

### 例

以下の例は、上記のメソッドを示しています：  
```swift
class TealiumHelper {
	var tealium: Tealium?
	let config = TealiumConfig(...)
	tealium = Tealium(config: config) { [weak self] _ in
		guard let self = self, let teal = self.tealium else { return }

		teal.dataLayer.add(key: &#34;mysessionvar&#34;, value: 123456)

		teal.dataLayer.add(key: &#34;myvarforever&#34;, value: &#34;hello&#34;, expiry: .forever)

		teal.dataLayer.add(key: &#34;campaign&#34;, value: &#34;summer&#34;, expiry: .afterCustom((.months, 3)))

		print(&#34;All event data: \(teal.dataLayer.all)&#34;)
		print(&#34;All session data: \(teal.dataLayer.allSessionData)&#34;)
		print(&#34;Single event data key `campaign`: \(teal.dataLayer.all[&#34;campaign&#34;])&#34;)

		teal.dataLayer.delete(forKeys: [&#34;myvarforever&#34;])

		teal.dataLayer.deleteAll()
	}
}
```

## モジュールデータ

### アプリデータコレクター

以下の変数は、[`AppData`](/ja/platforms/ios-swift/module-list/appdata/)モジュールによってデータレイヤーに追加されます。

| 変数名        | 説明                                                                                                                                                  | 例 |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `app_build`          | アプリのマイナービルドバージョン                                                                                                                               | `2213` |
| `app_name`           | アプリの名前（通常はApp Storeの名前）                                                                                                               | `Digital Velocity` |
| `app_rdns`           | アプリバンドルの完全修飾名                                                                                                                       | `com.tealium.digitalvelocity` |
| `app_uuid`           | ランダムな`uuid`。永続保存モジュールのいずれかが有効になっている場合、アプリのインストールの期間中永続化されます。アプリがアンインストールされるとリセットされます。 | `123e4567-e89b-12d3-a456-556642440000` |
| `app_version`        | アプリバンドルのバージョン                                                                                                                                    | `1.0` |
| `tealium_vid`        | 永続的なTealiumビジターID                                                                                                                                | `t3aL...1uM` |
| `tealium_visitor_id` | `tealium_vid`と同じで、レガシーの理由で含まれています                                                                                                        | `t3aL...1uM` |

### アトリビューションコレクター

以下の変数は、[`Attribution`](/ja/platforms/ios-swift/module-list/attribution/)モジュールによってデータレイヤーに追加されます。

| 変数名                   | 説明                                                                                                                                                                                                            | 例 |
|:--------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `ad_campaign_id`                | 対応する広告のキャンペーンID                                                                                                                                                                                     | `1234567890` |
| `ad_campaign_name`              | 対応する広告のキャンペーン名                                                                                                                                                                                   | `CampaignName` |
| `ad_creativeset_id`             | 対応する広告が所属するクリエイティブセットのID                                                                                                                                                     | `456093` |
| `ad_creativeset_name`           | 対応する広告が所属するクリエイティブセットの名前                                                                                                                                                   | `Beast Images` |
| `ad_group_id`                   | 対応する広告のキャンペーングループID                                                                                                                                                                               | `1234567890` |
| `ad_group_name`                 | 対応する広告のキャンペーングループ名                                                                                                                                                                             | `AdGroupName` |
| `ad_keyword`                    | 対応する広告のインプレッションを生成したキーワード                                                                                                                                                                   | `Keyword` |
| `ad_keyword_matchtype`          | ブロード、エクサクト、または検索マッチのいずれかであるキーワードマッチタイプ                                                                                                                | `Exact` |
| `ad_org_id`                     | 対応する広告のキャンペーン組織ID                                                                                                                                                                        | `OrgID` |
| `ad_org_name`                   | 対応する広告のキャンペーン組織名                                                                                                                                                                      | `OrgName` |
| `ad_purchase_date`              | ユーザーがアプリを初めてダウンロードした日時。`iadconversion-type = &#34;Redownload&#34;`の場合、これは元の購入日です。これはApple Search Adに関連付けられている場合もあります。 | `2016-12-05T17:31:40Z` |
| `ad_region`                     | インストールを駆動したキャンペーンに関連付けられた国または地域を識別します。                                                                                                                                | `US` |
| `ad_user_clicked_last_30_days`  | ユーザーがアプリのダウンロードの30日前にSearch Adsのインプレッションをクリックしたかどうかを示すブール値                                                                                                                     | `true` |
| `ad_user_conversion _type`      | アプリの新規ダウンロードまたは再ダウンロードを識別します                                                                                                                                                                       | `Download` |
| `ad_user_date_clicked`          | ユーザーが対応する広告をクリックした日時                                                                                                                                                                   | `2016-12-05T17:31:40Z` |
| `ad_user_date_converted`        | ユーザーがアプリをダウンロードした日時                                                                                                                                                                              | `2016-12-05T17:31:40Z` |
| `device_advertising_enabled`    | ユーザーが広告のトラッキングを許可したかどうかを示すブール値（`false`の場合、広告IDはゼロの文字列として表示されます）                                                                                                      | `true` |
| `device_advertising_id`         | ユーザーがリセット可能な広告識別子（IDFA）                                                                                                                                                                          | `6D92078A-8246...` |
| `device_advertising_vendor_id`  | 同じベンダーから提供される同じデバイス上のすべてのアプリで同じであることが保証される一意のID（RDNSバンドル識別子の最初の2つの部分が同じであるアプリ、例えばcom.tealiumまたはcom.acme）                       | `6D92078A-8246...` |
| `device_tracking_authorization` | ディスパッチペイロードに追加されるトラッキングの[承認ステータス](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus) | `authorized` |

### オートトラッキングコレクター

以下の変数は、[`Autotracking`](/ja/platforms/ios-swift/module-list/autotracking/)モジュールによってデータレイヤーに追加されます。

| 変数名 | 説明                                                | 例 |
|:--------------|:-----------------------------------------------------------|:--------|
| `autotracked` | `true`に構成され、各自動トラッキングのトラッキングコールに追加されます | `true`  |

### Collectディスパッチャー

以下の変数は、[`Collect`](/ja/platforms/ios-swift/module-list/collect/)ディスパッチャーによってデータレイヤーに追加されます。

| 変数名        | 説明                                                        | 例 |
|:---------------------|:-------------------------------------------------------------------|:--|
| `dispatch_service`   | トラッキングコールの元となるモジュールを示す静的な文字列 | `collect` |
| `tealium_event_type` | ディスパッチされているイベントタイプを示す文字列            | `view`または`event` |

### Consent Managerモジュール

以下の変数は、[`ConsentManager`](/ja/platforms/ios-swift/consent-management/)モジュールが有効になっている場合にデータレイヤーに追加されます。

| 変数名        | 説明                                                          | 例 |
|:---------------------|:---------------------------------------------------------------------|:--|
| `consent_categories` | ユーザーが選択した同意カテゴリの配列                   | `[&#34;analytics&#34;, &#34;cdp&#34;]` |
| `consent_status`     | ユーザーの現在の同意ステータス                                    | `consented`, `notConsented` |
| `policy`             | 同意ポリシー                                                       | `gdpr`, `ccpa` |
| `do_not_sell`        | ユーザーがデータの販売を希望しないかどうか（CCPAの場合のみ） | `true` |

### Core

以下の変数は、`Core`モジュールによってデータレイヤーに追加されます。

| 変数名                  | 説明                                                                                                                                         | 例 |
|:-------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `enabled_modules`              | 現在有効なすべてのモジュールのリスト                                                                                                               | `tagmanagement`, `collect` |
| `screen_title`                 | trackViewコールに渡されるスクリーンタイトル                                                                                                               | `homescreen ` |
| `tealium_datasource`           | データソース名を指定します（すべてのディスパッチに追加されます）                                                                                            | `a1b2c3` |
| `tealium_event`                | トラッキングされているイベントの名前                                                                                                                 | `checkout` |
| `queue_reason`                 | トラッキングリクエストが接続の欠如によりキューに入れられた場合、トラックコールに追加される理由。キューに入れられたイベントにのみ存在し、他のイベントには存在しません。 | `connectivity` |
| `was_queued`                   | トラッキングコールが接続の欠如によりキューに入れられたかどうかを示します。キューに入れられたイベントにのみ存在し、他のイベントには存在しません。                    | `true` |
| `tealium_account`              | 現在のTealiumアカウント（TealiumConfigオブジェクトから）                                                                                                 | `tealium` |
| `tealium_environment`          | 現在のTealium環境（TealiumConfigオブジェクトから）                                                                                             | `dev` |
| `tealium_library_name`         | Tealiumライブラリ名                                                                                                                                | `swift` |
| `tealium_library_version`      | Tealiumライブラリのバージョン                                                                                                                             | `1.8.0` |
| `tealium_profile`              | 現在のTealiumプロファイル（TealiumConfigオブジェクトから）                                                                                                 | `mobile` |
| `tealium_random`               | ランダムな番号                                                                                                                                       | `8449989974958830` |
| `tealium_session_id`           | TealiumセッションID                                                                                                                                  | `1511262829677` |
| `tealium_timestamp_epoch`      | 現在のUnixタイムスタンプ（1970年のエポック）（秒単位）                                                                                                      | `1511262829` |
| `timestamp`                    | イベントのタイムスタンプをISO 8601形式（UTC）、UTCで表したもの                                                                                                         | `2017-11-20T14:48:00Z` |
| `timestamp_local`              | イベントのタイムスタンプをISO 8601形式のローカルタイムゾーンで表したもの                                                                                                           | `2017-11-20T06:48:00` |
| `timestamp_offset`             | 現在のオフセット時間（UTCからの時間単位）                                                                                                                    | `-8` |
| `timestamp_unix`               | 現在のUnixタイムスタンプ（1970年のエポック）（秒単位）                                                                                                      | `1511189280` |
| `timestamp_unix_milliseconds`  | 現在のUnixタイムスタンプ（1970年のエポック）（ミリ秒単位）                                                                                                 | `1511189280337` |
| `deep_link_url`                | `String`                                                                                                                                            | アプリを開いたディープリンクの完全なURL（クエリパラメータを含む）。 | `https://example.com/?campaign_code=SUMMER` |
| `deep_link_param_X`            | `String`                                                                                                                                            | ディープリンクURLの各クエリパラメータ。`X`はパラメータの名前であり、`deep_link_param_campaign_code`などです。| `SUMMER` |
| `deep_link_referrer_url` (iOS) | `String`                                                                                                                                            | ディープリンクがクリックされたブラウザページの完全なURL。 | `https://www.example.com/referring/page` |
| `deep_link_referrer_app` (iOS) | `String`                                                                                                                                            | ディープリンクが別のアプリでカスタムスキーマから来た場合のリファラーアプリの識別子。 | `com.example.appId` |


### クラッシュコレクター

以下の変数は、[`CrashReporter`](/ja/platforms/ios-swift/module-list/crash-reporter/)モジュールによってデータレイヤーに追加されます。

| 変数名             | 説明                                                           | 例 |
|:--------------------------|:----------------------------------------------------------------------|:--|
| `app_memory_usage`        | クラッシュ時のデバイス上のアプリの現在のメモリ使用量 | `143.57MB` |
| `crash_cause`             | クラッシュの原因                                                    | `Crash Reason` |
| `crash_name`              | クラッシュのフレンドリーな名前（利用可能な場合）                              | `Crash Name` |
| `crash_libraries`         | クラッシュ時にロードされたライブラリのリスト                     | `{ &#34;baseAddress&#34;: &#34;0xa3e0000&#34;, &#34;codeType&#34;: { &#34;arch&#34;: 64, &#34;typeEncoding&#34;: &#34;Mach&#34;}, &#34;imageName&#34;: &#34;/Applications/Xcode9.3.app/ Contents/Developer/Platforms/ iPhoneOS.platform/Developer/ Library/CoreSimulator/Profiles/ Runtimes/iOS.simruntime/ Contents/Resources/ RuntimeRoot/usr/lib/dyld_sim&#34;, &#34;imageSize&#34;: 212992, &#34;imageUuid&#34;: &#34;4015e9b70bde&#34; }` |
| `crash_process_id`        | クラッシュ時のアプリのPID                                       | `84351` |
| `crash_process_path`      | アプリが実行されているパス                                        | `/DemoApp.app/DemoApp` |
| `crash_parent_process`    | アプリを起動した親プロセス                                  | `launchd_sim` |
| `crash_parent_process_id` | 親プロセスのPID                                                    | `83183` |
| `crash_signal_address`    | クラッシュのシグナルアドレス                                   | `4572945982` |
| `crash_signal_code`       | クラッシュのシグナルコード                                     | `#0` |
| `crash_signal_name`       | クラッシュのシグナル名                                         | `SIGABRT` |
| `crash_threads`           | クラッシュ時のすべてのアクティブスレッドを返します。 | `{&#34;crashed&#34;: 1,&#34;registers&#34;: {&#34;cs&#34;: &#34;0x07&#34;},&#34;stack&#34;: {&#34;instructionPointer&#34;: 4572945982,&#34;symbolInfo&#34;: {&#34;symbolName&#34;: &#34;&#34;,&#34;symbolStartAddr&#34;: 0},&#34;threadId&#34;: &#34;&#34;}}` |
| `crash_uuid`              | この特定のクラッシュの一意の識別子                             | `CC2DA0E9-E544-429A-AC5E-A268FC62F02A` |
| `device_memory_usage`     | クラッシュ時のデバイス上のアプリの現在のメモリ使用量 | `143.57MB` |
| `device_memory_available` | クラッシュ時のデバイス上の空きメモリ                        | `1068.88MB` |
| `device_os_build`         | 現在のOSビルド番号                                               | `15E217` |
| `memory_free`             | クラッシュ時のデバイス上の空きメモリ                        | `1068.88MB` |

### デバイスデータコレクター

以下の変数は、[`DeviceData`](/ja/platforms/ios-swift/module-list/device-data/)モジュールによってデータレイヤーに追加されます。

| 変数名                 | 説明                                                                                                                                         | 例 |
|:------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `app_memory_usage`            | デバイス上の現在のプロセス/アプリのメモリ使用量（メガバイト単位）                                                                                             | `35.75MB` |
| `carrier`                     | モバイルネットワークのキャリア名                                                                                                                           | `EE` |
| `carrier_iso`                 | モバイルキャリアのISOコード                                                                                                                                    | `gb` |
| `carrier_mcc`                 | キャリアのモバイル国コード                                                                                                                           | `234` |
| `carrier_mnc`                 | キャリアのモバイルネットワークコード                                                                                                                           | `34` |
| `connection_type`             | 現在の接続タイプ                                                                                                                               | `wifi`, `cellular` |
| `device`                      | デバイス名                                                                                                                                  | `iPhone 7 Plus` |
| `device_architecture`         | デバイスのアーキテクチャ                                                                                                                                   | `64` |
| `device_battery_percent`      | トラックコール時の現在のバッテリー残量                                                                                                       | `58` |
| `device_cputype`              | デバイスのCPUタイプ                                                                                                                                       | `ARM64v8` |
| `device_ischarging`           | デバイスが現在充電中かどうかを示すブール値                                                                                                     | `true` |
| `device_language`             | 現在のデバイスの言語                                                                                                                               | `en-US` |
| `device_orientation`          | シンプルな方向                                                                                                                                    | `Portrait`, `Landscape` |
| `device_orientation_extended` | フルの方向                                                                                                                                      | `Face Up` |
| `device_os_version`           | オペレーティングシステムのバージョン                                                                                                                                    | `11.1` |
| `device_resolution`           | 物理的な画面解像度（幅x高さ）                                                                                                 | `828x1792` |
| `device_logical_resolution`   | 論理的な画面解像度（幅x高さ）                                                                                               | `414x896` |
| `device_type`                 | Apple内部のデバイス識別子                                                                                                                      | `iPhone12,1` |
| `memory_active*`              | デバイス上の合計アクティブメモリ                                                                                                                     | `997.78MB` |
| `memory_compressed*`          | デバイス上の合計圧縮メモリ                                                                                                                 | `153.39MB` |
| `memory_free*`                | デバイス上の合計空きメモリ                                                                                                                       | `120.81MB` |
| `memory_inactive*`            | デバイス上の合計非アクティブメモリ                                                                                                                 | `441.83MB` |
| `memory_physical*`            | デバイス上の合計物理メモリ（RAM）（メガバイト単位）                                                                                                 | `2013.50MB` |
| `memory_wired*`               | デバイス上の合計有線メモリ                                                                                                                      | `207.12MB` |
| `model_name`                  | モデル名                                                                                                                                            | `iPhone 7 Plus` |
| `model_variant`               | モデルのバリアント（一般的にはデバイスで利用可能な無線技術を示します）                                                                 | `CDMA`, `GSM`, `WiFi`, `Cellular` |
| `network_iso_country_code`    | モバイルネットワークのISO国コード                                                                                                                       | `gb` |
| `os_name`                     | オペレーティングシステム名                                                                                                                 | `iOS`, `tvOS`, `watchOS`, `macOS` |
| `platform`                    | オペレーティングシステム名                                                                                                                 | `iOS`, `tvOS`, `watchOS`, `macOS` |


### ライフサイクルコレクター

以下の変数は、[`Lifecycle`](/ja/platforms/ios-swift/module-list/lifecycle/)モジュールによってデータレイヤーに追加されます。

| 変数名                        | 説明                                                                                                                              | 例 |
|:-------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:--|
| `lifecycle_dayofweek_local`          | コールが行われたローカルの曜日。1=日曜日、2=月曜日など                                                                                   | `4` |
| `lifecycle_dayssincelastwake`        | 整数の増分で最後に検出された起動からの日数                                                                                      | `1` |
| `lifecycle_dayssincelaunch`          | 整数の増分で最初の起動からの日数                                                                                                    | `23` |
| `lifecycle_dayssinceupdate`          | 整数の増分で最後に検出されたアプリバージョンの更新からの日数                                                                 | `46` |
| `lifecycle_diddetect_crash`          | この起動/起床イベント中にクラッシュが検出されたかどうか（`true`の場合のみ表示されます）                                                            | `true` |
| `lifecycle_firstlaunchdate`          | 最初に検出された起動/起床のGMTタイムスタンプ（UTCのISO 8601形式）                                                         | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | MM/DD/YYYYの形式にフォーマットされたGMTタイムスタンプ                                                                                                    | `01/17/2012 ` |
| `lifecycle_hourofday_local`          | コールが行われたローカルの時間（24時間形式）                                                                                      | `true` |
| `lifecycle_isfirstlaunch`            | コールが最初の起動/起床コールである場合にのみ存在します                                                                                       | `true` |
| `lifecycle_isfirstlaunchupdate`      | コールが最初の起動/起床コールで、更新が検出された後である場合にのみ存在します                                                                 | `true`, `false` |
| `lifecycle_isfirstwakemonth`         | コールが月の最初の起動/起床コールである場合にのみ存在します                                                                                   | `true` |
| `lifecycle_isfirstwaketoday`         | コールがその日の最初の起動/起床コールである場合にのみ存在します                                                                                 | `true` |
| `lifecycle_launchcount`              | アプリのこのバージョンの総起動回数（最後の更新以降）                                                                                   | `3` |
| `lifecycle_priorsecondsawake`        | ランチのみの場合、前のすべての起動からのアプリが起動していた秒数の合計。`lifecycle_type:launch`コールのみで送信されます。 | `126` |
| `lifecycle_secondsawake`             | 最新の起動/起床からのアプリが起動していた秒数の合計                                                                                   | `30` |
| `lifecycle_sleepcount`               | アプリがスリープに入った回数の合計（更新された場合にリセットされます）                                                                 | `5` |
| `lifecycle_totalcrashcount`          | インストール以降にカウントされたクラッシュの合計回数（アプリが削除される場合のみリセットされます）                                                            | `21` |
| `lifecycle_totallaunchcount`         | インストール以降の起動の合計回数（アプリが削除される場合のみリセットされます）                                                               | `3` |
| `lifecycle_totalsecondsawake`        | アプリが起動している/アクティブな状態である秒数の合計（アプリが削除される場合のみリセットされます）                          | `36` |
| `lifecycle_totalsleepcount`          | アプリがバックグラウンドに入った回数の合計（アプリが削除される場合のみリセットされます）                                                        | `400` |
| `lifecycle_totalwakecount`           | インストール以降の起動&#43;起床の合計回数（アプリが削除される場合のみリセットされます）                                                               | `563` |
| `lifecycle_type`                     | ライフサイクルコールのタイプ                                                                                                                  | `launch`, `wake`, `sleep` |
| `lifecycle_updatelaunchdate`         | バージョンの更新が検出された後の最初の起動/起床のGMTタイムスタンプ                                                                 | `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount`                | このバージョンのアプリの起動&#43;起床の合計回数（更新される場合にリセットされます）                                                          | `29` |

### ロケーションコレクター

以下の変数は、[`Location`](/ja/platforms/ios-swift/module-list/location/)モジュールによってデータレイヤーに追加されます。

| 変数  名             | 説明                                          | 例 |
|:---------------------------|:-----------------------------------------|:--|
| `geofence_name`            | ジオフェンス領域の名前                      | `Tealium_San_Diego` |
| `geofence_transition_type` | ジオフェンスのトランジションイベントのタイプ | `entered`,`exited` |
| `location_timestamp`       | ユーザーがジオフェンス領域に入った/出た日時（GMT） | `2020-01-28 16:29:46 &#43;0000` |
| `latitude`                 | ユーザーの最新の位置の緯度                  | `32.906119` |
| `longitude`                | ユーザーの最新の位置の経度                  | `-117.23791632509666` |
| `movement_speed`           | デバイスの瞬間的な速度（メートル/秒）       | `1.0` |
| `location_accuracy`        | 位置モジュールの精度構成                  | `high`, `low` |

### タグ管理

以下の変数は、[`Tag Management`](/ja/platforms/ios-swift/module-list/tag-management/)モジュールによってデータレイヤーに追加されます。

| 変数名        | 説明                                                        | 例 |
|:---------------------|:-------------------------------------------------------------------|:--|
| `dispatch_service`   | トラッキングコールの元となるモジュールを示す静的な文字列 | `tagmanagement` |
| `tealium_event_type` | トラッキングされているイベントタイプを示す文字列            | `view`または`event` |
