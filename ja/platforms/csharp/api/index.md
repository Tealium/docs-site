---
title: APIリファレンス
description: TealiumがC#向けに提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/csharp/api/
---
## クラス: `Config`

以下は、C#の`Config`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `Config()` | Tealiumの構成コンストラクタ |

### `Config()`

Tealiumインスタンスを構成するためのコンストラクタ

```csharp
Config tealConfig = new Config(account, profile, environment,
                               visitorID, modules, dataSourceKey,
                               overrideCollectUrl, optionalData, method);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `string` | Tealiumのアカウント名  | `"companyXYZ"` |
| `profile` | `string` |Tealiumのプロファイル名|  `"main"` |
| `environment` | `string` |(オプション) Tealiumの環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `visitorID` | `string` |ユーザー、アプリインスタンス、またはデバイスに固有の32文字の英数字のID (`null`可) |  `"t3aL...1uM"` |
| `modules` | `[string]` | (オプション) Collectライブラリで初期化するモジュール |  [利用可能なモジュール](#available-modules)を参照 |
| `dataSourceKey` | `string` |(オプション) データソースキー |  `"abc123"` |
| `overrideCollectUrl` | `string` |(オプション) Collect URLを上書き (データのカスタム宛先URL) |   |
| `optionalData` | `Dictionary<string, object>` |(オプション) モジュール使用のためのキーと値のペアとしてのデータ (`null`可 - ほとんどの構成では不要) | |
| `method` | `Method` enum | (オプション) Tealium Collectエンドポイントへのデータ送信に使用するHTTPメソッドを決定 | [`Method.POST`, `Method.GET`] |

## クラス: `Tealium`

以下は、C#の`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ------ | ----------- |
| `Disable()` | Tealiumライブラリモジュールを無効化 |
| `Enable()`| Tealiumライブラリモジュールを有効化 |
| `JoinTrace()` | トレースに参加 |
| `KillTraceSession()` | トレースを終了/キル |
| `LeaveTrace()`| トレースを離脱 |
| `Tealium()` | Tealiumコンストラクタ |
| `Track()` | イベントをトラック |

### `Enable()`

`Disable()`呼び出し後の`Tealium`インスタンスを有効化します。初期化時に自動的に呼び出されます。ライブラリが以前に無効化されていた場合、Tealiumインスタンスと内部モジュールを再度有効化します。

```csharp
tealium.Enable()
```

### `Disable()`
`Tealium`インスタンスを無効化します。一時的にイベントの処理を停止します。内部クラスオブジェクトの初期化を解除する可能性があります。

```csharp
tealium.Disable()
```

### `JoinTrace()`

`traceId`パラメータで識別されるトレースに参加します。`traceId`は、`LeaveTrace()`メソッドが呼び出されるまで、すべての後続のイベントにキーとして送信され、イベントのデバッグを可能にします。`traceId`パラメータは、Tealium Customer Data Hub内で事前に生成する必要があります。

```csharp
tealium.JoinTrace(traceId);
```

| パラメータ | タイプ | 説明  | 例 |
|----------- | ----------- | -----| ------- |
| `traceId`  | `string` |参加するトレースID   | `"12345"` |

### `KillTraceSession()`

トレースをキルします。サーバーでのトレース訪問セッションを終了する特定のイベントを発行します。これは、Customer Data Hubでのセッション終了時の動作をテストするのに便利です。

```csharp
tealiumObj.KillTraceSession();
```

### `LeaveTrace()`

トレースを離脱します。もしトレースに参加していた場合は。

```csharp
tealiumObj.LeaveTrace();
```

### `Tealium()`

`Tealium`クラスのコンストラクタメソッド。

```csharp
Tealium tealium = new Tealium(tealConfig);
```

| パラメータ  | タイプ | 説明  |
| ----------- | ----------- | -----|
| `tealConfig` | `Config` | Configインスタンス  |

### `Track()`

イベントをトラックします。

```csharp
tealium.Track(title, customData, completion);
```

| パラメータ | タイプ | 説明 |
| --- | --- | ---  |
| `title` | `string` | イベント識別子 |
| `customData` | `Dictionary<string, object>` | (オプション)  イベントデータをキーと値のペアとして (ない場合は`null`に構成) |
| `completion` | `TrackCompletion` (ない場合は`null`に構成)| (オプション) トラック呼び出し後にトリガーする完了ブロック |



## 利用可能なモジュール

以下の定数文字列の値は、現在のビルドでモジュールを有効にするために使用されます：

```csharp
config.Modules = new string[] { AppDataModule.Name,
                                CollectModule.Name,
                                LoggerModule.Name };
```

| モジュール名 | 説明 |
| --- | --- |
| `AppDataModule` | コールに自動データポイントを追加 |
| `CollectModule` | 処理済みイベントをTealium Collectエンドポイントに配信 |
| `LoggerModule` | デバッグ出力を提供 |


<blockquote>
各モジュールクラスの`.Name`定数を使用してください。
</blockquote>


