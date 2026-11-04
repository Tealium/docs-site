---
title: データレイヤー
description: モバイル環境で使用できるデータレイヤー変数の一覧です。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/data-layer/
---
各モバイルコンポーネントは、データレイヤーに変数を追加します。以下のセクションでは、各モジュールのすべての変数を示します。

すべての値は文字列に変換されます。ただし、必要に応じて、iQ拡張機能またはEvent Streamingのエンリッチメントを使用して、数値型に戻すことができます。


<blockquote>
自動追跡されるすべてのイベントには、属性 `autotracked="true"` が構成されます。
</blockquote>


## アプリデータ

ホストアプリケーションのプロパティです。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `app_name` | `String` | アプリケーション名 | `"Digital Velocity"` |
| `app_rdns` | `String` | 逆引きDNS形式のBundle ID／パッケージ名 | `"com.digitalvelocity.alpha"` |
| `app_version` | `String` | アプリケーションのバージョン |  `"1.2.0"` |

## Collect

プラットフォームのネイティブURL通信サービスを使用し、トラッキング呼び出しをネットワークリクエストとしてTealiumのCollectサービスへ送信します。

| イベント属性 | 型 | 値 |
| :-- | :-- | :-- |
| `dispatch_service` | `String` | `"collect"` |

## キャリアデータ

モバイルキャリアに関する情報を提供します。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `carrier` | `String` | キャリア名 |`"AT&T"` |
| `carrier_iso` | `String` | キャリアのISO 3166-1国コード |`"us"` |
| `carrier_mcc` | `String` | ITU-T E.212に基づくモバイル国コード | `"us"` |
| `carrier_mnc` | `String` | モバイルネットワークコード | `"410"` |

## 同意管理

同意のトラッキング構成に関する情報を提供します。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `policy` | `String` | 同意の取得時に適用されたポリシー |`"gdpr"` |
| `consent_status` | `String` | ユーザーの現在の同意ステータス |`"consented"` |
| `consent_categories` | `[String]` | ユーザーが選択した同意カテゴリーの配列 | `["analytics", "cdp"]` |

## デバイスデータ

ホストデバイスに関する情報を提供します。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `device` |`String` | デバイス名 |`"iPhone 6s"` |
| `device_architecture` |`Number` | デバイスのビットアーキテクチャ（32、64など） | `64` |
| `device_advertising_id` |`String` | 任意の広告識別子。すべてのデバイスで自動的に使用できるわけではありません |`"03402320-245A-4ED4-BEAE-A1F50E21C55E"` |
| `device_battery_percent` |`Number` | デバイスのバッテリー残量を整数のパーセント値で表したもの | `100` |
| `device_cputype` | `String` | CPU（中央処理装置）の種類（arm6、arm7など） |`"ARM64"` |
| `device_ischarging ` | `String` | デバイスが現在充電中かどうか（true／false） | `"false"` |
| `device_language ` | `String` | 2文字のISO-639-1言語識別子（en、jaなど） |`"en"` |
| `device_orientation` | `String` | イベント発生時のデバイスの向き（縦向き、横向きなど） |`"Portrait"` |
| `device_resolution ` | `String` | デバイスの解像度 |`"750x1334"` |

## ライフサイクルイベント

