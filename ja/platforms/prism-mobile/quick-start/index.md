---
title: クイックスタート
description: iOS、Android、React Native用のTealium Prismを構成するために、SDKをインストールし、構成を初期化し、データレイヤー値を持つ最初のイベントを送信します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/quick-start/
---
このガイドでは、モバイルプロファイルの作成、Prism SDKのインストール、Tealiumインスタンスの初期化、最初のトラッキングコールの送信、結果の検証を行う方法を説明します。

## モバイルプロファイルの作成

SDKをインストールする前に、タグ管理でモバイルプロファイルを作成します。手順については、[モバイルプロファイルの作成](https://docs.tealium.com/create-mobile-profile/)を参照してください。

## インストール



Mavenを使用してTealium Prism Kotlinライブラリをインストールするには：

Androidプロジェクトで、以下のMavenリポジトリを追加します：

```kotlin
dependencyResolutionManagement {
    repositories {
        // .. 他のリポ
        maven {
            url = URI("https://maven.tealiumiq.com/android/releases/")
        }
    }
}
```

プロジェクトモジュールの `build.gradle` ファイルに以下の依存関係を追加します。`platform()` エントリーのバージョン番号のみを指定する必要があります：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-moments-api")
```

以下のPrism Kotlinモジュールは個別の依存関係として利用可能です：

* `prism-core`（必須）
* `prism-lifecycle`
* `prism-moments-api`
* `prism-appdata`
* `prism-collect`
* `prism-connectivity-data`
* `prism-deeplink`
* `prism-device-data`
* `prism-time-data`
* `prism-trace`



Swift Package Managerを使用してTealium Prism Swiftをインストールするには：

1. Xcodeプロジェクトで、**File > Swift Packages > Add Package Dependency**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-prism-swift`。
1. バージョンルールを構成します。**次のメジャーバージョンまで**を構成することをお勧めします。現在のTealium Prism Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールを選択し、Xcodeプロジェクトのアプリターゲットの**Frameworks > Libraries & Embedded Content**にモジュールを追加します。

CocoaPodsを使用してインストールする場合、Podfileに以下の行を追加します：

```ruby
pod 'tealium-prism'
```

以下のPrism Swiftモジュールは個別の依存関係として利用可能です：

* `TealiumPrismCore`（必須）
* `TealiumPrismLifecycle`
* `TealiumPrismMomentsAPI`
* `TealiumPrismAppData`
* `TealiumPrismCollect`
* `TealiumPrismConnectivityData`
* `TealiumPrismDeepLink`
* `TealiumPrismDeviceData`
* `TealiumPrismDataLayer`
* `TealiumPrismTimeData`
* `TealiumPrismTrace`


Tealium Prism React Nativeは、新しいアーキテクチャ（TurboModules）を持つReact Native 0.85が必要です。

npmを使用してTealium Prism React Nativeライブラリをインストールするには：

```bash
npm install @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

Yarnを使用する場合は代わりに：

```bash
yarn add @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

ネイティブiOS依存関係をインストールするには：

```bash
cd ios && pod install
```

Androidには追加の手順は必要ありません。



CocoaPods、Carthage、手動インストールを含む詳細なインストール手順については、[インストール](https://docs.tealium.com/install/)を参照してください。

## 初期化




Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/)インスタンスを[`Tealium.create()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/)メソッドに渡します。Tealium Kotlinライブラリは、アプリのグローバルアプリケーションクラスの`onCreate()`メソッド内で初期化することをお勧めします。

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig

val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(
        Modules.appData(),
        Modules.collect(),
        Modules.connectivityData(),
        Modules.deepLink(),
        Modules.deviceData(),
        Modules.lifecycle(),
        Modules.timeData(),
        Modules.trace(),
       )
).build()
val tealium = Tealium.create(config)
```



Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html)インスタンスを[`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html)静的メソッドに渡します。

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

SDKをプログラムで構成し、特定のモジュールを有効にするには、モジュールを構成に追加します：

```swift
#if COCOAPODS
import TealiumPrism
else
import TealiumPrismCore
import TealiumPrismLifecycle
import TealiumPrismMomentsAPI
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.appData(),
                            Modules.collect(),
                            Modules.connectivityData(),
                            Modules.deepLink(),
                            Modules.deviceData(),
                            Modules.lifecycle(),
                            Modules.momentsAPI(),
                            Modules.timeData(),
                            Modules.trace(),
                           ],
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")
let tealium = Tealium.create(config: config)
```



Tealiumを初期化するには、アカウント、プロファイル、[環境](https://docs.tealium.com/tealium-prism-react-native/variables/Environment.html)を指定して[`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create)を呼び出します。アプリが開始するときに1つのインスタンスを作成し、アプリ全体で共有することをお勧めします。

```javascript
import { Tealium, Environment } from "@tealium/prism-react-native";

const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.prod,
  "my_settings.json",
  "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json"
);
```

iOSでは、構成ファイルをアプリターゲットに追加します。Androidでは、構成ファイルを`android/app/src/main/assets/`に置きます。

インストールされたパッケージとTealium構成によって、どのモジュールが実行されるかが決まります。



