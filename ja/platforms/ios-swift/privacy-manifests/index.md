---
title: iOSにおけるプライバシーマニフェスト
description: この記事では、プライバシーマニフェストとTealiumライブラリの使用中にAppleの新しい要件に準拠する方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift/privacy-manifests/
---
## Appleのプライバシーマニフェストファイル

Appleのプライバシーマニフェストは、アプリが使用する可能性のあるプライバシーに影響を与えるAPIを宣言するためのファイルです。Appleは、プライバシーマニフェストファイルを導入し、アプリ開発者が収集するプライバシーに関連するデータとアプリが使用するプライバシーに関連するAPIについて、ユーザーに対してより透明性を持たせるのを支援しています。アプリだけでなく、サードパーティのSDKもプライバシーマニフェストファイルを実装することができます。詳細については、Appleの[App Storeのアプリのプライバシーの詳細](https://developer.apple.com/app-store/app-privacy-details)と[プライバシーマニフェストファイル](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files)を参照してください。

## Tealiumのプライバシーマニフェスト

Tealium Swift SDKバージョン2.12.0以降には、[プライバシーマニフェスト](https://github.com/Tealium/tealium-swift/blob/main/tealium/core/PrivacyInfo.xcprivacy)が含まれており、Tealium Swift SDKが使用する必要のある理由APIを強調しています。

### 必要な理由API

Tealium Swift SDKは、「必要な理由」リストから2つのAPIを使用しています。これらはSDKと一緒に配布されるプライバシーマニフェストに含まれており、使用は許可された理由の範囲内です。

アプリは、独自の目的で「必要な理由」APIを使用する場合があります。この場合、アプリ開発者は独自のプライバシーマニフェストでその目的を指定する必要があります。

### データ収集の定義

Appleは、[App Storeのアプリのプライバシーの詳細のデータ収集セクション](https://developer.apple.com/app-store/app-privacy-details/#data-collection)で、「収集」という用語を次のように定義しています。

&gt; 「収集」とは、リアルタイムで送信されたリクエストを処理するために必要な期間よりも長い期間、デバイスからデータを送信する方法を指します。

この定義に加えて、Appleは[追加のガイダンスセクション](https://developer.apple.com/app-store/app-privacy-details/#additional-guidance)で次のように詳細を説明しています。

&gt; 「収集」とは、デバイスからデータを送信し、それを読み取り可能な形式で保存することを指します。たとえば、認証トークンやIPアドレスがサーバーコールで送信され、保持されない場合、またはデータがサーバーに送信され、リクエストの処理後にすぐに破棄される場合、App Store Connectの回答でこれを開示する必要はありません。

この定義によれば、データは、リクエストの処理に必要な時間よりも長く読み取り可能な形式で保存されている場合にのみ「収集」されます。この定義に従えば、Tealium SDKによって送信されるデータは、SDKによって収集されているわけではありません。したがって、私たちのプライバシーマニフェストにはデータ使用が報告されていません。

ただし、Tealiumの製品提供は多様であり、一部の場合には、Tealiumの顧客がAppleの定義に従ってデータを「収集」している可能性があります。たとえば、Tealiumの顧客がAudiencestreamでアプリユーザーのIPアドレスを訪問プロファイルに保存したり、Event Stream Connectorを介して後で使用するために保存したりする場合、このアクションは「収集」の定義に該当します。Tealiumの顧客は、自分自身のプライバシーマニフェストでこの動作を開示するかどうかを決定する責任があります。また、EventStreamやAudienceStreamを介してサードパーティにデータを送信しているかどうかを確認する必要があります。これらのデータが「収集」の定義に該当する可能性があります。

アプリのプライバシーマニフェストで宣言するデータを決定する際には、Tealium Swift SDKによって自動的に送信されるデータだけでなく、アプリが収集し、Tealium Swift SDKを介して送信している他のタイプのデータも考慮する必要があります。ただし、保存前にデータが削除される場合（例：変換または拡張機能を使用して）、そのデータは除外されます。

### トラッキングの定義

Appleの[トラッキング](https://developer.apple.com/app-store/app-privacy-details/#user-tracking)セクションでは、次のように「トラッキング」という用語を定義しています。

&gt; 「トラッキング」とは、特定のエンドユーザーやデバイスに関するアプリから収集されたデータ（ユーザーID、デバイスID、プロファイルなど）を、ターゲット広告や広告測定の目的でサードパーティデータとリンクさせること、またはアプリから収集されたデータをデータブローカーと共有することを指します。

&gt; 「サードパーティデータ」とは、所有していないアプリ、ウェブサイト、オフラインのプロパティから収集された特定のエンドユーザーやデバイスに関するデータを指します。

## TealiumSwiftライブラリによるデータの使用

TealiumのSDKは柔軟性があり、Tealiumの顧客が送信または収集するデータをTealiumが指示することはできません。したがって、すべてのアプリに対して汎用的なプライバシーマニフェストを提供することはできません。バンドルされたプライバシーマニフェストに含まれるAPIは、SDKを使用するために必要な最小限のものであり、Tealiumの顧客は、SDKが送信するデータの使用方法に応じて、追加のプライバシーマニフェストエントリが必要な場合があります。

以下の表は、Tealium Swift SDKによって送信されるデータをモジュールごとに分類したものです。Appleが定義する相対セクションに基づいています。Tealiumの顧客は、使用するモジュールから収集するデータを含むセクションを追加できます。

 CDPに送信されるデータが実際に保存されたり、販売されたりする場合を除き、すべてのカテゴリを報告する必要はありません。 

### Tealium Core

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `tealium_event` | アプリ内のユーザーアクティビティを追跡するために送信されるイベント | `NSPrivacyCollectedDataTypeProductInteraction` |
| `screen_title` | ユーザーが表示しているページ | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_name` | 完了までの時間を追跡しているイベント | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_start` | イベントの開始時間 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_end` | イベントの終了時間 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_duration` | イベントの期間 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `tealium_visitor_id` | AudienceStreamで使用されるID | `NSPrivacyCollectedDataTypeUserID` |
| `app_uuid` | 特定のデバイスにインストールされたアプリの固定ID | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_battery_percent` | 現在のバッテリー残量のパーセンテージ | `NSPrivacyCollectedDataTypePerformanceData` |
| `app_memory_usage` | アプリのメモリ使用量 | `NSPrivacyCollectedDataTypePerformanceData` |
| `memory_free` | 利用可能なメモリ量 | `NSPrivacyCollectedDataTypePerformanceData` |
| `device_ischarging` | デバイスが充電中かどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_active` | メモリがアクティブかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_inactive` | メモリが非アクティブかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_compressed` | メモリが圧縮されているかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_wired` | メモリが有線かどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_physical` | 物理メモリかどうか | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation` | デバイスの向き | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation_extended` | 拡張デバイスの向き | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_name` | デバイスのモデル | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_variant` | デバイスのバリアント | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_type` | デバイスのタイプ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_architecture` | デバイスのアーキテクチャ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_cputype` | デバイスのCPUタイプ | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_language` | デバイスの言語 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `os_name` | OSの名前 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_build` | アプリのビルド番号 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_name` | アプリの名前 | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_rdns` | アプリのRDNS | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_version` | アプリのバージョン | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_resolution` | デバイスの解像度 | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `device_logical_resolution` | デバイスの論理解像度 | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_url` | ディープリンクのURL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_param` | 各ディープリンクのクエリパラメータ | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_url` | ディープリンクのリファラURL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_app` | ディープリンクのリファラアプリ | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier` | キャリア | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mnc` | キャリアMNC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mcc` | キャリアMCC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_iso` | キャリアISO | `NSPrivacyCollectedDataTypeOtherDataTypes` |

### Tealium Attribution

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `device_advertising_id` | IDFA | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_advertising_vendor_id` | IDFV | `NSPrivacyCollectedDataTypeDeviceID` |

### Tealium Location

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `latitude` | 緯度（構成に基づく精度） | `NSPrivacyCollectedDataTypePreciseLocation`または`NSPrivacyCollectedDataTypeCoarseLocation` |
| `longitude` | 経度（構成に基づく精度） | `NSPrivacyCollectedDataTypePreciseLocation`または`NSPrivacyCollectedDataTypeCoarseLocation` |
| `geofence_name` | ユーザーが入退場したジオフェンス | `NSPrivacyCollectedDataTypeCoarseLocation` |

### Tealium Crash

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `crash_count` | このデバイス上のこのアプリで発生したクラッシュの数 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_threads` | クラッシュスレッド | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_libraries` | クラッシュライブラリ | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_address` | クラッシュシグナルアドレス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_name` | クラッシュシグナル名 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_code` | クラッシュシグナルコード | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_name` | クラッシュ名 | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process_id` | クラッシュ親プロセスID | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process` | クラッシュ親プロセス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_path` | クラッシュプロセスパス | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_id` | クラッシュプロセスID | `NSPrivacyCollectedDataTypeCrashData` |
| `device_os_build` | デバイスのOSビルド | `NSPrivacyCollectedDataTypeCrashData` |

### Tealium Lifecycle

|データキー|説明|Appleデータタイプ|
|--|--|--|
| `lifecycle_type` | ライフサイクルイベントのタイプ | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayofweek_local` | ライフサイクルイベントの現在の曜日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelaunch` | 最初の起動からの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssinceupdate` | 最後のアップデートからの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelastwake` | 最後の起動からの日数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_diddetectcrash` | ライフサイクルがクラッシュを検出したかどうか | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_firstlaunchdate` | 最初の起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | 最初の起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_hourofday_local` | ライフサイクルイベントの時間 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunch` | 最初の起動かどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunchupdate` | 最後のアップデート後の最初の起動かどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwakemonth` | 月の最初の起動かどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwaketoday` | 日の最初の起動かどうか | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastlaunchdate` | 最後の起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastsleepdate` | 最後のスリープ日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastwakedate` | 最後の起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastupdatedate` | 最後のアップデート日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_launchcount` | 起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_priorsecondsawake` | 前回の起動時の起動時間（秒） | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_secondsawake` | 起動時間（秒） | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_sleepcount` | スリープ回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalcrashcount` | 総クラッシュ回数 | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_totallaunchcount` | 総起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalwakecount` | 総起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsleepcount` | 総スリープ回数 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsecondsawake` | 総起動時間（秒） | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_updatelaunchdate` | 最後のアップデート後の最初の起動日 | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_wakecount` | 起動回数 | `NSPrivacyCollectedDataTypeProductInteraction` |

## 例

以下の例は、Tealium Swift SDKによって送信されるデータと、プライバシーマニフェストに報告する必要のあるデータのタイプを示しています。

 アプリは、Tealium Swift SDKが自動的に送信するデータよりも多くのデータを送信する場合があります。これは、データレイヤに追加するか、トラックリクエストにより多くのデータを追加することによって行われる場合があります。したがって、このデータタイプのリストは、アプリが報告する必要があるすべてのものの網羅的なリストではありません。 

アプリがAudienceStreamを使用している場合、`tealium_visitor_id`変数を使用して訪問プロファイルを保存および取得し、`tealium_event`および`screen_name`変数を使用してアプリ内で訪問が行っている操作を検出する場合があります。AudienceStreamは、これらのイベントとスクリーンに基づいて訪問プロファイルを変更します。

このアプリは、ライフサイクルモジュールを使用して、訪問がアプリをどれくらいの頻度で使用しているか、どれくらいの時間使用しているかなど、訪問に関する情報を推測する場合があります。

最後に、このアプリは位置情報データを使用して、訪問の一般的な位置と居住国を特定し、AudienceStreamが訪問プロファイルに保存します。

これらのユースケースを考慮すると、彼らのマニフェストファイルに報告する必要のある`NSPrivacyCollectedDataType`データオブジェクトを決定できます。

* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeCoarseLocation`

### イベントDBのユースケース

EventDBを使用し、データレイヤに何も削除せずにSDKから送信されるすべてのデータを保存するアプリは、使用するすべてのモジュールのすべてのデータタイプを報告する必要があります。

アプリがCoreとAttributionモジュールのみを使用している場合、マニフェストファイルには次の項目が含まれている必要があります。

* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeDeviceID`
* `NSPrivacyCollectedDataTypePerformanceData`
* `NSPrivacyCollectedDataTypeOtherDiagnosticData`
* `NSPrivacyCollectedDataTypeOtherDataTypes`

アプリがLocation、Crash、およびLifecycleモジュールも使用している場合、マニフェストファイルには次の項目も含まれている必要があります。

* `NSPrivacyCollectedDataTypeCoarseLocation`および/または`NSPrivacyCollectedDataTypePreciseLocation`
* `NSPrivacyCollectedDataTypeCrashData`

## トラッキングとトラッキングドメイン

アプリのプライバシーマニフェストファイルには、Tealiumに関連する2つのプロパティが含まれている場合があります。

* `NSPrivacyTracking`
* `NSPrivacyTrackingDomains`

これらの2つのプロパティは、Appleのトラッキングの定義に関連しているため、TealiumのSDKのアクティビティは含まれていません。ただし、一部のTealiumの顧客は、Tealium Swift SDKを介して送信されるデータを使用して訪問を追跡している場合があります。そのような場合、Tealiumのドメインをトラッキングドメインとして指定し、アプリが訪問を積極的に追跡していることを明示する必要があります。

Tealiumのドメインをトラッキングドメインとしてリストに追加すると、訪問がトラッキングの承認を拒否した場合、AppleはTealiumがトラッキングデータを受け取るのをブロックします。

トラッキングが特定のベンダータグまたはリモートコマンドを介してのみ行われる場合は、Tealiumのドメインの代わりにベンダーのトラッキングエンドポイントをトラッキングドメインのリストに追加します。この方法では、訪問が承認を拒否した場合でも、他のすべてのTealiumの機能が正常に動作します。

