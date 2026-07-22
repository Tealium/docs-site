---
title: データレイヤー
description: Tealium for iOSライブラリのバージョン4.xと5.xの違いを学び、最新バージョンへの移行方法を理解します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/data-layer/
---以下の変数は、モバイルデータレイヤーの一部としてTealium iOSライブラリによって自動的に追加されます。これらの変数は、ライブラリからの各トラッキングコールに自動的に含まれ、iQまたはTealium EventStreamの構成で使用されます。

追加の変数は、5.0.x用の[Lifecycle Tracking Module](https://docs.tealium.com/ja/platforms/ios-objective-c/module-list/lifecycle-tracking/)で利用可能です。

| 変数 | iOSバージョン | 説明 | 例 |
| --- | --- | --- | --- |
| `app_name` | 1.0+ | アプリケーション名。 | [任意の文字列] |
| `app_rdns` | 3.2+ | リバースDNSバンドルID/パッケージID。 | `com.tealium.sampleApp` |
| `app_uuid` | 5.1+ | (ユニバーサルユニークID) アプリの各インストールに対してユニーク（以前はuuid）。 | [任意の文字列] |
| `app_version` | 1.0+ | アプリケーションバージョン。 | [任意の文字列] |
| `call_type` | 2.2+ | コールタイプ。 | [`view`, `link`]|
| `carrier` | 2.0+ | 現在のデバイスのキャリア。 | `Verizon` |
| `carrier_iso` | 2.2+ | キャリアのISO国コード。 | `ISO 3166-1` |
| `carrier_mcc` | 2.2+ | モバイル国コード。| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 2.2+ | モバイルネットワークコード。 | |
| `connection_type` | 1.0+ | 接続タイプ。 | `wifi`|
| `device` | 1.0+ | iphone |
| `device_architecture` | 3.2+ | デバイスのビットアーキテクチャ。 |`64` |
| `device_battery_percent` | 4.0+ | デバイスの残り電力をパーセントで表した整数。 |`50` |
| `device_cputype` | 3.2+ | CPUタイプ。 | `arm7s` |
| `device_ischarging` | 4.0+ | デバイスは充電中ですか？ | [`true`, `false`] |
| `device_language` | 3.2+ | 2文字のISO 639-1言語構成識別子。 |`en` |
| `device_orientation` | 5.0+ | コール時のデバイスの向き。 | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, または `Unknown` |
| `device_os_version` | 5.0+ | デバイスのオペレーティングシステムバージョン。| `7.0` |
| `event_name` | 5.0+ | `mobile_link`はvdataに必要。 | [任意の文字列]|
| `library_version` | 2.0+ | アプリがインストールしたTealiumライブラリのバージョン。 | |
| `link_id` | 1.0+ | (EVENT CALLS ONLY) 一般的なイベントまたはリンクタイトル - ボタンタイトルやオブジェクトのTealium IDなど。 | [任意の文字列] |
| `~~orientation~~` | 2.0+ | **非推奨** コール時のデバイスの向き。 | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, または `Unknown` |
| `origin` | 3.2+ | モバイルとウェブの実装を区別するためのマッピングで使用される定数。  | `mobile` |
| `os_version` | 1.0+ | デバイスのオペレーティングシステムバージョン。 | `7.0` |
| `page_type` | 5.0+ | "mobile_view"は、モバイルビュー/ページの変更をモバイルまたはウェブイベントから区別するためのマッピングで使用される定数 - vdataに必要。 | |
| `platform` | 1.0+ | デバイスのプラットフォーム | `iOS` |
| `screen_title` | 1.0+ | (VIEW CALLS ONLY) 一般的なビュータイトル。 | [任意の文字列] |
| `timestamp` | 2.0+ | イベント発生のタイムスタンプ（秒）。 | `2013-07-11T19:57:47Z` [ISO 8601 at UTC] |
| `timestamp_local` | 2.2+ | イベント発生のローカルタイムスタンプ（秒）。 | `2013-07-11T19:57:47` [ISO 8601 without offset] |
| `timestamp_offset` | 2.2+ | デバイスの位置のローカルタイムゾーンオフセット（時間）。 | `-3` |
| `timestamp_unix` | 2.2+ | 任意の発生のGMT/UTC Unixタイムスタンプ。 | `1373498679` |
| `timestamp_unix_milliseconds` |  5.4.5+ |  イベント発生のGMT/UTC Unixタイムスタンプ（ミリ秒）。 | `1373498679123` |
| `visitor_id` | 5.0+ | Tealiumが生成した訪問ID。 | |
| `was_queued` | 4.1+ | このディスパッチは送信前にキューまたはバッチされましたか？ | [`true`, `false`] |
