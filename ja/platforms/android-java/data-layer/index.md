---
title: データレイヤー
description: Androidライブラリのデータレイヤー変数について説明します。
url: https://docs.tealium.com/ja/platforms/android-java/data-layer/
---以下の変数は、モバイルデータレイヤーの一部としてTealium Androidライブラリによって構成されます。これらの変数は、ライブラリからの各トラッキング呼び出しに自動的に含まれ、Tealium Customer Data Hubの構成で使用できます。


<blockquote>
これらの変数は、[モバイル用にプロファイルを有効化](https://docs.tealium.com/create-mobile-profile/)すると、Tag Managementアカウントに追加されます。
</blockquote>


5.0.xでは、[ライフサイクルトラッキングモジュール](https://docs.tealium.com/ja/platforms/android/lifecycle-tracking-module/)で追加の変数を使用できます。

| 変数名 | Androidバージョン | 説明 | 例 |
| --- | --- | --- | --- |
| `app_build` | 5.4+ | アプリのビルドバージョン | `1 `|
| `app_name` | 1.1+ | アプリケーション名（[アプリケーションマニフェスト属性 `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)から取得） | `My App`|
| `app_memory_usage` | 5.4+ | アプリプロセスが使用しているメモリ（MB） | `57` |
| `app_rdns` | 3.0+ | 逆引きDNS形式のアプリケーションID（[ルートマニフェスト属性 `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)から取得） | `com.example.myapp` |
| `app_version` | 1.1+ | アプリケーションのバージョン | `version 1.0 `|
| `call_type` | 2.0+ | 呼び出しタイプ。 | [`view`, `link`] |
| `carrier` | 1.1+ | デバイスのモバイル通信事業者 | `Verizon` |
| `carrier_iso` | 1.1+ | 通信事業者のISO国コード | `ISO 3166-1` |
| `carrier_mcc` | 1.1+ | モバイル国コード | `ITU-T Recommendation E.212` |
| `carrier_mnc` | 1.1+ | モバイルネットワークコード |
| `connection_type` | 1.1+ | 接続タイプ | `wifi` |
| `device` | 1.1+ | デバイスタイプ。 | iPhone、iPad |
| `device_android_runtime` | 5.4+ | Android Runtimeのバージョン | `2.1.0` |
| `device_available_external_storage` | 5.4+ | デバイスで利用可能な外部保存の合計容量 | |
| `device_available_system_storage` | 5.4+ | デバイスで利用可能な保存の合計容量 |` 273772544` |
| `device_architecture` | 3.0+ | デバイスのビットアーキテクチャ | `64` |
| `device_battery_percent` | 4.0+ | デバイスのバッテリー残量を整数のパーセント値で表したもの | `50` |
| `device_cputype` | 3.0+ | CPUタイプ | `arm7s` |
| `device_ischarging` | 4.0+ | デバイスが現在充電中かどうか | [`true`, `false`] |
| `device_language` | 3.0+ | 2文字のISO 639-1言語構成識別子 | `en` |
| `device_orientation` | 5.0+ | 呼び出し時のデバイスの向き | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `device_os_build` | 5.4+ | オペレーティングシステムのビルドバージョン | `4499259` |
| `device_os_version` | 5.0+ | デバイスのオペレーティングシステムバージョン | `7.0` |
| `event_name` | 5.0+ | vdataで必須の`mobile_link` | |
| `library_version` | 1.2+ | アプリにインストールされているTealiumライブラリのバージョン | `1.2` |
| `lifecycle_dayofweeklocal*` | 1.2+ | 呼び出しが行われた現地の曜日 | `1`=日曜日、`2`=月曜日 |
| `lifecycle_dayssincelastwake*` | 1.2+ | 最後に検出されたウェイクからの日数（整数単位） | |
| `lifecycle_dayssincelaunch*` | 1.2+ | 初回起動からの日数（整数単位） | |
| `lifecycle_dayssinceupdate*` | 1.2+ | 最後に検出されたアプリバージョンの更新からの日数（整数単位） | |
| `lifecycle_diddetectcrash*` | 5.0.3+ | 起動イベント時にクラッシュがあったと判定されたかどうか | `true` |
| `lifecycle_firstlaunchdate*` | 1.2+ | 最初に検出された起動／ウェイクのGMTタイムスタンプ（UTCを基準としたISO 8601形式） | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY*` | 1.2+ | MM/DD/YYYY形式のGMTタイムスタンプ | `01/17/2012` |
| `lifecycle_hourofday_local*` | 1.2+ | 呼び出しが行われた現地時刻の時間（24時間形式） | |
| `lifecycle_isfirstlaunch*` | 1.2+ | 呼び出しが初回の起動／ウェイク呼び出しかどうか | [`true`, `false`]  |
| `lifecycle_isfirstlaunchupdate*` | 1.2+ | 呼び出しが、更新の検出後における最初の起動／ウェイクかどうか | [`true`, `false`]  |
| `lifecycle_isfirstwakemonth*` | 1.2+ | 呼び出しがその月の最初の起動／ウェイクかどうか | [`true`, `false`] |
| `lifecycle_isfirstwaketoday*` | 1.2+ | 呼び出しがその日の最初の起動／ウェイクかどうか | [`true`, `false`]  |
| `lifecycle_lastlaunchdate*` | 1.2+ | 最後に記録された起動のGMTタイムスタンプ（UTCを基準としたISO 8601形式） | `2013-01-17T17:55:04Z` |
| `lifecycle_lastsleepdate*` | 1.2+ | 最後に記録されたスリープのGMTタイムスタンプ（UTCを基準としたISO 8601形式） |`2013-07-11T17:55:04Z` |
| `lifecycle_lastwakedate*` | 1.2+ | 最後に記録されたウェイクのGMTタイムスタンプ（UTCを基準としたISO 8601形式） | `2013-07-11T17:55:04Z` |
| `lifecycle_launchcount*` | 1.2+ | 現在のアプリバージョンにおける起動回数の合計（アプリのバージョンが更新されるとリセット） | |
| `lifecycle_priorsecondsawake*` | 1.2+ | 前回の起動以降にアプリがアウェイク状態だった秒数の整数値（以前のすべてのウェイクからの合計を集計し、`lifecycle_type:launch`呼び出しでのみ送信） | |
| `lifecycle_secondsawake*` | 1.2+ | 前回のウェイク／起動以降にアプリがアウェイク状態だった秒数の整数値（`lifecycle_type:sleep`でのみ送信） | |
| `lifecycle_sleepcount*` | 1.2+ | アプリがスリープ状態になった回数の合計（アプリのバージョンが更新されるとリセット） | |
| `lifecycle_totalcrashcount*` | 5.0.4+ | クラッシュが検出された回数の合計。アプリを再インストールしない限りリセットされません | |
| `lifecycle_totallaunchcount*` | 1.2+ | インストール後の起動回数の合計。アプリを再インストールしない限りリセットされません | |
| `lifecycle_totalsecondsawake*`| 1.2+ | アプリがウェイク／アクティブ状態だった秒数の合計（アプリを再インストールしない限りリセットされません） | |
| `lifecycle_totalsleepcount*` | 1.2+ | インストール後にアプリがバックグラウンドへ移行した回数の合計（アプリを再インストールしない限りリセットされません） | |
| `lifecycle_totalwakecount*` | 1.2+ | インストール後の起動回数とウェイク回数の合計（アプリを再インストールしない限りリセットされません） |
| `lifecycle_type*` | 1.2+ | ライフサイクル呼び出しのタイプ | [`launch`, `wake`, `sleep`] |
| lifecycle_updatelaunchdate*` | 1.2+ | バージョン更新が検出された後の最初のウェイク／起動のGMTタイムスタンプ。UTCを基準としたISO 8601形式 | `2013-01-17T17:55:04Z` |
| lifecycle_wakecount* | 1.2+ | 現在のアプリバージョンにおける起動回数とウェイク回数の合計（アプリのバージョンが更新されるとリセット） |
| `link_id` | 1.0+ | （イベント呼び出しのみ）一般的なイベント名またはリンクタイトル（ボタンのタイトルやオブジェクトのTealium IDなど） | [任意の文字列] |
| `~orientation~` | 2.0+ | **非推奨** 呼び出し時のデバイスの向き | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `origin` | 3.0+ | モバイル実装とWeb実装を区別するためにマッピングで使用される定数 | `mobile` |
| `os_version` | 1.1+ | デバイスのオペレーティングシステムバージョン | `7.0` |
| `page_type` | 5.0+ | モバイルビュー／ページ変更をモバイルまたはWebイベントと区別するためにマッピングで使用される`mobile_view`定数。vdataで必須 | |
| `platform` | 1.0+ | モバイルプラットフォーム | `Android` |
| `screen_title` | 1.0+ | （ビュー呼び出しのみ）一般的なビュータイトル | [任意の文字列] |
| `timestamp` | 1.1+ | イベント発生時刻を秒単位で示すタイムスタンプ［UTCのISO 8601形式］ | `2013-07-11T19:57:47Z` |
| `timestamp_local` | 2.0+ | イベント発生時刻を秒単位で示すローカルタイムスタンプ（オフセットなしのISO 8601形式） | `2013-07-11T19:57:47` |
| `timestamp_offset` | 2.0+ | デバイス所在地のローカルタイムゾーンオフセット（時間単位） | `-3` |
| `timestamp_unix` | 1.1+ | イベント発生時刻のGMT/UTC Unixタイムスタンプ |`1373498679` |
| `timestamp_unix_milliseconds` | 5.5.1 | イベント発生時刻のGMT/UTC Unixタイムスタンプ（ミリ秒単位） | `1373498679123` |
| `uuid` | 1.2+ | （汎用一意識別子）デバイスへのアプリのインストールごとに一意 | [任意の文字列] |
| `visitor_id` | 5.0+ | Tealiumによって生成された訪問ID | |