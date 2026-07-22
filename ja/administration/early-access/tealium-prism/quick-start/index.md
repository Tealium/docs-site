---
title: Tealium Prism クイックスタートガイド
description: SDKをインストールし、構成を初期化して、データレイヤー値を持つ最初のイベントを送信することでiOSとAndroidのTealium Prismを構成します。
url: https://docs.tealium.com/ja/administration/early-access/tealium-prism/quick-start/
---
## インストール



Mavenを使用してTealium Prism Kotlinライブラリをインストールするには：

Androidプロジェクトで、以下のmavenリポジトリを追加します：

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

```ruby
implementation(platform("com.tealium.prism:prism-bom:0.4.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-moments-api")  
```



Swift Package Managerを使用してTealium Prism Swiftをインストールするには：

1. Xcodeプロジェクトで、**File > Swift Packages > Add Package Dependency**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-prism-swift`。
1. バージョンルールを構成します。**次のメジャーバージョンまで**を構成することをお勧めします。現在のTealium Prism Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールを選択し、Xcodeプロジェクトの各アプリターゲットにモジュールを追加します。**Frameworks > Libraries & Embedded Content**の下にあります。

Cocoapodsを使用してインストールする場合、podfileに以下の行を追加します：

```ruby
pod 'tealium-prism'
```



## 初期化




Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/) インスタンスを [`Tealium.create()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/) メソッドに渡します。Tealium Kotlinライブラリはアプリのグローバルアプリケーションクラスの `onCreate()` メソッド内で初期化することをお勧めします。

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



Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) インスタンスを [`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) 静的メソッドに渡します。

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

リモート構成を使用しない場合、または異なるデフォルトを提供するために構成のローカルコピーが必要な場合は、ローカル構成ファイルを指定します：

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

SDK全体をプログラムで構成し、特定のモジュールをデフォルトで有効にするか、モジュール構成を変更するには、モジュールを構成に追加します：

```swift
#if COCOAPODS
import TealiumPrism
#else
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
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json",
)
let tealium = Tealium.create(config: config)
```

各モジュールは追加のプログラム構成を指定できます。これにより、ローカルおよびリモート構成が上書きされ、リモートで変更することはできません。
次の例は、Collectモジュールの構成を指定しています。プログラムで構成されていない他の構成はリモートで更新できます。

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile("custom_profile")
        .setOverrideDomain("custom_domain")
}
```




## トラッキング

イベントをトラッキングするには、イベント名とオプションのタイプおよびデータを `track()` メソッドに渡します。イベント名はデータレイヤーに `tealium_event` として表示されます。



イベントをトラッキングするには、[track()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) を呼び出します。

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```


イベントをトラッキングするには、[track()](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) を呼び出します。

```swift
/// 基本的なトラック、デフォルトのイベントタイプと空のデータレイヤーで。
tealium.track("homepage")

/// フルパラメータでトラック
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

/// 異なるビュータイプでトラック
tealium.track("homepage", type: .view)
```


## データレイヤー

データレイヤーにデータを追加するには：



データレイヤーの値を取得するには、[get()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) メソッドを使用し、結果またはエラーを処理する必要がある場合は購読します：
```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // customerIdを使って何かをする
}
```

データレイヤーの値を構成するには、[put()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) メソッドを使用します：
```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
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



データレイヤーの値を取得するには、[get()](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを呼び出します：
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

データレイヤーオブジェクトを構成するには `DataObject()` を使用します：

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones", "/ja/early-access/tealium-prism/quick-start"]
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

詳細については、[LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html) を参照してください。


ログレベルを構成するには、[TealiumConfig ビルダー](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html)の構成で `setMinLogLevel()` を呼び出します：

```swift
var config = TealiumConfig(account: "your_account",
                           profile: "your_profile",
                           environment: "dev",
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace) // または .debug, .info, .warn, .error, .silent
})
```



### トレース

[モバイルトレースツール](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool) は、TealiumモバイルSDKからのライブイベントを表示するためにデバイスでスキャンできるQRコードを提供します。



[トレースインターフェース](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/) の使用方法について学びます。

```kotlin
trace.join("TRACE_ID")

// 現在のトレースセッションを離れる
trace.leave()

// テストのために訪問の終了を強制する
trace.forceEndOfVisit()
```


[トレースプロトコルリファレンス](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html) の使用方法について学びます。

```swift
// トレースセッションに参加する
tealium.trace.join(id: "TRACE_ID")

// 現在のトレースセッションを離れる
tealium.trace.leave()

// テストのために訪問の終了を強制する
tealium.trace.forceEndOfVisit()
```



### ライブイベント

[モバイルインストールのトラブルシューティングにライブイベントを使用します](https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/)。

[ライブイベント](https://docs.tealium.com/about-live-events/) についてもっと学びます。