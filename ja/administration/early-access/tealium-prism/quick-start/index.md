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
            url = URI(&#34;https://maven.tealiumiq.com/android/releases/&#34;)
        }
    }
}
```

プロジェクトモジュールの `build.gradle` ファイルに以下の依存関係を追加します。`platform()` エントリーのバージョン番号のみを指定する必要があります：

```ruby
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-core&#34;)
implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
implementation(&#34;com.tealium.prism:prism-moments-api&#34;)  
```



Swift Package Managerを使用してTealium Prism Swiftをインストールするには：

1. Xcodeプロジェクトで、**File &gt; Swift Packages &gt; Add Package Dependency**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-prism-swift`。
1. バージョンルールを構成します。**次のメジャーバージョンまで**を構成することをお勧めします。現在のTealium Prism Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールを選択し、Xcodeプロジェクトの各アプリターゲットにモジュールを追加します。**Frameworks &gt; Libraries &amp; Embedded Content**の下にあります。

Cocoapodsを使用してインストールする場合、podfileに以下の行を追加します：

```ruby
pod &#39;tealium-prism&#39;
```



## 初期化




Tealiumを初期化するには、[`TealiumConfig`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/) インスタンスを [`Tealium.create()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/) メソッドに渡します。Tealium Kotlinライブラリはアプリのグローバルアプリケーションクラスの `onCreate()` メソッド内で初期化することをお勧めします。

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig

val config = TealiumConfig.Builder(
   accountName = &#34;my_account&#34;,
   profileName = &#34;my_profile&#34;,
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



Tealiumを初期化するには、[`TealiumConfig`](/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) インスタンスを [`Tealium.create()`](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) 静的メソッドに渡します。

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json&#34;)
let tealium = Tealium.create(config: config)
```

リモート構成を使用しない場合、または異なるデフォルトを提供するために構成のローカルコピーが必要な場合は、ローカル構成ファイルを指定します：

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           settingsFile: &#34;my_settings&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json&#34;)
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

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
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
                           settingsFile: &#34;my_settings&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json&#34;,
)
let tealium = Tealium.create(config: config)
```

各モジュールは追加のプログラム構成を指定できます。これにより、ローカルおよびリモート構成が上書きされ、リモートで変更することはできません。
次の例は、Collectモジュールの構成を指定しています。プログラムで構成されていない他の構成はリモートで更新できます。

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile(&#34;custom_profile&#34;)
        .setOverrideDomain(&#34;custom_domain&#34;)
}
```




## トラッキング

イベントをトラッキングするには、イベント名とオプションのタイプおよびデータを `track()` メソッドに渡します。イベント名はデータレイヤーに `tealium_event` として表示されます。



イベントをトラッキングするには、[track()](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) を呼び出します。

```kotlin
tealium.track(&#34;user_login&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;1234567890&#34;)
})
```


イベントをトラッキングするには、[track()](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) を呼び出します。

```swift
/// 基本的なトラック、デフォルトのイベントタイプと空のデータレイヤーで。
tealium.track(&#34;homepage&#34;)

/// フルパラメータでトラック
tealium.track(&#34;user_login&#34;, type: .event, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])

/// 異なるビュータイプでトラック
tealium.track(&#34;homepage&#34;, type: .view)
```


## データレイヤー

データレイヤーにデータを追加するには：



データレイヤーの値を取得するには、[get()](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) メソッドを使用し、結果またはエラーを処理する必要がある場合は購読します：
```kotlin
tealium.dataLayer.getString(&#34;customer_id&#34;).subscribe { result -&gt;
    val customerId = result.getOrNull()
    // customerIdを使って何かをする
}
```

データレイヤーの値を構成するには、[put()](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) メソッドを使用します：
```kotlin
tealium.dataLayer.put(&#34;my_string&#34;, &#34;my_string_value&#34;)
```

データレイヤーオブジェクトを構成するには `DataObject.Builder()` を使用します：
```kotlin
val globalContext = DataObject.Builder()
    .put(&#34;customer_id&#34;, &#34;12345&#34;)
    .put(&#34;is_logged_in&#34;, true)
    .put(&#34;consent_status&#34;, &#34;consented&#34;)
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```

個々の `put` 操作は、各呼び出しが独立して順番に実行されるため、原子性が必要ない場合にのみ使用します。複数の値を構成し、タイミングや一貫性が重要な場合は、`transactionally` を使用してすべての更新を単一の原子操作で適用し、すべてが成功するかすべてが失敗するようにします。

```kotlin
tealium.dataLayer.transactionally { editor -&gt;
    editor.put(&#34;key&#34;, &#34;value&#34;.asDataItem(), Expiry.SESSION)
        .put(&#34;key2&#34;, &#34;value2&#34;.asDataItem(), Expiry.SESSION)
        .remove(&#34;key2&#34;)
        .commit()
}.onFailure {
    Log.d(&#34;DataLayer&#34;, &#34;Transactional update failed: ${it.message}&#34;)
}
```

配列値を構成するには `DataList.Builder()` を使用します：
```kotlin
val productCategories = DataList.create {
  add(&#34;electronics&#34;)
  add(&#34;headphones&#34;)
}

dataLayer.put(
    key = &#34;product_category&#34;,
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -&gt; })
```

データの有効期限を構成するには `Expiry` を使用します：
```kotlin
dataLayer.put(
    key = &#34;currency&#34;,
    value = DataItem(any = &#34;USD&#34;),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = &#34;order_total&#34;,
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```



データレイヤーの値を取得するには、[get()](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを呼び出します：
```swift
tealium.dataLayer.get(key: &#34;customer_id&#34;,
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print(&#34;Optional Value: \(String(describing: value))&#34;)
    case .failure(let error):
        print(&#34;Error: \(error)&#34;)
    }
}
```

データレイヤーの値を構成するには、[`put()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを使用します。

```swift
tealium.dataLayer.put(key: &#34;some_key&#34;, value: &#34;some value&#34;)
```

データレイヤーオブジェクトを構成するには `DataObject()` を使用します：

```swift
tealium.dataLayer.put(data: [
    &#34;customer_id&#34;: &#34;12345&#34;,
    &#34;is_logged_in&#34;: true,
    &#34;consent_status&#34;: &#34;consented&#34;,
    &#34;product_category&#34;: [&#34;electronics&#34;, &#34;headphones&#34;, &#34;/ja/early-access/tealium-prism/quick-start&#34;]
])
```

データの有効期限を構成するには [`Expiry`](/tealium-prism-swift/TealiumPrismCore/Enums/Expiry.html) を使用します：
```swift
tealium.dataLayer.put(key: &#34;currency&#34;, 
                      value: &#34;USD&#34;, 
                      expiry: .untilRestart)

tealium.dataLayer.put(key: &#34;order_total&#34;, 
                      value: 249.95, 
                      expiry: .after(Date().advanced(by: 1000)))
```



## 検証

ログファイルを検査し、トレースを実行し、ライブイベントを表示してデータを検証します。

### ログ



ログレベルを構成するには、`TealiumConfig` ビルダーの構成で `setLogLevel()` を呼び出します：

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings -&gt;
    settings.setLogLevel(LogLevel.WARN)
  }
```

詳細については、[LogLevel](/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html) を参照してください。


ログレベルを構成するには、[TealiumConfig ビルダー](/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html)の構成で `setMinLogLevel()` を呼び出します：

```swift
var config = TealiumConfig(account: &#34;your_account&#34;,
                           profile: &#34;your_profile&#34;,
                           environment: &#34;dev&#34;,
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace) // または .debug, .info, .warn, .error, .silent
})
```



### トレース

[モバイルトレースツール](/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool) は、TealiumモバイルSDKからのライブイベントを表示するためにデバイスでスキャンできるQRコードを提供します。



[トレースインターフェース](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/) の使用方法について学びます。

```kotlin
trace.join(&#34;TRACE_ID&#34;)

// 現在のトレースセッションを離れる
trace.leave()

// テストのために訪問の終了を強制する
trace.forceEndOfVisit()
```


[トレースプロトコルリファレンス](/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html) の使用方法について学びます。

```swift
// トレースセッションに参加する
tealium.trace.join(id: &#34;TRACE_ID&#34;)

// 現在のトレースセッションを離れる
tealium.trace.leave()

// テストのために訪問の終了を強制する
tealium.trace.forceEndOfVisit()
```



### ライブイベント

[モバイルインストールのトラブルシューティングにライブイベントを使用します](/ja/platforms/getting-started-mobile/troubleshooting/)。

[ライブイベント]() についてもっと学びます。