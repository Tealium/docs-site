---
title: データレイヤー
description: Tealium for iOSライブラリのバージョン4.xと5.xの違いを学び、最新バージョンへの移行方法を理解します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/data-layer/
---以下の変数は、モバイルデータレイヤーの一部としてTealium iOSライブラリによって自動的に追加されます。これらの変数は、ライブラリからの各トラッキングコールに自動的に含まれ、iQまたはTealium EventStreamの構成で使用されます。

追加の変数は、5.0.x用の[Lifecycle Tracking Module](/ja/platforms/ios-objective-c/module-list/lifecycle-tracking/)で利用可能です。

| 変数 | iOSバージョン | 説明 | 例 |
| --- | --- | --- | --- |
| `app_name` | 1.0&#43; | アプリケーション名。 | [任意の文字列] |
| `app_rdns` | 3.2&#43; | リバースDNSバンドルID/パッケージID。 | `com.tealium.sampleApp` |
| `app_uuid` | 5.1&#43; | (ユニバーサルユニークID) アプリの各インストールに対してユニーク（以前はuuid）。 | [任意の文字列] |
| `app_version` | 1.0&#43; | アプリケーションバージョン。 | [任意の文字列] |
| `call_type` | 2.2&#43; | コールタイプ。 | [`view`, `link`]|
| `carrier` | 2.0&#43; | 現在のデバイスのキャリア。 | `Verizon` |
| `carrier_iso` | 2.2&#43; | キャリアのISO国コード。 | `ISO 3166-1` |
| `carrier_mcc` | 2.2&#43; | モバイル国コード。| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 2.2&#43; | モバイルネットワークコード。 | |
| `connection_type` | 1.0&#43; | 接続タイプ。 | `wifi`|
| `device` | 1.0&#43; | iphone |
| `device_architecture` | 3.2&#43; | デバイスのビットアーキテクチャ。 |`64` |
| `device_battery_percent` | 4.0&#43; | デバイスの残り電力をパーセントで表した整数。 |`50` |
| `device_cputype` | 3.2&#43; | CPUタイプ。 | `arm7s` |
| `device_ischarging` | 4.0&#43; | デバイスは充電中ですか？ | [`true`, `false`] |
| `device_language` | 3.2&#43; | 2文字のISO 639-1言語構成識別子。 |`en` |
| `device_orientation` | 5.0&#43; | コール時のデバイスの向き。 | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, または `Unknown` |
| `device_os_version` | 5.0&#43; | デバイスのオペレーティングシステムバージョン。| `7.0` |
| `event_name` | 5.0&#43; | `mobile_link`はvdataに必要。 | [任意の文字列]|
| `library_version` | 2.0&#43; | アプリがインストールしたTealiumライブラリのバージョン。 | |
| `link_id` | 1.0&#43; | (EVENT CALLS ONLY) 一般的なイベントまたはリンクタイトル - ボタンタイトルやオブジェクトのTealium IDなど。 | [任意の文字列] |
| `~~orientation~~` | 2.0&#43; | **非推奨** コール時のデバイスの向き。 | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, または `Unknown` |
| `origin` | 3.2&#43; | モバイルとウェブの実装を区別するためのマッピングで使用される定数。  | `mobile` |
| `os_version` | 1.0&#43; | デバイスのオペレーティングシステムバージョン。 | `7.0` |
| `page_type` | 5.0&#43; | &#34;mobile_view&#34;は、モバイルビュー/ページの変更をモバイルまたはウェブイベントから区別するためのマッピングで使用される定数 - vdataに必要。 | |
| `platform` | 1.0&#43; | デバイスのプラットフォーム | `iOS` |
| `screen_title` | 1.0&#43; | (VIEW CALLS ONLY) 一般的なビュータイトル。 | [任意の文字列] |
| `timestamp` | 2.0&#43; | イベント発生のタイムスタンプ（秒）。 | `2013-07-11T19:57:47Z` [ISO 8601 at UTC] |
| `timestamp_local` | 2.2&#43; | イベント発生のローカルタイムスタンプ（秒）。 | `2013-07-11T19:57:47` [ISO 8601 without offset] |
| `timestamp_offset` | 2.2&#43; | デバイスの位置のローカルタイムゾーンオフセット（時間）。 | `-3` |
| `timestamp_unix` | 2.2&#43; | 任意の発生のGMT/UTC Unixタイムスタンプ。 | `1373498679` |
| `timestamp_unix_milliseconds` |  5.4.5&#43; |  イベント発生のGMT/UTC Unixタイムスタンプ（ミリ秒）。 | `1373498679123` |
| `visitor_id` | 5.0&#43; | Tealiumが生成した訪問ID。 | |
| `was_queued` | 4.1&#43; | このディスパッチは送信前にキューまたはバッチされましたか？ | [`true`, `false`] |