アプリケーションの起動、復帰、スリープというライフサイクルイベントを自動的に追跡します。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `lifecycle_ dayofweek_local` | `Number` | 現地時間の曜日（1＝日曜日、2＝月曜日など） | `3` |
| `lifecycle_ dayssincelaunch` | `Number` | 初回起動からの経過日数（整数単位） | `0`（まだ24時間が経過していない） |
| `lifecycle_ dayssinceupdate` | `String` | アプリが更新されてからの経過日数（整数単位） |`"1"` |
| `lifecycle_ diddetectcrash` | `String` | 起動時にクラッシュが検出されたかどうか |`"true"` |
| `lifecycle_ firstlaunchdate` | `String` | 最初に検出された起動のGMTタイムスタンプ（UTCのISO 8601形式） | `"2016-05-16T16:32:04Z"` |
| `lifecycle_ firstlaunchdate_ MMDDYYYY` | `String` | 最初に検出された起動のGMTタイムスタンプ（MM/DD/YYYY形式） |`"5/16/2016"` |
| `lifecycle_ hourofday_local` | `Number` | 現地時間の時刻（24時間形式） | `13` |
| `lifecycle_ isfirstlaunch` | `String` | 初回起動の場合は`"true"`（それ以外の場合は値なし） |  `"true"` |
| `lifecycle_ isfirstlaunchupdate` | `String` | 検出されたアプリのバージョン更新後、最初の起動の場合は`"true"`（それ以外の場合は値なし） |`"true"` |
| `lifecycle_ isfirstwakemonth` | `String` | 起動イベントが当月で最初の場合は`"true"`（それ以外の場合は値なし） | `"true"` |
| `lifecycle_ isfirstwaketoday ` | `String` | 起動／復帰イベントが当日で最初の場合は`"true"`（それ以外の場合は値なし） | `"true"` |
| `lifecycle_ lastlaunchdate ` | `String` | 直前に記録された起動のGMTタイムスタンプ（UTCのISO 8601形式。最初のセッション内の場合は値なし） | `"2013-07-11T17:55:04Z"` |
| `lifecycle_ lastsleepdate ` | `String` | 直前に記録されたスリープイベントのGMTタイムスタンプ（UTCのISO 8601形式） |`"2013-07-11T17:55:04Z"` |
| `lifecycle_ lastwakedate ` | `String` | 直前に記録された復帰イベントのGMTタイムスタンプ（UTCのISO 8601形式） |`"2013-07-11T17:55:04Z"` |
| `lifecycle_ launchcount ` | `Number` | 最後のバージョン更新以降のアプリケーション起動回数（整数値。新しいバージョンが検出されるとリセット） |`3` |
| `lifecycle_ priorsecondsawake` | `Number` | 起動イベント時にのみ値が構成されます。復帰からスリープまでアプリケーションが稼働していた秒数の整数値です。起動イベントまでのすべての復帰とスリープを集計します。 | `148` |
| `lifecycle_ secondsawake ` | `Number` | スリープイベント時にのみ値が構成されます。直前の復帰からスリープイベントまで、アプリケーションが稼働していた秒数の整数値です。 |`480` |
| `lifecycle_ sleepcount ` | `Number` | アプリがスリープ状態またはバックグラウンドに移行したことが検出された合計回数 |`3` |
| `lifecycle_ totallaunchcount` | `Number` | アプリのインストール以降の起動回数の合計。アプリケーションを削除して再インストールした場合にのみリセットされます。 |`5` |
| `lifecycle_ totalsecondsawake ` | `Number` | アプリケーションが稼働していた合計秒数。アプリケーションを削除して再インストールした場合にのみリセットされます。 |`800` |
| `lifecycle_ totalsleepcount ` | `Number` | アプリケーションがスリープ状態に移行したことが検出された合計回数。アプリケーションを削除して再インストールした場合にのみリセットされます。 |`8` |
| `lifecycle_ totalcrashcount` | `Number` | アプリケーションがスリープイベントを適切に記録できず、クラッシュによってライフサイクルシーケンスに不整合が発生した合計回数。アプリケーションを削除して再インストールした場合にのみリセットされます。 |`2` |
| `lifecycle_ totalwakecount ` | `Number` | 起動と復帰の合計回数。アプリケーションを削除して再インストールした場合にのみリセットされます。 |`7` |
| `lifecycle_type`  | `String` | ライフサイクルイベントの種類 |  [`"launch"`, `"wake"`, `"sleep"`] |
| `lifecycle_ updatelaunchdate` | `String` | アプリのバージョン更新が検出された後、最初に起動／復帰した時点のGMTタイムスタンプ。UTCのISO 8601形式です。 |`"2016-05-16T16:32:04Z"` |
| `lifecycle_ wakecount` | `Number` | このアプリケーションバージョンでの起動と復帰の合計回数。ホストアプリケーションの新しいバージョンが検出されるとリセットされます。 |`34` |

## オフラインキュー

デバイスのネットワーク接続が一時的に失われた場合などに、後で配信できるようイベント送信データを保持します。

キューに保存された送信データ内の以下のイベント属性に値を構成します。

| イベント属性 | 値 |
| :-- | :-- |
| `was_queued` | `"true"` |

## タグ管理

Tag Managementで構成されたベンダータグを、非表示のWebView内で実行します。

| イベント属性 | 値 |
| :-- | :-- |
| `dispatch_service` | `"tagmanagement"` |
## Tealiumデータ

すべてのライブラリに存在するデフォルトのイベント属性です。

| イベント属性 | 型 | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `tealium_event` | `String` | イベントのタイトル。Tealiumが提供するトラッキング呼び出しの「title」引数によって構成されます。一意である必要はありません。 | `"button_tapped"` |
| `tealium_random` | `Number` | イベントごとに生成される16桁のランダムな数値。16桁を維持するため、先頭にゼロがエンリッチメントされます。 | `1234567890123456` |
| `tealium_account` | `String` | Tealium統合ライブラリの初期化に使用されるTealiumアカウント名。 | `"companyXYZ"` |
| `tealium_environment` | `String` | Tealium統合ライブラリの初期化に使用されるTealium TIQ環境。 | [`"dev"`, `"qa"`, `"prod"`] |
| `tealium_library_name` | `String` | プラットフォーム統合ライブラリの名前。 | `"swift"` |
| `tealium_library_version` | `String` | プラットフォーム統合ライブラリのバージョン。 | `"1.2.0"` |
| `tealium_profile` | `String` | Tealium統合ライブラリの初期化に使用されるTealiumプロファイル名。 | `"main"` |
| `tealium_datasource` | `String` | Tealium Customer Data Hubによって提供される6桁の英数字識別子。 | `"abc123"` |
| `tealium_session_id` | `Number` | 最初のイベントのミリ秒単位のUNIXエポックタイムスタンプ（小数点以下なし）。新しいセッションの開始後（通常は新規起動時）にリセットされます。 | `1496350751928` |
| `tealium_visitor_id` | `String` | ユーザーを区別する、アプリとデバイスに固有の訪問ID。Collectサービスで必須です。 |（32文字の英数字）|
| `tealium_timestamp_epoch` | `Number` | UTCでのUNIXタイムスタンプ。 | `1496350751` |