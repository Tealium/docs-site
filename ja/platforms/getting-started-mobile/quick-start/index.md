---
title: モバイル用クイックスタートガイド
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/quick-start/
---
## インストール

[Android](https://docs.tealium.com/ja/platforms/android-java/install)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/install)用のTealiumのインストールから始めましょう。



Mavenを使用してAndroidライブラリのTealiumをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します：

      ```ruby
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url "https://maven.tealiumiq.com/android/releases/"
              }
            }
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに以下のMaven依存関係を追加します：

      ```ruby
      dependencies {
            implementation 'com.tealium:kotlin-core:1.X.X'
      }
      ```

<blockquote>
最新のリリースは[Github](https://github.com/tealium/tealium-kotlin/releases)で確認し、1.X.Xを最新のリリース番号に置き換えてください。
</blockquote>




Swift Package Managerを使用してiOSライブラリのTealiumをインストールするには：

1. Xcodeプロジェクトで**File > Swift Packages > Add Package Dependency**を選択します
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
3. バージョンルールを構成します。通常、**Up to next major**が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールするモジュールを選択し、Xcodeプロジェクトの**Frameworks > Libraries & Embedded Content**の各アプリターゲットにモジュールを追加します



## 初期化

[Android](https://docs.tealium.com/ja/platforms/android-java/install/#initialize)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/#initialize)用のTealiumの初期化から始めましょう。




Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/)インスタンスを構成し、それを[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/)インスタンスに渡します。Tealium Kotlinライブラリは、アプリのグローバルアプリケーションクラスの`onCreate()`メソッド内で初期化することをお勧めします。


<blockquote>
[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#class-tealium)インスタンスをトラッキングヘルパークラスを使用して管理し、Tealium Kotlinライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。
</blockquote>


```kotlin
object TealiumHelper {

  lateinit var tealium: Tealium

  fun init(application: Application) {
    val tealiumConfig = TealiumConfig(
                      application,
                      "ACCOUNT",
                      "PROFILE",
                      Environment.DEV,
                      dataSourceId = "DATASOURCE_ID",  //optional
                      modules = mutableSetOf(VisitorService),
                      dispatchers = mutableSetOf(TagManagement, Collect)
                    )
    tealium = Tealium.create("tealium_instance", tealiumConfig)
  }
}
```




Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)インスタンスを[`Tealium()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#tealium)コンストラクタに渡します。


<blockquote>
[`Tealium`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#class-tealium)インスタンスをトラッキングヘルパークラスを使用して管理し、Tealium iOSライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。
</blockquote>


```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
    var tealium: Tealium?

    private init() {

        // add necessary config options
        config.batchingEnabled = true
        config.logLevel = .debug

        // add the Collectors you want - no need to include if want all compiled collectors
        config.collectors = [Collectors.Lifecycle,
                             Collectors.Location,
                             Collectors.VisitorService]

        // add the Dispatchers you want - no need to include if want compiled dispatchers
        config.dispatchers = [Dispatchers.TagManagement,
                              Dispatchers.RemoteCommands]

        tealium = Tealium(config: config)

        // optional post init processing
        tealium?.dataLayer.add("mykey", "myvalue", expiry: .forever)

    }

    public func start() {
        _ = TealiumHelper.shared
    }

    class func trackView(title: String, data: [String: Any]?) {    
      let tealView = TealiumView(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealView)
    }

    class func trackEvent(title: String, data: [String: Any]?) {
      let tealEvent = TealiumEvent(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealEvent)
    }
}
```


<blockquote>
モバイルパブリッシュ構成はデフォルトで有効になっており、使用しない場合は無効にする必要があります。iQタグ管理でモバイルパブリッシュ構成を構成するか、`config.shouldUseRemotePublishSettings = false`を使用して無効にしてください。
</blockquote>





## トラッキング

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/track/)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/track/)のビューやイベントのトラッキングを始めましょう。

### ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(viewName:dataLayer:)`のインスタンスを`track()`メソッドに渡します。`TealiumView`は、データレイヤーに`tealium_event`として表示されるビュー名と、オプションのデータ辞書で構成されています。



ビューをトラッキングするには：  
```kotlin
val tealView = TealiumView("screen_view", mutableMapOf("screen_name" to "Home"))
tealium.track(tealView);
```



ビューをトラッキングするには：  
```swift
let tealView = TealiumView("screen_view", dataLayer: ["screen_name": "Home"])
tealium?.track(tealView)
```




### イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent(eventName:dataLayer:)`のインスタンスを`track()`メソッドに渡します。`TealiumEvent`は、データレイヤーに`tealium_event`として表示されるイベント名と、オプションのデータ辞書で構成されています。



