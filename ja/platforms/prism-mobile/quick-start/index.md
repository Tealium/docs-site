---
title: クイックスタート
description: SDK のインストール、構成の初期化、データレイヤー値を使用した最初のイベント送信を行い、iOS、Android、React Native 向けに Tealium Prism をセットアップします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/quick-start/
---
このガイドでは、モバイルプロファイルの作成、Prism SDK のインストール、Tealium インスタンスの初期化、最初のトラッキングコールの送信、結果の検証について説明します。

## モバイルプロファイルを作成する

SDK をインストールする前に、タグ管理でモバイルプロファイルを作成します。手順については、[モバイルプロファイルを作成する](https://docs.tealium.com/create-mobile-profile/)を参照してください。

## インストール



Maven を使用して Tealium Prism Kotlin ライブラリをインストールするには、次の手順を実行します。

Android プロジェクトに、次の Maven リポジトリを追加します。

```kotlin
dependencyResolutionManagement {
    repositories {
        // .. other repos
        maven {
            url = uri("https://maven.tealiumiq.com/android/releases/")
        }
    }
}
```

プロジェクトモジュールの `build.gradle` ファイルに、次の依存関係を追加します。バージョン番号を指定する必要があるのは、`platform()` エントリのみです。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-context-api")
```

次の Prism Kotlin モジュールを個別の依存関係として利用できます。

* `prism-core`（必須）
* `prism-lifecycle`
* `prism-context-api`

AppData、Collect、ConnectivityData、DeepLink、DeviceData、TimeData、Trace の各モジュールは、`prism-core` に含まれています。



Swift Package Manager を使用して Tealium Prism Swift をインストールするには、次の手順を実行します。

1. Xcode プロジェクトで、**File > Add Package Dependencies** を選択します。
1. リポジトリ URL `https://github.com/tealium/tealium-prism-swift` を入力します。
1. バージョンルールを構成します。**Up to next major** に構成することをお勧めします。現在の Tealium Prism Swift ライブラリのバージョンがリストに表示されない場合は、Swift パッケージのキャッシュをリセットしてください。
1. インストールするモジュールを選択し、Xcode プロジェクトの各アプリターゲットの **Frameworks > Libraries & Embedded Content** に追加します。

CocoaPods を使用してインストールするには、Podfile に次の行を追加します。

```ruby
pod 'tealium-prism'
```

次の Prism Swift モジュールを個別の依存関係として利用できます。

* `TealiumPrismCore`（必須）
* `TealiumPrismLifecycle`
* `TealiumPrismContextAPI`

AppData、Collect、ConnectivityData、DeepLink、DeviceData、DataLayer、TimeData、Trace の各モジュールは、`TealiumPrismCore` に含まれています。


Tealium Prism React Native には、新アーキテクチャ（TurboModules）を使用する React Native 0.85 が必要です。

npm を使用して Tealium Prism React Native ライブラリをインストールするには、次のコマンドを実行します。

```bash
npm install @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

代わりに Yarn を使用してインストールするには、次のコマンドを実行します。

```bash
yarn add @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

ネイティブ iOS の依存関係をインストールするには、次のコマンドを実行します。

```bash
cd ios && pod install
```

Android では追加の手順は必要ありません。



CocoaPods を含む詳細なインストール手順については、[インストール](https://docs.tealium.com/install/)を参照してください。

## 初期化




Tealium を初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/) インスタンスを [`Tealium.create()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/) メソッドに渡します。Tealium Kotlin ライブラリは、アプリのグローバルアプリケーションクラス内にある `onCreate()` メソッドで初期化することをお勧めします。

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig
import com.tealium.prism.core.api.Modules
import com.tealium.prism.core.api.misc.Environment
import com.tealium.prism.lifecycle.lifecycle

val config = TealiumConfig.Builder(
   application = application,
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



Tealium を初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) インスタンスを [`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) 静的メソッドに渡します。

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
let tealium = Tealium.create(config: config)
```

SDK をプログラムで構成して特定のモジュールを有効にするには、構成にモジュールを追加します。

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
import TealiumPrismLifecycle
import TealiumPrismContextAPI
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
                            Modules.contextAPI(),
                            Modules.timeData(),
                            Modules.trace(),
                           ],
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
let tealium = Tealium.create(config: config)
```



Tealium を初期化するには、アカウント、プロファイル、[環境](https://docs.tealium.com/tealium-prism-react-native/variables/Environment.html)を指定して [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create) を呼び出します。アプリの起動時にインスタンスを 1 つ作成し、アプリ全体で共有することをお勧めします。

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

iOS では、構成ファイルをアプリターゲットに追加します。Android では、構成ファイルを `android/app/src/main/assets/` に配置します。

実行されるモジュールは、インストール済みのパッケージと Tealium の構成によって決まります。



構成オプションの詳細については、[インストール](https://docs.tealium.com/install/)を参照してください。
## トラッキング

イベントをトラッキングするには、イベント名と、必要に応じてタイプおよびデータを `track()` メソッドに渡します。イベント名はデータレイヤーに `tealium_event` として表示されます。



イベントをトラッキングするには、[`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) を呼び出します。

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```


イベントをトラッキングするには、[`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) を呼び出します。

```swift
// Basic track with default event type and empty data layer
tealium.track("homepage")

// Track with full parameters
tealium.track("user_login", type: .event, data: ["customer_id": "1234567890"])

// Track with view type
tealium.track("homepage", type: .view)
```


イベントをトラッキングするには、[`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track) を呼び出します。SDK がデータをシリアル化できない場合、`track()` が返す Promise は拒否されます。

```javascript
// Track an event with the default type.
await tealium.track("homepage");

// Track an event with data.
await tealium.track("user_login", "event", { customer_id: "1234567890" });

// Track a view.
await tealium.track("homepage", "view");
```



トラッキングの詳細については、[トラッキング](https://docs.tealium.com/track/)を参照してください。

## データレイヤー

データレイヤーにデータを追加するには、次の操作を行います。



データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) メソッドを使用します。

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```

データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) メソッドを使用し、結果を処理するためにサブスクライブします。

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // do something with customerId
}
```

データレイヤーオブジェクトを構成するには、`DataObject.Builder()` を使用します。

```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.putAll(globalContext, Expiry.FOREVER)
```

個々の `put` 操作は、アトミック性が必要ない場合にのみ使用してください。各呼び出しは独立して順番に実行されるためです。複数の値を構成する際にタイミングや一貫性が重要な場合は、`transactionally` を使用して、すべての更新を単一のアトミック操作として適用します。これにより、すべての更新が成功するか、すべて失敗するかのいずれかになります。

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

配列値を構成するには、`DataList.Builder()` を使用します。

```kotlin
val productCategories = DataList.create {
  add("electronics")
  add("headphones")
}

dataLayer.put(
    key = "product_category",
    value = productCategories,
    expiry = Expiry.SESSION
).onFailure { err -> }
```

データの有効期限を構成するには、`Expiry` を使用します。

```kotlin
dataLayer.put(
    key = "currency",
    value = "USD",
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = "order_total",
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```


データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを呼び出します。

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

複数のデータレイヤー値を一度に構成するには、[`putAll(dataObject:)`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) に辞書を渡します。

```swift
tealium.dataLayer.putAll(dataObject: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
])
```

データの有効期限を構成するには、[`Expiry`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Expiry.html) を使用します。

```swift
tealium.dataLayer.put(key: "currency",
                      value: "USD",
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total",
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```



データレイヤーの値を取得するには、[`tealium.dataLayer`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#datalayer) の [`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get) を呼び出します。

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put) を呼び出します。

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

1 回の呼び出しで複数の値を構成するには、[`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall) にプレーンオブジェクトを渡します。

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
  product_category: ["electronics", "headphones"],
});
```

データの有効期限を構成するには、最後の引数として[有効期限](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html)を渡します。

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart"); // or "session", "forever"

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```

データレイヤーのすべての値を取得するには、[`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall) を呼び出します。

```javascript
const data = await tealium.dataLayer.getAll();
```

データレイヤーの値を削除するには、キーまたはキーの配列を指定して [`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove) を呼び出します。

```javascript
await tealium.dataLayer.remove("customer_id");
await tealium.dataLayer.remove(["is_logged_in", "consent_status"]);
```

データレイヤーのすべての値を削除するには、[`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear) を呼び出します。

```javascript
await tealium.dataLayer.clear();
```



データレイヤーの詳細については、[データレイヤー](https://docs.tealium.com/data-layer/)を参照してください。

## 検証

ログファイルの確認、トレースの実行、ライブイベントの表示によって、データを検証します。
### ログ



ログレベルを構成するには、`TealiumConfig` ビルダーの構成で `setLogLevel()` を呼び出します。

```kotlin
val config = TealiumConfig.Builder(...)
  .configureCoreSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

詳細については、[LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html) を参照してください。


ログレベルを構成するには、[`TealiumConfig` ビルダー](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html)の構成で `setMinLogLevel()` を呼び出します。

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


ログレベルを構成するには、[`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create) の6番目の引数として [`LogLevel`](https://docs.tealium.com/tealium-prism-react-native/types/LogLevel.html) を渡します。使用しない構成引数には `undefined` を渡します。

```javascript
const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.dev,
  undefined,
  undefined,
  "debug" // or "trace", "info", "warn", "error", "silent"
);
```



### トレース

[Mobile Trace Tool](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/) では、デバイスでスキャンして Tealium モバイル SDK からのイベントをリアルタイムで表示できる QR コードが提供されます。



[Trace インターフェイス](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/)の使用方法について詳しく説明します。

```kotlin
trace.join("TRACE_ID")

// Leave the current trace session
trace.leave()

// Force end of visit for testing
trace.forceEndOfVisit()
```


[Trace プロトコルリファレンス](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)の使用方法について詳しく説明します。

```swift
// Join a trace session
tealium.trace.join(id: "TRACE_ID")

// Leave the current trace session
tealium.trace.leave()

// Force end of visit for testing
tealium.trace.forceEndOfVisit()
```


[Trace インターフェイス](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html)の使用方法について詳しく説明します。

```javascript
// Join a trace session.
await tealium.trace.join("TRACE_ID");

// Force end of visit for testing.
await tealium.trace.forceEndOfVisit();

// Leave the current trace session.
await tealium.trace.leave();
```

これらの呼び出しを使用するには、Tealium の構成で Trace モジュールを有効にします。有効になっていない場合、Promise は拒否されます。



### ライブイベント

ライブイベントを使用して、[モバイルインストールをトラブルシューティングします](https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/)。

[ライブイベント](https://docs.tealium.com/about-live-events/)について詳しく説明します。