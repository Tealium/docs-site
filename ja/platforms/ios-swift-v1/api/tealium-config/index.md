---
title: TealiumConfig
description: Tealiumクラスの構成オプションを構成するためのクラス。個々のモジュールは、有効になっている場合、TealiumConfigクラスの拡張を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/
---
## クラス: `TealiumConfig`

以下は、iOS (Swift) `TealiumConfig` クラスの一般的に使用されるメソッドとプロパティをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| `addDelegate()` | TealiumDelegateプロトコルに準拠する新しいデリゲートを追加します |
| `addRemoteCommand()` | 後で実行するリモートコマンドを追加します |
| `batchingBypassKeys` | バッチ処理をバイパスするイベント名のリストを構成します（個別のイベントとして送信されます） |
| `batchingEnabled` | イベントバッチ処理を有効または無効にします（デフォルトは無効） |
| `batchSize` | 単一のバッチリクエストに組み合わせるイベントの量を構成します（最大：10） |
| `collectOverrideProfile` | データを異なるTealiumプロファイルに送信するためにTealium Collectプロファイルを上書きします |
| `collectOverrideURL` | データを異なるエンドポイントに送信するためにTealium Collect URLを上書きします |
| `connectivityRefreshEnabled` | 有効にすると（デフォルト）、接続性モジュールは指定された間隔で接続をチェックします |
| `connectivityRefreshInterval` | デフォルトの接続性リフレッシュ間隔を秒単位で構成します |
| `consentLoggingEnabled` | 同意ログ機能を有効または無効にします |
| `delegates` | 有効になっているデリゲートの配列を返します |
| `dispatchAfter` | キューがフラッシュされるイベントの数を構成します |
| `dispatchExpiration` | デバイスが長期間オフラインの場合、古いイベントが削除されるバッチの有効期限を日数で構成します |
| `dispatchQueueLimit` | キューされたイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます |
| `enableRemoteHTTPCommand()` | 組み込みのリモートHTTPコマンドを有効にします |
| `existingVisitorId` | 既存の訪問IDを構成します。アプリ拡張機能での第一者IDとして使用されます |
| `geofenceFileName` | ローカルのジオフェンスJSONファイルアセットの名前を構成します。_ファイル拡張子は含めないでください。_ |
| `geofenceUrl` | ホストされたJSONファイルのURLを構成します |
| `initialUserConsentCategories` | ライブラリが初めて起動するときにユーザーの初期同意カテゴリを構成します |
| `initialUserConsentStatus` | 初期ユーザー同意ステータスを構成します |
| `logLevel` | 新しいログレベルを構成します |
| `memoryReportingEnabled` | DeviceDataモジュールでのメモリレポートを有効または無効にします |
| `modulesList`| 有効または無効にするモジュールのリスト |
| `overrideConsentPolicy` | デフォルトの同意`policy`パラメータを上書きします |
| `remoteAPIEnabled` | `remote_api`イベントを有効（`true`）または無効（`false`）にします。RemoteCommandsモジュールを使用する場合、DispatchQueueモジュールが必要です。 |
| `remoteCommand` | 登録されているすべてのリモートコマンドの配列を返します |
| `remoteHTTPCommandDisabled` | 組み込みのリモートHTTPコマンドを無効にします（`true`の場合）|
| `rootView` | `WKWebView`をアタッチするための現在の`UIView`を構成します|
| `searchAdsEnabled` | AttributionモジュールでのApple Search Ads APIを有効または無効にします |
| `shouldAddCookieObserver` | Tealiumが`WKWebView` Cookie Observerを追加するかどうかを決定します |
| `shouldUseRemotePublishSettings` | モバイルパブリッシュ構成を構成します（デフォルト：有効）|
| `tagManagementOverrideURL` | タグ管理モジュールで使用されるデフォルトURLを上書きします |
| `TealiumConfig()`  | `TealiumConfig`オブジェクトのコンストラクタ |
| `updateDistance`  | 位置情報の更新を受け取る距離間隔（メートル）を構成します |
| `useHighAccuracy` | 位置精度を低精度（デフォルト）または高精度に構成します |


