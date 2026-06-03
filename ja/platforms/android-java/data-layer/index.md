---
title: データレイヤー
description: Androidライブラリからのデータレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/android-java/data-layer/
---以下の変数は、モバイルデータレイヤーの一部としてTealium Androidライブラリによって自動的に追加されます。これらの変数は、ライブラリからの各トラッキングコールに自動的に含まれ、Tealium Customer Data Hubの構成で使用できます。

これらの変数は、[モバイル用のプロファイルを有効化する]()ときに、あなたのTealium iQタグ管理アカウントに追加されます。

追加の変数は、5.0.x用の[ライフサイクルトラッキングモジュール](/ja/platforms/android/lifecycle-tracking-module/)で利用できます。

| 変数名 | Androidバージョン | 説明 | 例 |
| --- | --- | --- | --- |
| `app_build` | 5.4&#43; | アプリのビルドバージョン | `1 `|
| `app_name` | 1.1&#43; | アプリケーション名（[アプリケーションマニフェスト属性 `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)から） | `My App`|
| `app_memory_usage` | 5.4&#43; | アプリプロセスが使用中のメモリ（MB） | `57` |
| `app_rdns` | 3.0&#43; | 逆DNSアプリケーションID（[ルートマニフェスト属性 `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)から） | `com.example.myapp` |
| `app_version` | 1.1&#43; | アプリケーションバージョン | `version 1.0 `|
| `call_type` | 2.0&#43; | コールタイプ。 | [`view`, `link`] |
| `carrier` | 1.1&#43; | デバイスのモバイルキャリア | `Verizon` |
| `carrier_iso` | 1.1&#43; | キャリアISO国コード| `ISO 3166-1` |
| `carrier_mcc` | 1.1&#43; | モバイル国コード| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 1.1&#43; | モバイルネットワークコード |
| `connection_type` | 1.1&#43; | 接続タイプ | `wifi` |
| `device` | 1.1&#43; | デバイスタイプ。 | iPhone, iPad |
| `device_android_runtime` | 5.4&#43; | Androidランタイムバージョン | `2.1.0` |
| `device_available_external_storage` | 5.4&#43; | デバイス上の利用可能な外部保存の合計 | |
| `device_available_system_storage` | 5.4&#43; | デバイス上の利用可能な保存の合計 |` 273772544` |
| `device_architecture` | 3.0&#43; | デバイスのビットアーキテクチャ | `64` |
| `device_battery_percent` | 4.0&#43; | デバイスの残り電力を整数パーセントで表したもの | `50` |
| `device_cputype` | 3.0&#43; | CPUタイプ | `arm7s` |
| `device_ischarging` | 4.0&#43; | デバイスは充電中ですか？ | [`true`, `false`] |
| `device_language` | 3.0&#43; | 2文字のISO 639-1言語構成識別子 | `en` |
| `device_orientation` | 5.0&#43; | コール時のデバイスの向き | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `device_os_build` | 5.4&#43; | オペレーティングシステムのビルドバージョン | `4499259` |
| `device_os_version` | 5.0&#43; | デバイス上のオペレーティングシステムのバージョン | `7.0` |
| `event_name` | 5.0&#43; | `mobile_link`はvdataに必要 | |
| `library_version` | 1.2&#43; | アプリがインストールしたTealiumライブラリのバージョン | `1.2` |
| `lifecycle_dayofweeklocal*` | 1.2&#43; | コールが行われた週のローカルの曜日 | `1`=日曜日, `2`=月曜日 |
| `lifecycle_dayssincelastwake*` | 1.2&#43; | 最後に検出されたウェイクからの日数（整数で増加） | |
| `lifecycle_dayssincelaunch*` | 1.2&#43; | 最初の起動からの日数（整数で増加） | |
| `lifecycle_dayssinceupdate*` | 1.2&#43; | 最後に検出されたアプリバージョンの更新からの日数（整数で増加） | |
| `lifecycle_diddetectcrash*` | 5.0.3&#43; | 起動イベントでクラッシュが検出されましたか？ | `true` |
| `lifecycle_firstlaunchdate*` | 1.2&#43; | 最初に検出された起動/ウェイクのGMTタイムスタンプ（UTCからのISO 8601形式） | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY*` | 1.2&#43; | MM/DD/YYYY形式でフォーマットされたGMTタイムスタンプ | `01/17/2012` |
| `lifecycle_hourofday_local*` | 1.2&#43; | コールが行われたローカルの日の時間（24時間形式） | |
| `lifecycle_isfirstlaunch*` | 1.2&#43; | コールは最初の起動/ウェイクコールですか？ | [`true`, `false`]  |
| `lifecycle_isfirstlaunchupdate*` | 1.2&#43; | コールは検出された更新後の最初の起動/ウェイクですか？ | [`true`, `false`]  |
| `lifecycle_isfirstwakemonth*` | 1.2&#43; | コールは月の最初の起動/ウェイクですか？ | [`true`, `false`] |
| `lifecycle_isfirstwaketoday*` | 1.2&#43; | コールは日の最初の起動/ウェイクですか？ | [`true`, `false`]  |
| `lifecycle_lastlaunchdate*` | 1.2&#43; | 最後に記録された起動のGMTタイムスタンプ（UTCからのISO 8601形式） | `2013-01-17T17:55:04Z` |
| `lifecycle_lastsleepdate*` | 1.2&#43; | 最後に記録されたスリープのGMTタイムスタンプ（UTCからのISO 8601形式） |`2013-07-11T17:55:04Z` |
| `lifecycle_lastwakedate*` | 1.2&#43; | 最後に記録されたウェイクのGMTタイムスタンプ（UTCからのISO 8601形式） | `2013-07-11T17:55:04Z` |
| `lifecycle_launchcount*` | 1.2&#43; | あなたのアプリのこのバージョンの起動回数の合計（アプリバージョンが更新されるとリセットされます） | |
| `lifecycle_priorsecondsawake*` | 1.2&#43; | 最後の起動からのアプリのスリープ解除秒数（以前のすべてのスリープ解除からの合計を集計し、`lifecycle_type:launch`コールでのみ送信） | |
| `lifecycle_secondsawake*` | 1.2&#43; | 最後のスリープ解除/起動からのアプリのスリープ解除秒数（`lifecycle_type:sleep`でのみ送信） | |
| `lifecycle_sleepcount*` | 1.2&#43; | あなたのアプリがスリープに入った回数の合計（アプリバージョンが更新されるとリセットされます） | |
| `lifecycle_totalcrashcount*` | 5.0.4&#43; | クラッシュが検出された回数の合計。アプリが再インストールされない限りリセットされません | |
| `lifecycle_totallaunchcount*` | 1.2&#43; | インストール以来の起動回数の合計。アプリが再インストールされない限りリセットされません | |
| `lifecycle_totalsecondsawake*`| 1.2&#43; | あなたのアプリがスリープ解除/アクティブ状態にあった秒数の合計（アプリが再インストールされない限りリセットされません） | |
| `lifecycle_totalsleepcount*` | 1.2&#43; | インストール以来、あなたのアプリがバックグラウンドに入った回数の合計（アプリが再インストールされない限りリセットされません） | |
| `lifecycle_totalwakecount*` | 1.2&#43; | インストール以来の起動&#43;スリープ解除の回数の合計（アプリが再インストールされない限りリセットされません） |
| `lifecycle_type*` | 1.2&#43; | ライフサイクルコールのタイプ | [`launch`, `wake`, `sleep`] |
| lifecycle_updatelaunchdate*` | 1.2&#43; | バージョン更新が検出された後の最初のスリープ解除/起動のGMTタイムスタンプ。UTCからのISO 8601形式 | `2013-01-17T17:55:04Z` |
| lifecycle_wakecount* | 1.2&#43; | あなたのアプリのこのバージョンの起動&#43;スリープ解除の回数の合計（アプリバージョンが更新されるとリセットされます） |
| `link_id` | 1.0&#43; | （イベントコールのみ）一般的なイベントまたはリンクタイトル - ボタンタイトルやオブジェクトのTealium IDなど | [任意の文字列] |
| `~orientation~` | 2.0&#43; | **非推奨** コール時のデバイスの向き | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `origin` | 3.0&#43; | モバイルとウェブの実装を区別するためのマッピングで使用される定数 | `mobile` |
| `os_version` | 1.1&#43; | デバイス上のオペレーティングシステムのバージョン | `7.0` |
| `page_type` | 5.0&#43; | モバイルビュー/ページの変更をモバイルまたはウェブイベントから区別するためにマッピングで使用される`mobile_view`定数 - vdataに必要 | |
| `platform` | 1.0&#43; | モバイルプラットフォーム | `Android` |
| `screen_title` | 1.0&#43; | （ビューコールのみ）一般的なビュータイトル | [任意の文字列] |
| `timestamp` | 1.1&#43; | イベント発生の秒単位のタイムスタンプ [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | 2.0&#43; | イベント発生のローカルタイムスタンプ（秒単位）（ISO 8601形式、オフセットなし） | `2013-07-11T19:57:47` |
| `timestamp_offset` | 2.0&#43; | デバイスの位置のローカルタイムゾーンオフセット（時間単位） | `-3` |
| `timestamp_unix` | 1.1&#43; | イベント発生のGMT/UTC Unixタイムスタンプ |`1373498679` |
| `timestamp_unix_milliseconds` | 5.5.1 | イベント発生のGMT/UTC Unixタイムスタンプ（ミリ秒単位） | `1373498679123` |
| `uuid` | 1.2&#43; | （Universally Unique Identifier）各アプリのインストールごとにユニーク | [任意の文字列] |
| `visitor_id` | 5.0&#43; | Tealiumが生成した訪問ID | |