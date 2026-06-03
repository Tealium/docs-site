---
title: コレクターモジュール
description: Tealium Kotlinライブラリで利用可能なさまざまなデータコレクターについて学び、アプリに組み込みましょう。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/
---
## 使用方法

コレクターモジュールはコアライブラリで利用可能です。各コレクターモジュールから収集されたデータはデータレイヤーに追加され、各トラックコールで送信されます。これらのコレクターの使用は推奨されますが、必須ではありません。コレクターを除外すると、そのコレクターに関連するデータ変数がデータレイヤーから省略されます。

アプリ実装にコレクターモジュールを追加するには、`TealiumConfig`インスタンスを作成する際に`collectors`パラメータを追加します：

```kotlin
val config = TealiumConfig(application,
                 &#34;ACCOUNT&#34;,
                 &#34;PROFILE&#34;,
                 Environment.DEV,
                 collectors = mutableSetOf(
                     Collectors.Tealium,
                     Collectors.Time,
                     Collectors.App,
                     Collectors.Device,
                     Collectors.Connectivity
                 )
          )
```

### Tealium コレクター

Tealiumアカウントに関する情報を収集します。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `tealium_account` | `TealiumConfig`からのTealiumアカウント名 | `tealium` |
| `tealium_profile` | `TealiumConfig`からのTealiumプロファイル名 | `mobile` |
| `tealium_environment` | `TealiumConfig`からのTealium環境 | `dev` |
| `tealium_datasource`| `TealiumConfig`からのTealiumデータソース名 | `abc123` |
| `tealium_visitor_id` | Tealium訪問ID | `t3aL...1uM` |
| `tealium_random` | 各イベントのランダムな数値 | `1234567890` |
| `was_queued` | このイベントがデバイス上でキューに入れられたかどうかを示します | `true` |

### アプリ コレクター

アプリパッケージに関する情報を収集します。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `app_build` | アプリのビルドバージョン | `1`|
| `app_name` | アプリケーション名（[アプリケーションマニフェスト属性 `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)から） | `My App`|
| `app_memory_usage` | アプリプロセスによって使用されるメモリ（MB） | `57` |
| `app_rdns` | [ルートマニフェスト属性 `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)からの逆DNSアプリケーションID | `com.example.myapp` |
| `app_uuid` | ランダムな`uuid`。永続的な保存モジュールのいずれかが有効になっている限り、アプリのインストール期間中に持続します。アプリがアンインストールされるとリセットされます。 | `123e4567-e89b-12d3-a456-556642440000`|
| `app_version` | アプリケーションバージョン | `version 1.0`|

### 接続性 コレクター

デバイスのネットワークとキャリアに関する情報を収集します。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `carrier` | デバイスのモバイルキャリア | `Verizon` |
| `carrier_iso` | キャリアISO国コード| `gb` |
| `carrier_mcc` | モバイル国コード| `ITU-T Recommendation E.212` |
| `carrier_mnc` | モバイルネットワークコード | `34` |
| `connection_type` | 接続タイプ | `wifi` |

### デバイス コレクター

ユーザーのデバイスに関する情報を収集します。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `device` | 小売デバイス名（メーカー&#43;モデル） | `Google Pixel 8`, `Sony Xperia 1 V` |
| `device_android_runtime` | Androidランタイムバージョン | `2.1.0` |
| `device_architecture` | デバイスのビットアーキテクチャ | `64` |
| `device_battery_percent` | デバイスの残り電力の整数パーセンテージ表現 | `50` |
| `device_cputype` | CPUタイプ | `arm7s` |
| `device_free_external_storage` | デバイスの利用可能な外部保存の合計 | |
| `device_free_system_storage` | デバイスの利用可能な保存の合計 |`273772544` |
| `device_ischarging` | デバイスが充電中かどうかを示します | `true`, `false` |
| `device_language` | 2文字のISO 639-1言語構成識別子 | `en` |
| `device_logical_resolution` | ポイントでの論理画面解像度（幅x高さ） | `414x896` |
| `device_manufacturer` | 製品/ハードウェアの製造元 | `Google`, `Sony` |
| `device_model` | 最終製品のエンドユーザーに見える名前 | `Pixel 8`, `Xperia 1 V` |
| `device_orientation` | コール時のデバイスの向き | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown` |
| `device_os_build` | オペレーティングシステムのビルドバージョン | `4499259` |
| `device_os_version` | デバイスのオペレーティングシステムバージョン | `7.0` |
| `device_resolution` | ピクセルでのディスプレイ解像度サイズ | `1920x1080` |
| `origin` | モバイルとウェブの実装を区別するために使用される定数 | `mobile` |
| `os_name` | オペレーティングシステムの名前 | `Android` |
| `platform` | モバイルプラットフォーム | `android` |

### 時間 コレクター

トラックコールが発生したときのタイムスタンプ情報を収集します。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `timestamp` | イベント発生の秒単位のタイムスタンプ [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | イベント発生の秒単位のローカルタイムスタンプ (ISO 8601 without offset) | `2013-07-11T19:57:47` |
| `timestamp_offset` | デバイスの位置のローカルタイムゾーンオフセット（時間単位） | `-3` |
| `timestamp_unix` | イベント発生のGMT/UTC Unixタイムスタンプ |`1373498679` |
| `timestamp_unix_milliseconds` | イベント発生のGMT/UTC Unixタイムスタンプ（ミリ秒単位） | `1373498679123` |