### `addDelegate()`
TealiumDelegateプロトコルに準拠する新しいデリゲートを追加します。

```swift
addDelegate(delegate)
```

| パラメータ   | タイプ    | 説明                                       |
|-------------|---------|---------------------------------------------------|
| `delegate`  | `TealiumDelegate`  | TealiumDelegateプロトコルに準拠するクラス  |

次の例は、現在のモジュールが`TealiumDelegate`プロトコルを実装していると仮定しています：

```swift
config.addDelegate(self)
```

### `addRemoteCommand()`

後で実行するリモートコマンドを追加します。

```swift
addRemoteCommand(command)
```

| パラメータ   | タイプ    | 説明                                       |
|-------------|---------|---------------------------------------------------|
| `command`   | `TealiumRemoteCommand`  | 追加されるTealiumRemoteCommandのインスタンス |

次の例は、Tealiumの初期化の前に配置され、リモートコマンドを追加する方法を示しています：

```swift
#if os(iOS)
let remoteCommand = TealiumRemoteCommand(commandId: "test",
        description: "test") { response in
			print("Remote Command 'test' executed")
}
config.addRemoteCommand(remoteCommand)
#endif
```

### `batchingBypassKeys`

バッチ処理をバイパスするイベント名のリストを構成します（個別のイベントとして送信されます）。

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

イベントバッチ処理を有効（`true`）または無効（`false`）にします。デフォルトでは無効です。

```swift
config.batchingEnabled = true
```

### `batchSize`

単一のバッチリクエストに組み合わせるイベントの量を構成します。最大は10です。

```swift
config.batchSize = 8
```

### `collectOverrideProfile`

データを異なるTealiumプロファイルに送信するためにTealium Collectプロファイルを上書きします。

```swift
config.collectOverrideProfile = "main"
```

### `collectOverrideURL`

データを異なるエンドポイントに送信するためにTealium Collect URLを上書きします。

```swift
config.collectOverrideURL = url
```

| プロパティ値  | タイプ | 説明 |
| --- | --- | --- |
| `url` | `String` | 上書きするURL |

デフォルトのURLは：  
```bash
https://collect.tealiumiq.com/event/
```
イベントバッチングを使用する場合のデフォルトのURLは：  
```bash
https://collect.tealiumiq.com/bulk-event/
```

このメソッドは通常、カスタムホスト名を構成するか、特定の地域のホスト名を構成するために使用されます。次の例は、Tealium Collectの基本URLをEU Central地域内に保持するように構成します：

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.collectOverrideURL = url
```

### `connectivityRefreshEnabled`

有効にすると（デフォルト）、接続性モジュールは指定された間隔で接続をチェックします（`setConnectivityRefreshInterval`を介して制御されます）。接続が再開されると、キューに入れられたディスパッチが送信されます。

```swift
config.connectivityRefreshEnabled = true
```

### `connectivityRefreshInterval`

デフォルトの接続性リフレッシュ間隔を秒単位で構成します。TealiumConfigインスタンスで構成されていない場合、デフォルトは30秒です。

```swift
config.connectivityRefreshInterval = 30
```


### `consentLoggingEnabled`

[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします。これにより、すべての同意ステータスの変更が監査目的でTealium Customer Data Hubに送信されます。

```swift
config.consentLoggingEnabled = true
```


### `delegates`

有効になっているデリゲートの配列を返します。

次の例は、有効になっているデリゲートの配列を取得する方法を示しています：

```swift
let delegates = config.delegates
```

### `dispatchAfter`

自動的にキューをフラッシュするイベントの数。

```swift
config.dispatchAfter = 20
```

### `dispatchExpiration`

デバイスが長期間オフラインの場合、古いイベントが削除されるディスパッチの有効期限を日数で構成します。

```swift
config.dispatchExpiration = 5
```

### `dispatchQueueLimit`

イベントキューに格納するイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます。

```swift
config.dispatchQueueLimit = 50
```



### `enableRemoteHTTPCommand()`
組み込みのリモートHTTPコマンドを有効にします（[Swift Module: RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/)を参照）。


```swift
enableRemoteHTTPCommand()
```

### `existingVisitorId`

既存の訪問IDを構成します。アプリ拡張機能での第一者IDとして使用されます |

```swift
config.existingVisitorId = id
```
### `geofenceFileName`

ローカルのジオフェンスファイルアセットの名前を構成します。ファイル拡張子は含めないでください。

```swift
config.geofenceFileName = <String>
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | JSONファイル名 | `"geofences"` |

