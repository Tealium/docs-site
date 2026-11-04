---
title: モバイル向けクイックスタートガイド
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/quick-start/
---
## インストール

[Android](https://docs.tealium.com/ja/platforms/android-java/install) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/install) 向けの Tealium をインストールします。



Maven を使用して Android 向け Tealium ライブラリをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の `build.gradle` ファイルに Tealium Maven URL を追加します。

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

2. プロジェクトモジュールの `build.gradle` ファイルに、次の Maven 依存関係を追加します。

      ```ruby
      dependencies {
            implementation 'com.tealium:kotlin-core:1.X.X'
      }
      ```

<blockquote>
[GitHub](https://github.com/tealium/tealium-kotlin/releases) で最新リリースを確認し、1.X.X を最新のリリース番号に置き換えてください。
</blockquote>




Swift Package Manager を使用して iOS 向け Tealium ライブラリをインストールするには、次の手順を実行します。

1. Xcode プロジェクトで、**File > Swift Packages > Add Package Dependency** を選択します。
2. リポジトリの URL を入力します：`https://github.com/tealium/tealium-swift`
3. バージョンルールを構成します。通常は **Up to next major** を推奨します。現在の Tealium Swift ライブラリのバージョンが一覧に表示されない場合は、Swift パッケージのキャッシュをリセットしてください。
4. インストールするモジュールを選択し、Xcode プロジェクトの **Frameworks > Libraries & Embedded Content** で、各アプリターゲットにモジュールを追加します。



## 初期化

[Android](https://docs.tealium.com/ja/platforms/android-java/install/#initialize) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/#initialize) 向けの Tealium を初期化します。




Tealium を初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/) インスタンスを構成し、それを [`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/) インスタンスに渡します。Tealium Kotlin ライブラリは、アプリのグローバルアプリケーションクラスの `onCreate()` メソッド内で初期化することを推奨します。


<blockquote>
トラッキングヘルパークラスを使用して [`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#class-tealium) インスタンスを管理してください。これにより、Tealium Kotlin ライブラリへの単一のエントリポイントが提供され、今後のアップグレードが容易になります。
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




Tealium を初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/) インスタンスを [`Tealium()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#tealium) コンストラクターに渡します。


<blockquote>
トラッキングヘルパークラスを使用して [`Tealium`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#class-tealium) インスタンスを管理してください。これにより、Tealium iOS ライブラリへの単一のエントリポイントが提供され、今後のアップグレードが容易になります。
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
モバイルパブリッシュ構成はデフォルトで有効になっているため、使用しない場合は無効にする必要があります。タグ管理でモバイルパブリッシュ構成を構成するか、`config.shouldUseRemotePublishSettings = false` を使用して無効にしてください。
</blockquote>





## トラッキング

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/track/) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/track/) でビューとイベントのトラッキングを開始します。

### ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(viewName:dataLayer:)` のインスタンスを `track()` メソッドに渡します。`TealiumView` は、データレイヤーに `tealium_event` として表示されるビュー名と、任意のデータディクショナリで構成されます。



ビューをトラッキングするには、次のようにします。  
```kotlin
val tealView = TealiumView("screen_view", mutableMapOf("screen_name" to "Home"))
tealium.track(tealView);
```



ビューをトラッキングするには、次のようにします。  
```swift
let tealView = TealiumView("screen_view", dataLayer: ["screen_name": "Home"])
tealium?.track(tealView)
```




### イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent(eventName:dataLayer:)` のインスタンスを `track()` メソッドに渡します。`TealiumEvent` は、データレイヤーに `tealium_event` として表示されるイベント名と、任意のデータディクショナリで構成されます。



イベントをトラッキングするには、次のようにします。  
```kotlin
val tealEvent = TealiumEvent("user_login", mutableMapOf("customer_id" to "1234567890"))
tealium.track(tealEvent);
```



イベントをトラッキングするには、次のようにします。  
```swift
let tealEvent = TealiumEvent("user_login", dataLayer: ["customer_id": "1234567890"])
tealium?.track(tealEvent)
```

[`track()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#track) メソッドは、イベント名と任意のデータディクショナリで構成される `TealiumEvent` 型の `TealiumDispatch` を受け取り、イベントをトラッキングします。


## データレイヤー

一般的なデータレイヤー値と各モジュールによって提供されるデータの管理を、[Android](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/data-layer/) 向けに開始します。

データレイヤーにデータを追加するには、次のようにします。  



`String` 値を構成するには、[putString()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putstring) メソッドを使用します。   
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value")
```

他のデータ型についても同様に、メソッド名は `put` で始まります。たとえば、整数には [putInt()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putint)、浮動小数点数の配列には [putDoubleArray()](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#getdoublearray) を使用します。さまざまな[データ型](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/#data-types)のメソッドについて詳しく説明します。

`String` 値を1日後に期限切れになるよう構成するには、次のようにします。  
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value", Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

[有効期限の種類](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/#data-expiration)について詳しく説明します。


任意の型の値を構成するには、[`add()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-data-layer/#add) メソッドを使用します。  
```swift
tealium.dataLayer.add(key: "my_value", value: 123456)
```

任意の型の値を1日後に期限切れになるよう構成するには、次のようにします。  
```swift
tealium?.dataLayer.add(key: "my_value", value: 123456, expiry: .afterCustom((.days, 1)))
```





## IDの解決

Tealiumの匿名IDを使用し、独自のユーザー識別子を構成する方法について説明します。

### 匿名ID

Tealiumライブラリは、アプリの初回起動時に一意で永続的な匿名IDを生成します。この値は `visitorId` に保存されます。また、この値は属性 `tealium_visitor_id` として、追跡される各イベントに含まれます。



訪問IDを取得するには、次のようにします。  
```kotlin
class TealiumHelper {
	lateinit var tealium: Tealium

    fun getVisitorId(): String {
        return tealium.visitorId
    }
}
```


訪問IDを取得するには、次のようにします。  
```swift
class TealiumHelper {
	var tealium: Tealium?

    var visitorId: String? {
		tealium?.visitorId
	}
}
```



Customer Data Platform（CDP）を使用している場合、`visitorId` は訪問に関連付けられた匿名IDです。[Customer Data Platform（CDP）の匿名ID](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)について詳しく説明します。

### ユーザー識別子

既知のユーザーを識別する場合は、永続データ保存にユーザー識別子属性を追加します。

[CDPのユーザー識別子](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)について詳しく説明します。



顧客IDなどのユーザー識別子を追加するには、次のようにします。  
```kotlin
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString("customer_id", id, Expiry.FOREVER)
}
```


顧客IDなどのユーザー識別子を追加するには、次のようにします。  
```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: "customer_id", value: id, expiry: .forever)
}
```



## 検証

ログファイルの確認、トレースの実行、ライブイベントの表示によってデータを検証します。

### ログ

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/#log-level) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/install/#log-level) のロギングを開始します。



ログレベルを構成するには、[`logLevel`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#loglevel) プロパティを構成します。

```kotlin
Logger.logLevel = LogLevel.DEV // or LogLevel.QA, LogLevel.PROD
```


ログレベルを構成するには、[`logLevel`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#loglevel) プロパティを構成します。

```swift
config.logLevel = .debug // or .info, .error, .fault, .silent
```



### トレース

[Android](https://docs.tealium.com/ja/platforms/android-kotlin/track/#trace) または [iOS](https://docs.tealium.com/ja/platforms/ios-swift/track/#trace) で[トレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/)を開始します。



トレースに参加するには、[joinTrace()](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#jointrace) メソッドを呼び出します。

```kotlin
Tealium["INSTANCE_NAME"]?.joinTrace("TRACE_ID")
```

トレースから離脱するには、[leaveTrace()](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#leavetrace) メソッドを呼び出します。

```kotlin
Tealium["INSTANCE_NAME"]?.leaveTrace()
```


トレースに参加するには、[joinTrace()](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#jointrace) メソッドを呼び出します。

```swift
tealium?.joinTrace(id: "TRACE_ID")
```

トレースから離脱するには、[leaveTrace()](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#leavetrace) メソッドを呼び出します。

```swift
tealium?.leaveTrace()
```




[モバイルトレースツール](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool)は、デバイスでスキャン可能なQRコードを提供することでトレース機能をエンリッチメントし、Tealium Mobile SDKから送信されるイベントをすばやく確認できるようにします。

### ライブイベント

Event Streamingのライブイベント機能は、[モバイルインストールのトラブルシューティング](https://docs.tealium.com/ja/platforms/getting-started-mobile/troubleshooting/)を目的として、すべてのTealiumのお客様が利用できます。

[ライブイベント](https://docs.tealium.com/about-live-events/)の使用方法について詳しく説明します。