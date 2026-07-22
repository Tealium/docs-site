---
title: データレイヤー
description: C#ライブラリからのデータレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/csharp/data-layer/
---
以下の変数は、モバイルデータレイヤーの一部としてTealium C#ライブラリによって自動的に追加されます。これらの変数は、ライブラリからの各トラッキング呼び出しに自動的に含まれます。

| パラメータ | タイプ | 説明  | 例 |
| --- | --- | --- | --- |
| `tealium_account` | `string` | ライブラリを初期化するために使用されるTealiumアカウント名 | `"companyXYZ"` |
| `tealium_profile` | `string` | ライブラリを初期化するために使用されるTealiumプロファイル名 | `"main"` |
| `tealium_environment` | `string` | ライブラリを初期化するために使用されるTealium環境 |[`"dev"`, `"qa"`, `"prod"`]|
| `tealium_event` |	`string` | イベントのタイトル。Tealiumトラック呼び出しのeventTitle引数によって構成されます |  `"Some Event"` |
| `tealium_datasource` | 	`string` | Tealium Customer Data Hubによって提供される6文字の英数字名 |`"abc123"`|
| `tealium_visitor_id` | `string` | ユーザーを区別するための一意のデバイス訪問ID（Collect Serviceが必要とする） | `"t3aL...1uM"` |
| `tealium_library_name` | `string` | プラットフォーム統合ライブラリの名前 |  `"csharp"` |
| `tealium_library_version` | `string` | プラットフォーム統合ライブラリのバージョン | `"1.0.0"` |
| `tealium_random` | `string` | イベントごとに生成されるランダムな16桁の数字 |  `"1234567890123456"` |
| `tealium_session_id` | `string` | 最初のイベントのミリ秒単位のUnixエポックタイムスタンプ、小数点以下なし（新しいセッションが開始/起動するとリセットされます） | `"1496350751928"` |
| `tealium_timestamp_epoch` | `string` | UTCでのUnixタイムスタンプ | `"1496350751"` |
