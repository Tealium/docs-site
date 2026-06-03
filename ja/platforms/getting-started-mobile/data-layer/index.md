---
title: データレイヤー
description: モバイルインストールで利用可能なデータレイヤー変数のリスト。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/data-layer/
---
各モバイルコンポーネントはデータレイヤーに変数を追加します。以下のセクションでは、各モジュールのすべての変数をリストアップします。

すべての値は文字列に変換されます。ただし、必要に応じてiQ拡張機能やTealium EventStreamの機能を使用して数値型に強制変換することができます。

 すべての自動追跡イベントは属性を構成します: `autotracked=&#34;true&#34;` 

## アプリデータ

ホストアプリケーションのプロパティ。

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `app_name` | `String` | アプリケーション名 | `&#34;Digital Velocity&#34;` |
| `app_rdns` | `String` | リバースDNSバンドルID/パッケージ名 | `&#34;com.digitalvelocity.alpha&#34;` |
| `app_version` | `String` | アプリケーションバージョン |  `&#34;1.2.0&#34;` |

## Collect

プラットフォームのネイティブURL通信サービスを使用して、TealiumのCollectサービスにトラッキングコールをネットワークリクエストとして送信します。

| イベント属性 | タイプ | 値 |
| :-- | :-- | :-- |
| `dispatch_service` | `String` | `&#34;collect&#34;` |

## キャリアデータ

モバイルキャリアに関する情報を提供します。

| イベント属性 | タイプ | 説明 |例 |
| :-- | :-- | :-- | :-- |
| `carrier` | `String` |キャリアの名前 |`&#34;AT&amp;T&#34;` |
| `carrier_iso` | `String` |キャリアのISO 3166-1国コード  |`&#34;us&#34;` |
| `carrier_mcc` | `String` |モバイルITU-T E.212国コード | `&#34;us&#34;` |
| `carrier_mnc` | `String` |モバイルネットワークコード  | `&#34;410&#34;` |

## 同意管理

同意追跡の構成に関する情報を提供します。

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `policy` | `String` |同意が収集されたポリシー |`&#34;gdpr&#34;` |
| `consent_status` | `String` |ユーザーの現在の同意状態 |`&#34;consented&#34;` |
| `consent_categories` | `[String]` |ユーザーが選択した同意カテゴリの配列 | `[&#34;analytics&#34;, &#34;cdp&#34;]` |


## デバイスデータ

ホストデバイスに関する情報を提供します。

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `device` |`String` | デバイスの名前 |`&#34;iPhone 6s&#34;` |
| `device_architecture` |`Number` | デバイスのビットアーキテクチャ（32, 64など）| `64` |
| `device_advertising_id` |`String` | オプションの広告識別子。すべてのデバイスで自動的に利用可能ではありません |`&#34;03402320-245A-4ED4-BEAE-A1F50E21C55E&#34;` |
| `device_battery_percent` |`Number` | デバイスの残りバッテリー電力の全数値表現| `100` |
| `device_cputype` | `String` |中央処理装置タイプ（arm6, arm7など） |`&#34;ARM64&#34;` |
| `device_ischarging ` | `String` |デバイスがアクティブに充電中かどうか（true/false）| `&#34;false&#34;` |
| `device_language ` | `String` |2文字のIOS-639-1言語識別子（en, jaなど） |`&#34;en&#34;` |
| `device_orientation` | `String` |イベント時のデバイスの向き（縦、横など）  |`&#34;Portrait&#34;` |
| `device_resolution ` | `String` | デバイスの解像度 |`&#34;750x1334&#34;` |



## ライフサイクルイベント

