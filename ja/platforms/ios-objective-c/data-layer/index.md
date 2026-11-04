---
title: データレイヤー
description: Tealium iOSライブラリのバージョン4.xと5.xの違い、および最新バージョンへの移行方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/data-layer/
---以下の変数は、モバイルデータレイヤーの一部としてTealium iOSライブラリによって構成されます。これらの変数は、ライブラリからの各トラッキング呼び出しに自動的に含まれ、iQまたはEventStreamの構成で使用されます。

5.0.xでは、[ライフサイクルトラッキングモジュール](https://docs.tealium.com/ja/platforms/ios-objective-c/module-list/lifecycle-tracking/)で追加の変数を使用できます。

| 変数 | iOSバージョン | 説明 | 例 |
| --- | --- | --- | --- |
| `app_name` | 1.0+ | アプリケーション名。 | ［任意の文字列］ |
| `app_rdns` | 3.2+ | 逆引きDNS形式のバンドルID／パッケージID。 | `com.tealium.sampleApp` |
| `app_uuid` | 5.1+ | （Universally Unique Identifier：汎用一意識別子）デバイスにアプリをインストールするたびに一意となる識別子（以前のuuid）。 | ［任意の文字列］ |
| `app_version` | 1.0+ | アプリケーションのバージョン。 | ［任意の文字列］ |
| `call_type` | 2.2+ | 呼び出しタイプ。 | [`view`, `link`]|
| `carrier` | 2.0+ | デバイスが現在接続している通信事業者。 | `Verizon` |
| `carrier_iso` | 2.2+ | 通信事業者のISO国コード。 | `ISO 3166-1` |
| `carrier_mcc` | 2.2+ | モバイル国コード。| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 2.2+ | モバイルネットワークコード。 | |
| `connection_type` | 1.0+ | 接続タイプ。 | `wifi`|
| `device` | 1.0+ | iPhone。 |
| `device_architecture` | 3.2+ | デバイスのビットアーキテクチャ。 |`64` |
| `device_battery_percent` | 4.0+ | デバイスのバッテリー残量を整数のパーセント値で表したもの。 |`50` |
| `device_cputype` | 3.2+ | CPUタイプ。 | `arm7s` |
| `device_ischarging` | 4.0+ | デバイスが現在充電中かどうか。 | [`true`, `false`] |
| `device_language` | 3.2+ | 2文字のISO 639-1言語構成識別子。 |`en` |
| `device_orientation` | 5.0+ | 呼び出し時のデバイスの向き。 | `Portrait`、`Landscape Left`、`Landscape Right`、`Portrait UpsideDown`、`Face Up`、`Face Down`、または`Unknown` |
| `device_os_version` | 5.0+ | デバイスのオペレーティングシステムのバージョン。| `7.0` |
| `event_name` | 5.0+ | vdataで必須の`mobile_link`。 | ［任意の文字列］|
| `library_version` | 2.0+ | アプリにインストールされているTealiumライブラリのバージョン。 | |
| `link_id` | 1.0+ | （イベント呼び出しのみ）ボタンのタイトルやオブジェクトのTealium IDなど、一般的なイベントまたはリンクのタイトル。 | ［任意の文字列］ |
| `~~orientation~~` | 2.0+ | **非推奨** 呼び出し時のデバイスの向き。 | `Portrait`、`Landscape Left`、`Landscape Right`、`Portrait UpsideDown`、`Face Up`、`Face Down`、または`Unknown` |
| `origin` | 3.2+ | モバイル実装とWeb実装を区別するためにマッピングで使用される定数。 | `mobile` |
| `os_version` | 1.0+ | デバイスのオペレーティングシステムのバージョン。 | `7.0` |
| `page_type` | 5.0+ | モバイルビュー／ページの変更をモバイルまたはWebイベントと区別するためにマッピングで使用される「mobile_view」定数。vdataで必須。 | |
| `platform` | 1.0+ | デバイスのプラットフォーム。 | `iOS` |
| `screen_title` | 1.0+ | （ビュー呼び出しのみ）一般的なビューのタイトル。 | ［任意の文字列］ |
| `timestamp` | 2.0+ | イベント発生時刻の秒単位のタイムスタンプ。 | `2013-07-11T19:57:47Z`［UTCのISO 8601］ |
| `timestamp_local` | 2.2+ | イベント発生時刻の秒単位のローカルタイムスタンプ。 | `2013-07-11T19:57:47`［オフセットなしのISO 8601］ |
| `timestamp_offset` | 2.2+ | デバイスの所在地におけるローカルタイムゾーンのオフセット（時間単位）。 | `-3` |
| `timestamp_unix` | 2.2+ | 任意の事象に対するGMT／UTCのUnixタイムスタンプ。 | `1373498679` |
| `timestamp_unix_milliseconds` |  5.4.5+ | イベント発生時刻のミリ秒単位のGMT／UTC Unixタイムスタンプ。 | `1373498679123` |
| `visitor_id` | 5.0+ | Tealiumによって生成された訪問ID。 | |
| `was_queued` | 4.1+ | このディスパッチが送信前にキューへ追加されたか、バッチ処理されたかを示します。 | [`true`, `false`] |