イベントをトラッキングするには：  
```kotlin
val tealEvent = TealiumEvent("user_login", mutableMapOf("customer_id" to "1234567890"))
tealium.track(tealEvent);
```



イベントをトラッキングするには：  
```swift
let tealEvent = TealiumEvent("user_login", dataLayer: ["customer_id": "1234567890"])
tealium?.track(tealEvent)
```

[`track()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#track)メソッドは、イベント名とオプションのデータ辞書を含む`TealiumDispatch`タイプの`TealiumEvent`を受け入れてイベントをトラッキングします。


## データレイヤー

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/data-layer/)で、一般的なデータレイヤー値と各モジュールによって提供されるデータの管理を始めましょう。

データレイヤーにデータを追加するには：



`String` 値を構成するには、[putString()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putstring) メソッドを使用します：
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value")
```

異なるデータタイプについても、メソッドは `put` で始まります。例えば、整数には [putInt()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putint)、浮動小数点数の配列には [putDoubleArray()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#getdoublearray) を使用します。異なる[データタイプ](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/#data-types)についてのメソッドをさらに学びましょう。

1日後に期限切れになる `String` 値を構成するには：
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value", Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

[有効期限のタイプ](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/#data-expiration)についてさらに学びましょう。


任意のタイプの値を構成するには、[`add()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-data-layer/#add) メソッドを使用します：
```swift
tealium.dataLayer.add(key: "my_value", value: 123456)
```

1日後に期限切れになる任意のタイプの値を構成するには：
```swift
tealium?.dataLayer.add(key: "my_value", value: 123456, expiry: .afterCustom((.days, 1)))
```





## アイデンティティ解決

Tealium の匿名 ID を使用し、独自のユーザー識別子を構成する方法を学びましょう。

### 匿名 ID

Tealium ライブラリは、アプリが初めて起動されたときに一意の永続的な匿名 ID を生成します。この値は `visitorId` に保存され、各トラッキングイベントに `tealium_visitor_id` 属性として含まれます。



訪問 ID を取得するには：
```kotlin
class TealiumHelper {
	lateinit var tealium: Tealium

    fun getVisitorId(): String {
        return tealium.visitorId
    }
}
```


訪問 ID を取得するには：
```swift
class TealiumHelper {
	var tealium: Tealium?

    var visitorId: String? {
		tealium?.visitorId
	}
}
```



Tealium AudienceStream を使用している場合、`visitorId` は訪問に関連付けられた匿名 ID です。[AudienceStream での匿名 ID](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)についてさらに学びましょう。

### ユーザー識別子

既知のユーザーを識別する場合、永続的なデータ保存にユーザー識別子属性を追加します。

[AudienceStream でのユーザー識別子](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)についてさらに学びましょう。



ユーザー識別子を追加するには、例えば顧客 ID を：
```kotlin
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString("customer_id", id, Expiry.FOREVER)
}
```


ユーザー識別子を追加するには、例えば顧客 ID を：
```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: "customer_id", value: id, expiry: .forever)
}
```



## 検証

ログファイルを検査し、トレースを実行し、ライブイベントを表示することでデータを検証します。

### ログ

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/#log-level)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/#log-level)のログについて始めましょう。



ログレベルを構成するには、[`logLevel`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#loglevel) プロパティを構成します：

```kotlin
Logger.logLevel = LogLevel.DEV // または LogLevel.QA, LogLevel.PROD
```


ログレベルを構成するには、[`logLevel`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#loglevel) プロパティを構成します：

```swift
config.logLevel = .debug // または .info, .error, .fault, .silent
```



### トレース

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/track/#trace)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/track/#trace)の[トレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/)について始めましょう。



トレースに参加するには、[joinTrace()](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#jointrace) メソッドを呼び出します：

```kotlin
Tealium["INSTANCE_NAME"]?.joinTrace("TRACE_ID")
```

トレースを離れるには、[leaveTrace()](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#leavetrace) メソッドを呼び出します：

```kotlin
Tealium["INSTANCE_NAME"]?.leaveTrace()
```


トレースに参加するには、[joinTrace()](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#jointrace) メソッドを呼び出します：

```swift
tealium?.joinTrace(id: "TRACE_ID")
```

トレースを離れるには、[leaveTrace()](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#leavetrace) メソッドを呼び出します：

```swift
tealium?.leaveTrace()
```




[モバイルトレースツール](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool)は、デバイスでスキャン可能なQRコードを提供することでトレース機能をエンリッチメントし、TealiumモバイルSDKからのイベントを迅速に表示できます。

### ライブイベント

Tealium EventStreamのライブイベント機能は、[モバイルインストールのトラブルシューティング](https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/)の目的で全てのTealium顧客に利用可能です。

[ライブイベント](https://docs.tealium.com/about-live-events/)の使用についてさらに学びましょう。