### `geofenceUrl`

ホストされているジオフェンスファイルのURLを構成します。

```swift
config.geofenceUrl = <String (url)>
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | ジオフェンスファイルのURL | `"https://example.com/.../geofences.json"` |

### `initialUserConsentCategories`

ライブラリが初めて起動するときにユーザーの初期同意カテゴリを構成します。保存された構成がある場合、これらは構成オブジェクトで渡された構成を上書きします。同意状態を `.consented` に構成します。

```swift
config.initialUserConsentCategories = [.cdp, .analytics]
```

### `initialUserConsentStatus`

ユーザーの初期同意状態を構成します。これはライブラリが初めて起動するときにユーザーに対して行われます。保存された構成がある場合、これらは構成オブジェクトで渡された構成を上書きします。

同意状態が `.consented` の場合、利用可能なすべての同意カテゴリを含むように同意カテゴリのリストを構成します。カテゴリを選択的に構成することはできません。

この方法を使用して、同意が与えられる前に追跡されたすべてのイベントを無視し、同意が与えられる前にイベントをキューに入れるデフォルトの動作を上書きします。構成オブジェクトに次の行を追加します：

```swift
config.initialUserConsentStatus = .notConsented
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus` | TealiumConsentStatus列挙型からの値 | [`.unknown`, `.consented`, `.notConsented`] |

以下は `TealiumConsentStatus` 列挙型からのTealium同意ステータスの異なるタイプを定義しています。

**.unknown**  
`unknown` ステータスは同意マネージャーのデフォルト構成です。この状態では、同意マネージャーはローカルにイベントをキューに入れ、肯定的な `consented`/`notConsented` ステータスが提供されるまで待ちます。

**.consented**  
ユーザーが追跡に同意した場合に構成される `consented` ステータスです。この状態では、同意マネージャーは通常どおりすべての追跡コールを続行させます。

**.notConsented**  
ユーザーが追跡を拒否した場合に構成される `notConsented` ステータスです。この状態では、同意マネージャーはすべての追跡コールをドロップし、SDKによるさらなる処理を停止します。
### `updateDistance`

位置更新が受信される距離間隔（メートル）を構成します。


<blockquote>
このメソッドは、`useHighAccuracy`が`true`に構成されている場合のみ使用してください。
</blockquote>


```swift
config.updateDistance = <Double>
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `Double` | 位置更新が受信される距離間隔（メートル） | `150.0` |

使用例:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `useHighAccuracy`

位置精度を低精度（デフォルト）または高精度に構成します。

このプロパティはデフォルトで無効（`false`）に構成されており、位置精度を低精度に構成します。位置情報を有効にしたデバイスが500メートル以上移動すると、これは重要な位置変更と見なされ、位置更新が行われます。この構成では、位置更新には通常5分以上かかります。

[Appleの重要変更位置サービスについての詳細を学ぶ](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service)。

有効にすると（`true`）、このプロパティは可能な限り最高の精度で位置データの精度を構成します。初期イベントはできるだけ早く配信され、その後、位置を特定し、データが利用可能になったときに必要に応じて追加のイベントを配信します。

[Appleの位置データの精度についての詳細を学ぶ](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift)。

高精度を使用すると、位置更新が頻繁に行われるため、低精度よりもデバイスのバッテリー消費が増加します。

```swift
config.useHighAccuracy = <Bool>
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `Boolean` | 位置データの精度を構成 | `true` |

使用例:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```