次のアプリケーションライフサイクルイベントの自動追跡を提供します：起動、起床、睡眠。

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `lifecycle_ dayofweek_local` | `Number` |地元の曜日（1=日曜日、2=月曜日など） | `3` |
| `lifecycle_ dayssincelaunch` | `Number` | 最初の起動からの日数（全数値増分） | `0` (24時間はまだ経過していません) |
| `lifecycle_ dayssinceupdate` | `String` |アプリが更新されてからの日数（全数値増分）|`&#34;1&#34;` |
| `lifecycle_ diddetectcrash` | `String` | 起動時にクラッシュが検出されたかどうか  |`&#34;true&#34;` |
| `lifecycle_ firstlaunchdate` | `String` |最初に検出された起動のGMTタイムスタンプ（UTCのISO 8601形式） | `&#34;2016-05-16T16:32:04Z&#34;` |
| `lifecycle_ firstlaunchdate_ MMDDYYYY` | `String` |最初に検出された起動のGMTタイムスタンプ（MM/DD/YYYY形式） |`&#34;5/16/2016&#34;` |
| `lifecycle_ hourofday_local` | `Number` |地元の時間（24時間形式）  | `13` |
| `lifecycle_ isfirstlaunch` | `String` |起動が最初である場合は`&#34;true&#34;`（それ以外の場合は未構成）|  `&#34;true&#34;` |
| `lifecycle_ isfirstlaunchupdate` | `String` |検出されたアプリバージョン更新後の最初の起動である場合は`&#34;true&#34;`（それ以外の場合は未構成） |`&#34;true&#34;` |
| `lifecycle_ isfirstwakemonth` | `String` |起動イベントがその月の最初である場合は`&#34;true&#34;`（それ以外の場合は未構成） | `&#34;true&#34;` |
| `lifecycle_ isfirstwaketoday ` | `String` |起動/起床イベントがその日の最初である場合は`&#34;true&#34;`（それ以外の場合は未構成） | `&#34;true&#34;` |
| `lifecycle_ lastlaunchdate ` | `String` |以前に記録された起動のGMTタイムスタンプ（UTCのISO 8601形式）（最初のセッション内であれば未構成） | `&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ lastsleepdate ` | `String` |以前に記録された睡眠イベントのGMTタイムスタンプ（UTCのISO 8601形式） |`&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ lastwakedate ` | `String` |以前に記録された起床イベントのGMTタイムスタンプ（UTCのISO 8601形式） |`&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ launchcount ` | `Number` |最新バージョン更新以降のアプリケーションの起動回数の合計（新しいバージョンが検出されるとリセットされます） |`3` |
| `lifecycle_ priorsecondsawake` | `Number` |起動イベント中にのみ構成されます。起床と睡眠の間にアプリケーションが起動していた全秒数。起動イベントまでのこれらの起床と睡眠の合計。 | `148` |
| `lifecycle_ secondsawake ` | `Number` |睡眠イベント中にのみ構成されます。最近の起床から睡眠イベントまでのアプリケーションが起動していた全秒数。  |`480` |
| `lifecycle_ sleepcount ` | `Number` |アプリが背景に移動したり、睡眠状態になったと検出された回数の合計。  |`3` |
| `lifecycle_ totallaunchcount` | `Number` |アプリがインストールされてからの起動回数の合計。アプリが削除されて再インストールされない限りリセットされません。  |`5` |
| `lifecycle_ totalsecondsawake ` | `Number` |アプリケーションが起動していた秒数の合計。アプリが削除されて再インストールされない限りリセットされません。  |`800` |
| `lifecycle_ totalsleepcount ` | `Number` |アプリケーションが睡眠状態になった回数の合計。アプリが削除されて再インストールされない限りリセットされません。 |`8` |
| `lifecycle_ totalcrashcount` | `Number` |アプリケーションが適切に睡眠イベントを記録できなかったため、クラッシュによってライフサイクルシーケンスの不一致が発生した回数の合計。アプリが削除されて再インストールされない限りリセットされません。  |`2` |
| `lifecycle_ totalwakecount ` | `Number` |起動と起床の合計回数。アプリが削除されて再インストールされない限りリセットされます。  |`7` |
| `lifecycle_type`  | `String` |ライフサイクルイベントタイプ |  [`&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;`] |
| `lifecycle_ updatelaunchdate` | `String` |アプリバージョン更新が検出された後の最初の起動/起床のGMTタイムスタンプ。UTCのISO 8601形式。|`&#34;2016-05-16T16:32:04Z&#34;` |
| `lifecycle_ wakecount` | `Number` |このアプリバージョンの起動と起床の合計回数。新しいホストアプリケーションバージョンが検出された場合にリセットされます。 |`34` |


## オフラインキューイング

たとえば、デバイスが一時的にネットワーク接続を失った場合に、後で配信するためにイベントディスパッチデータを保存します。

キューに入れられたディスパッチデータ内の次のイベント属性を構成します：

| イベント属性 | 値 |
| :-- | :-- |
| `was_queued` | `&#34;true&#34;` |


## タグ管理

Tealium iQタグ管理で構成されたベンダータグを隠しwebviewで実行します。

| イベント属性 | 値 |
| :-- | :-- |
| `dispatch_service` | `&#34;tagmanagement&#34;` |


## Tealiumデータ

すべてのライブラリに存在するデフォルトのイベント属性。

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `tealium_event` | `String` | イベントのタイトル。Tealiumが提供するトラックコールの&#39;title&#39;引数によって値が構成されます。一意である必要はありません。 | `&#34;button_tapped&#34;` |
| `tealium_random` | `Number` | イベントごとに生成されるランダムな16桁の数字。16桁の長さを維持するためにゼロでパディングされます。| `1234567890123456` |
| `tealium_account` | `String` | Tealium統合ライブラリを初期化するために使用されるTealiumアカウント名。 | `&#34;companyXYZ&#34;` |
| `tealium_environment` | `String` | Tealium統合ライブラリを初期化するために使用されるTealium TIQ環境。 | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `tealium_library_name` | `String` | プラットフォーム統合ライブラリの名前。 | `&#34;swift&#34;` |
| `tealium_library_version` | `String` | プラットフォーム統合ライブラリのバージョン。 | `&#34;1.2.0&#34;` |
| `tealium_profile` | `String` | Tealium統合ライブラリを初期化するために使用されるTealiumプロファイル名。 | `&#34;main&#34;` |
| `tealium_datasource` | `String` | Tealium Customer Data Hubによって提供される6桁の英数字識別子。 | `&#34;abc123&#34;` |
| `tealium_session_id` | `Number` | 最初のイベントのUnixエポックタイムスタンプ（ミリ秒単位、小数点なし）。新しいセッションが開始されるとリセットされます（通常は新しい起動時）。 | `1496350751928` |
| `tealium_visitor_id` | `String` | ユーザーを区別するためのユニークなアプリデバイス訪問ID。Collectサービスによって必要とされます。 | (32文字の英数字) |
| `tealium_timestamp_epoch` | `Number` | UTCでのUnixタイムスタンプ。 | `1496350751` |