構成オプションの詳細については、[インストール](https://docs.tealium.com/install/)を参照してください。
## トラック

イベントをトラックするには、イベント名とオプションのタイプおよびデータを `track()` メソッドに渡します。イベント名はデータレイヤーで `tealium_event` として表示されます。



イベントをトラックするには、[`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) を呼び出します。

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```


イベントをトラックするには、[`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) を呼び出します。

```swift
// デフォルトのイベントタイプと空のデータレイヤーで基本的なトラック
tealium.track("homepage")

// フルパラメータでトラック
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

// ビュータイプでトラック
tealium.track("homepage", type: .view)
```


イベントをトラックするには、[`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track) を呼び出します。`track()` はSDKがデータをシリアライズできない場合にPromiseを拒否します。

```javascript
// デフォルトタイプでイベントをトラック。
await tealium.track("homepage");

// データを持つイベントをトラック。
await tealium.track("user_login", "event", { customer_id: "1234567890" });

// ビューをトラック。
await tealium.track("homepage", "view");
```



トラッキングの詳細については、[Track](https://docs.tealium.com/track/)を参照してください。

## データレイヤー

データレイヤーにデータを追加するには：



データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) メソッドを使用します：

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```

データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) メソッドを使用し、結果を処理するためにサブスクライブします：

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // customerIdを何かに使用する
}
```

データレイヤーオブジェクトを構成するには `DataObject.Builder()` を使用します：
```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```

個々の `put` 操作は、各呼び出しが独立して順番に実行されるため、原子性が必要ない場合にのみ使用します。複数の値を構成し、タイミングや一貫性が重要な場合は、`transactionally` を使用してすべての更新を単一の原子操作で適用し、すべてが成功するかすべてが失敗するようにします。

```kotlin
tealium.dataLayer.transactionally { editor ->
    editor.put("key", "value".asDataItem(), Expiry.SESSION)
        .put("key2", "value2".asDataItem(), Expiry.SESSION)
        .remove("key2")
        .commit()
}.onFailure {
    Log.d("DataLayer", "Transactional update failed: ${it.message}")
}
```

配列値を構成するには `DataList.Builder()` を使用します：
```kotlin
val productCategories = DataList.create {
  add("electronics")
  add("headphones")
}

dataLayer.put(
    key = "product_category",
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -> })
```

データの有効期限を構成するには `Expiry` を使用します：
```kotlin
dataLayer.put(
    key = "currency",
    value = DataItem(any = "USD"),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = "order_total",
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```


データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを呼び出します：
```swift
tealium.dataLayer.get(key: "customer_id",
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print("Optional Value: \(String(describing: value))")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを使用します。

```swift
tealium.dataLayer.put(key: "some_key", value: "some value")
```

一度に複数のデータレイヤー値を構成するには、辞書を [`put(data:)`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) に渡します：

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
])
```

データの有効期限を構成するには [`Expiry`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Expiry.html) を使用します：
```swift
tealium.dataLayer.put(key: "currency",
                      value: "USD",
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total",
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```



データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get) を [`tealium.dataLayer`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#datalayer) で呼び出します：

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put) を呼び出します：

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

一度に複数の値を構成するには、プレーンオブジェクトを [`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall) に渡します：

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
  product_category: ["electronics", "headphones"],
});
```

データの有効期限を構成するには、最後の引数として [expiry](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html) を渡します：

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart"); // または "session", "forever"

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```

すべてのデータレイヤー値を取得するには、[`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall) を呼び出します：

```javascript
const data = await tealium.dataLayer.getAll();
```

データレイヤー値を削除するには、キーまたはキーの配列を指定して [`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove) を呼び出します：

```javascript
await tealium.dataLayer.remove("customer_id");
await tealium.dataLayer.remove(["is_logged_in", "consent_status"]);
```

すべてのデータレイヤー値を削除するには、[`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear) を呼び出します：

```javascript
await tealium.dataLayer.clear();
```



データレイヤーの詳細については、[Data layer](https://docs.tealium.com/data-layer/)を参照してください。

## 検証

ログファイルを検査し、トレースを実行し、ライブイベントを表示してデータを検証します。
### ログ



ログレベルを構成するには、`TealiumConfig` ビルダーの構成で `setLogLevel()` を呼び出します：

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

詳細については、[LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html)を参照してください。


ログレベルを構成するには、[`TealiumConfig` ビルダー](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html)の構成で `setMinLogLevel()` を呼び出します：

```swift
var config = TealiumConfig(account: "your_account",
                           profile: "your_profile",
                           environment: "dev",
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace)
})
```


ログレベルを構成するには、[`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create)の第六引数として[`LogLevel`](https://docs.tealium.com/tealium-prism-react-native/types/LogLevel.html)を渡します。使用しない構成引数には `undefined` を渡します：

```javascript
const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.dev,
  undefined,
  undefined,
  "debug" // または "trace", "info", "warn", "error", "silent"
);
```



### トレース

[モバイルトレースツール](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/)は、TealiumモバイルSDKからのライブイベントを表示するためにデバイスでスキャンできるQRコードを提供します。



[トレースインターフェース](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/)の使用方法について学びましょう。

```kotlin
trace.join("TRACE_ID")

// 現在のトレースセッションを離れる
trace.leave()

// テストのために訪問を強制終了する
trace.forceEndOfVisit()
```


[トレースプロトコルリファレンス](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)の使用方法について学びましょう。

```swift
// トレースセッションに参加する
tealium.trace.join(id: "TRACE_ID")

// 現在のトレースセッションを離れる
tealium.trace.leave()

// テストのために訪問を強制終了する
tealium.trace.forceEndOfVisit()
```


[トレースインターフェース](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html)の使用方法について学びましょう。

```javascript
// トレースセッションに参加する。
await tealium.trace.join("TRACE_ID");

// テストのために訪問を強制終了する。
await tealium.trace.forceEndOfVisit();

// 現在のトレースセッションを離れる。
await tealium.trace.leave();
```

これらの呼び出しを使用するには、Tealium構成でトレースモジュールを有効にしてください。そうでない場合、Promiseは拒否されます。



### ライブイベント

[モバイルインストールのトラブルシューティング](https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/)にライブイベントを使用します。

[ライブイベント](https://docs.tealium.com/about-live-events/)についてもっと学びましょう。