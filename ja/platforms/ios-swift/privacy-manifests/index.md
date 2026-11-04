---
title: iOSのプライバシーマニフェスト
description: この記事では、プライバシーマニフェストと、Tealiumライブラリを使用しながらAppleの新しい要件に準拠する方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift/privacy-manifests/
---
## Appleのプライバシーマニフェストファイル

Appleのプライバシーマニフェストは、アプリが使用する、プライバシーに影響を与える可能性のあるAPIを宣言するためのファイルです。Appleは、アプリデベロッパーが、収集するプライバシーに関わるデータや、アプリで使用するプライバシーに関わるAPIについて、ユーザーに対する透明性を高められるよう、プライバシーマニフェストファイルを導入しました。アプリに加えて、サードパーティSDKもプライバシーマニフェストファイルを実装できます。詳細については、Appleの[App Storeにおけるアプリのプライバシー詳細](https://developer.apple.com/app-store/app-privacy-details)および[プライバシーマニフェストファイル](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files)を参照してください。

## Tealiumのプライバシーマニフェスト

Tealium Swift SDKバージョン2.12.0以降には、Tealium Swift SDKが使用するRequired Reason APIを示す[プライバシーマニフェスト](https://github.com/Tealium/tealium-swift/blob/main/tealium/core/PrivacyInfo.xcprivacy)が含まれています。

### Required Reason API

Tealium Swift SDKは、「Required Reason」リストに含まれる2つのAPI（User DefaultsとDisk Space）を使用します。これらはSDKとともに配布されるプライバシーマニフェストに含まれており、その使用方法は許可された理由の範囲内です。

アプリが独自の目的で「Required Reason」APIを使用する場合、アプリデベロッパーは自身のプライバシーマニフェストにその使用目的を明記する必要があります。

### データ収集の定義

Appleは、[App Storeにおけるアプリのプライバシー詳細の「データ収集」セクション](https://developer.apple.com/app-store/app-privacy-details/#data-collection)で、*収集*という用語を次のように定義しています。

> 「収集」とは、送信されたリクエストをリアルタイムで処理するために必要な期間を超えて、自社またはサードパーティパートナーがアクセスできる形で、デバイス外にデータを送信することを指します。

Appleは、この定義に加えて、[追加ガイダンスのセクション](https://developer.apple.com/app-store/app-privacy-details/#additional-guidance)で次のように詳しく説明しています。

> 「収集」とは、デバイス外にデータを送信し、自社またはサードパーティパートナーがリクエストを処理するために要する時間を超えて、読み取り可能な形式で保存することを指します。たとえば、認証トークンやIPアドレスがサーバー呼び出しで送信されても保持されない場合、またはデータがサーバーに送信された後、リクエストの処理直後に破棄される場合は、App Store Connectの回答でこれを開示する必要はありません。

この定義によると、データが「収集」されたと見なされるのは、リクエストの処理に要する時間を超えて、読み取り可能な形式で保存される場合に限られます。この定義に従うと、Tealium SDKによって送信されるデータはいずれも、TealiumのSDKによって収集されるものではありません。そのため、Tealiumのプライバシーマニフェストではデータの使用について申告していません。

ただし、Tealiumの製品は多岐にわたるため、場合によっては、Tealiumのお客様がAppleの定義に基づいてデータを「収集」している可能性があります。たとえば、Tealiumのお客様が、アプリユーザーのIPアドレスをCustomer Data Platform（CDP）の訪問プロファイルに保存したり、Event Streamingコネクタを介して後で使用するために保存したりした場合、その行為は「収集」の定義に該当します。データを収集しているかどうかを判断し、その行為を自身のプライバシーマニフェストで開示する最終的な責任は、Tealiumのお客様にあります。また、Tealiumのお客様は、Event StreamingまたはCustomer Data Platform（CDP）を介して、「収集」の定義に該当する可能性のあるデータをサードパーティに送信していないか確認する必要があります。

アプリのプライバシーマニフェストで何を宣言するかを決定する際は、Tealium Swift SDKによって自動的に送信されるデータに加えて、アプリが収集し、Tealium Swift SDKを介して送信するその他の種類のデータも考慮する必要があります。唯一の例外は、影響を受けるデータが保存前に（たとえば、変換または拡張機能を使用して）除去される場合です。

### トラッキングの定義

Appleは、App Storeにおけるアプリのプライバシー詳細の[トラッキング](https://developer.apple.com/app-store/app-privacy-details/#user-tracking)セクションで、*トラッキング*という用語を次のように定義しています。

> 「トラッキング」とは、特定のエンドユーザーまたはデバイスについてアプリから収集したユーザーID、デバイスID、プロファイルなどのデータを、ターゲティング広告または広告効果測定を目的としてサードパーティデータと関連付けること、あるいは特定のエンドユーザーまたはデバイスについてアプリから収集したデータをデータブローカーと共有することを指します。

> 「サードパーティデータ」とは、自社が所有していないアプリ、Webサイト、またはオフライン資産から収集された、特定のエンドユーザーまたはデバイスに関するあらゆるデータを指します。

## TealiumSwiftライブラリによるデータ使用

Tealium SDKは柔軟性が高く、Tealiumのお客様が送信または収集するデータをTealiumが指定することはできないため、すべてのアプリに対応する汎用的なプライバシーマニフェストを提供することはできません。同梱のプライバシーマニフェストに含まれるAPIは、SDKを使用するために最低限必要なものです。Tealiumのお客様は、SDKが送信するデータの使用方法に応じて、プライバシーマニフェストに追加の項目を記載しなければならない場合があります。

以下の表は、Tealium Swift SDKによって送信されるデータを、Appleが定義する関連セクションに従ってモジュール別に示しています。Tealiumのお客様は、使用しているモジュールから実際に収集するデータを含むセクションを追加できます。


<blockquote>
CDPに送信されたデータが、実際に保存されるか、そのデータを保存または販売するサードパーティに送信される場合を除き、これらすべてのカテゴリを申告する必要はありません。
</blockquote>

### Tealium Core

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `tealium_event` | アプリ内のユーザーアクティビティを追跡するために送信されるイベント | `NSPrivacyCollectedDataTypeProductInteraction` |
| `screen_title` | ユーザーが表示しているページ | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_name` | 完了までの時間を追跡するイベント | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_start` | イベント継続時間の計測開始 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_end` | イベント継続時間の計測終了 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_duration` | イベントの計測時間 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `tealium_visitor_id` | CDPに使用されるID | `NSPrivacyCollectedDataTypeUserID` |
| `app_uuid` | 特定のデバイスにインストールされたアプリの固定ID | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_battery_percent` | 現在のバッテリー充電率 | `NSPrivacyCollectedDataTypePerformanceData` |
| `app_memory_usage` | アプリが使用しているメモリ量 | `NSPrivacyCollectedDataTypePerformanceData` |
| `memory_free` | 使用可能なメモリ量 | `NSPrivacyCollectedDataTypePerformanceData` |
| `device_ischarging` | デバイスが充電中かどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_active` | メモリがアクティブかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_inactive` | メモリが非アクティブかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_compressed` | メモリが圧縮されているかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_wired` | メモリがワイヤードかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_physical` | メモリが物理メモリかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation` | デバイスの向き | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation_extended` | デバイスの拡張方向情報 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_name` | デバイスのモデル | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_variant` | デバイスのバリアント | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_type` | デバイスのタイプ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_architecture` | デバイスのアーキテクチャ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_cputype` | デバイスのCPUタイプ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_language` | デバイスの言語 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `os_name` | OS名 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_build` | アプリのビルド番号 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_name` | アプリ名 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_rdns` | アプリのRDNS | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_version` | アプリのバージョン | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_resolution` | デバイスの解像度 | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `device_logical_resolution` | デバイスの論理解像度 | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_url` | ディープリンクURL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_param` | 各ディープリンクのクエリパラメータ | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_url` | ディープリンクの参照元URL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_app` | ディープリンクの参照元アプリ | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier` | 通信事業者 | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mnc` | 通信事業者のMNC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mcc` | 通信事業者のMCC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_iso` | 通信事業者のISOコード | `NSPrivacyCollectedDataTypeOtherDataTypes` |

### Tealium Attribution

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `device_advertising_id` | IDFA | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_advertising_vendor_id` | IDFV | `NSPrivacyCollectedDataTypeDeviceID` |

### Tealium Location

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `latitude` | 緯度（精度は構成に基づく） | `NSPrivacyCollectedDataTypePreciseLocation` または `NSPrivacyCollectedDataTypeCoarseLocation` |
| `longitude` | 経度（精度は構成に基づく） | `NSPrivacyCollectedDataTypePreciseLocation` または `NSPrivacyCollectedDataTypeCoarseLocation` |
| `geofence_name` | ユーザーが進入または退出したジオフェンス | `NSPrivacyCollectedDataTypeCoarseLocation` |

### Tealium Crash

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `crash_count` | このデバイス上でこのアプリに発生したクラッシュの回数 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_threads` | クラッシュ時のスレッド | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_libraries` | クラッシュ時のライブラリ | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_address` | クラッシュシグナルのアドレス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_name` | クラッシュシグナル名 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_code` | クラッシュシグナルコード | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_name` | クラッシュ名 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process_id` | クラッシュしたプロセスの親プロセスID | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process` | クラッシュしたプロセスの親プロセス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_path` | クラッシュしたプロセスのパス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_id` | クラッシュしたプロセスのID | `NSPrivacyCollectedDataTypeCrashData` |
| `device_os_build` | デバイスのOSビルド | `NSPrivacyCollectedDataTypeCrashData` |
### Tealium Lifecycle

|データキー|説明|Apple データ型|
|--|--|--|
| `lifecycle_type` | ライフサイクルイベントの種類 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayofweek_local` | ライフサイクルイベント発生時の曜日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelaunch` | 初回起動からライフサイクルイベントまでの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssinceupdate` | 前回のアップデートからライフサイクルイベントまでの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelastwake` | 前回のウェイクからライフサイクルイベントまでの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_diddetectcrash` | ライフサイクルでクラッシュが検出されたかどうか | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_firstlaunchdate` | 初回起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | 初回起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_hourofday_local` | ライフサイクルイベント発生時の時刻（時） | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunch` | ライフサイクルイベントが初回起動であるかどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunchupdate` | ライフサイクルイベントがアップデート後の初回起動であるかどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwakemonth` | ライフサイクルイベントがその月の初回ウェイクであるかどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwaketoday` | ライフサイクルイベントがその日の初回ウェイクであるかどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastlaunchdate` | ライフサイクルイベントの前回起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastsleepdate` | ライフサイクルイベントの前回スリープ日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastwakedate` | ライフサイクルイベントの前回ウェイク日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastupdatedate` | ライフサイクルイベントの前回アップデート日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_launchcount` | ライフサイクルイベントの起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_priorsecondsawake` | 前回の起動時にアウェイク状態だった秒数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_secondsawake` | ライフサイクルイベントでアウェイク状態だった秒数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_sleepcount` | ライフサイクルイベントのスリープ回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalcrashcount` | ライフサイクルイベントのクラッシュ総回数 | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_totallaunchcount` | ライフサイクルイベントの合計起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalwakecount` | ライフサイクルイベントの合計ウェイク回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsleepcount` | ライフサイクルイベントの合計スリープ回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsecondsawake` | ライフサイクルイベントでアウェイク状態だった合計秒数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_updatelaunchdate` | 前回のアップデート後にライフサイクルイベントが初めて起動した日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_wakecount` | ライフサイクルイベントのウェイク回数 | `NSPrivacyCollectedDataTypeProductInteraction` |

## 例

以下の例では、Tealium Swift SDK によってデータが送信されるユースケースと、プライバシーマニフェストで報告する必要があるデータ型について説明します。


<blockquote>
アプリでは、データを DataLayer に追加したり、トラッキングリクエストをより多くのデータでエンリッチしたりすることで、Tealium Swift SDK が自動送信するデータよりも多くのデータを送信する場合があります。したがって、このデータ型の一覧は、アプリで報告が必要になる可能性のあるすべてのデータを網羅したものではありません。
</blockquote>


アプリが収集し、報告する必要があるデータ型ごとに、収集する理由も指定する必要があります。また、そのデータが訪問に明示的に関連付けられているか、トラッキングに使用されているかも指定する必要があります。詳細については、Apple の Developer サイトにある「[アプリまたはサードパーティ SDK がデータを収集する理由を報告する](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests#4250556)」を参照してください。

### Audience Stream のユースケース

CDP を使用するアプリでは、訪問プロファイルの保存と取得に `tealium_visitor_id` 変数を使用し、訪問がアプリ内で何をしているかを検出するために `tealium_event` 変数と `screen_name` 変数を使用する場合があります。CDP は、それらのイベントや訪問が移動した画面に応じて訪問プロファイルを変更します。

このアプリでは、Lifecycle モジュールを使用して、訪問がアプリを使用する頻度や使用時間など、訪問に関する情報を推測する場合もあります。

最後に、このアプリは位置情報データを使用して訪問のおおよその位置を特定し、居住国を判定します。CDP はこの情報を訪問プロファイルに保存します。

これらのユースケースを考慮すると、マニフェストファイルで報告する必要がある `NSPrivacyCollectedDataType` データオブジェクトは次のとおりです。

* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeCoarseLocation`

### EventDB のユースケース

EventDB を使用し、拡張機能や変換によってデータレイヤーから何も除外せずに SDK から送信されるすべてのデータを保存するアプリでは、使用するすべてのモジュールについて、すべてのデータ型を報告する必要があります。

アプリが Core モジュールと Attribution モジュールのみを使用している場合、マニフェストファイルには次の項目を含める必要があります。

* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeDeviceID`
* `NSPrivacyCollectedDataTypePerformanceData`
* `NSPrivacyCollectedDataTypeOtherDiagnosticData`
* `NSPrivacyCollectedDataTypeOtherDataTypes`

アプリが Location、Crash、および Lifecycle モジュールも使用している場合、マニフェストファイルには次の項目も含める必要があります。

* `NSPrivacyCollectedDataTypeCoarseLocation` および／または `NSPrivacyCollectedDataTypePreciseLocation`
* `NSPrivacyCollectedDataTypeCrashData`

## Tracking と TrackingDomains

アプリのプライバシーマニフェストファイルには、Tealium に関連する可能性がある次の 2 つのプロパティも含まれています。

* `NSPrivacyTracking`
* `NSPrivacyTrackingDomains`

これら 2 つのプロパティは Apple によるトラッキングの定義に基づくため、Tealium SDK のアクティビティは含まれません。ただし、一部の Tealium のお客様は、Tealium Swift SDK を介して送信されるデータを使用して訪問をトラッキングしている場合があります。その場合、Tealium のドメインをトラッキングドメインとして指定し、アプリが訪問を積極的にトラッキングしていることを明示する必要がある場合があります。

Tealium のドメインをトラッキングドメインとして指定すると、トラッキングの許可を拒否した訪問について、Tealium がトラッキングデータを受信することを Apple が能動的にブロックします。

トラッキングが特定のベンダータグまたは RemoteCommand を介してのみ行われる場合は、Tealium のドメインではなく、そのベンダーのトラッキングエンドポイントをトラッキングドメインの一覧に追加してください。この方法により、訪問がトラッキングの許可を拒否した場合でも、Tealium のその他の機能はすべて想定どおりに動作します。