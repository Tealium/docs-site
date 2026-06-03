---
title: モバイル用クイックスタートガイド
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/quick-start/
---
## インストール

[Android](/ja/platforms/android-java/install)または[iOS](/ja/platforms/ios-swift/install)用のTealiumのインストールから始めましょう。



Mavenを使用してAndroidライブラリのTealiumをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します：

      ```ruby
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに以下のMaven依存関係を追加します：

      ```ruby
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.X.X&#39;
      }
      ```
最新のリリースは[Github](https://github.com/tealium/tealium-kotlin/releases)で確認し、1.X.Xを最新のリリース番号に置き換えてください。



Swift Package Managerを使用してiOSライブラリのTealiumをインストールするには：

1. Xcodeプロジェクトで**File &gt; Swift Packages &gt; Add Package Dependency**を選択します
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
3. バージョンルールを構成します。通常、**Up to next major**が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールするモジュールを選択し、Xcodeプロジェクトの**Frameworks &gt; Libraries &amp; Embedded Content**の各アプリターゲットにモジュールを追加します



## 初期化

[Android](/ja/platforms/android-java/install/#initialize)または[iOS](/ja/platforms/ios-swift/install/#initialize)用のTealiumの初期化から始めましょう。




Tealiumを初期化するには、[`TealiumConfig`](/ja/platforms/android-kotlin/api/tealium-config/)インスタンスを構成し、それを[`Tealium`](/ja/platforms/android-kotlin/api/tealium/)インスタンスに渡します。Tealium Kotlinライブラリは、アプリのグローバルアプリケーションクラスの`onCreate()`メソッド内で初期化することをお勧めします。

[`Tealium`](/ja/platforms/android-kotlin/api/tealium/#class-tealium)インスタンスをトラッキングヘルパークラスを使用して管理し、Tealium Kotlinライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。

```kotlin
object TealiumHelper {

  lateinit var tealium: Tealium

  fun init(application: Application) {
    val tealiumConfig = TealiumConfig(
                      application,
                      &#34;ACCOUNT&#34;,
                      &#34;PROFILE&#34;,
                      Environment.DEV,
                      dataSourceId = &#34;DATASOURCE_ID&#34;,  //optional
                      modules = mutableSetOf(VisitorService),
                      dispatchers = mutableSetOf(TagManagement, Collect)
                    )
    tealium = Tealium.create(&#34;tealium_instance&#34;, tealiumConfig)
  }
}
```




Tealiumを初期化するには、[`TealiumConfig`](/ja/platforms/ios-swift/api/tealium-config/)インスタンスを[`Tealium()`](/ja/platforms/ios-swift/api/tealium/#tealium)コンストラクタに渡します。

[`Tealium`](/ja/platforms/ios-swift/api/tealium/#class-tealium)インスタンスをトラッキングヘルパークラスを使用して管理し、Tealium iOSライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。

```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)
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
        tealium?.dataLayer.add(&#34;mykey&#34;, &#34;myvalue&#34;, expiry: .forever)

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

モバイルパブリッシュ構成はデフォルトで有効になっており、使用しない場合は無効にする必要があります。iQタグ管理でモバイルパブリッシュ構成を構成するか、`config.shouldUseRemotePublishSettings = false`を使用して無効にしてください。




## トラッキング

[Android](/ja/platforms/android-kotlin/track/)または[iOS](/ja/platforms/ios-swift/track/)のビューやイベントのトラッキングを始めましょう。

### ビューのトラッキング

画面ビューをトラッキングするには、`TealiumView(viewName:dataLayer:)`のインスタンスを`track()`メソッドに渡します。`TealiumView`は、データレイヤーに`tealium_event`として表示されるビュー名と、オプションのデータ辞書で構成されています。



ビューをトラッキングするには：  
```kotlin
val tealView = TealiumView(&#34;screen_view&#34;, mutableMapOf(&#34;screen_name&#34; to &#34;Home&#34;))
tealium.track(tealView);
```



ビューをトラッキングするには：  
```swift
let tealView = TealiumView(&#34;screen_view&#34;, dataLayer: [&#34;screen_name&#34;: &#34;Home&#34;])
tealium?.track(tealView)
```




### イベントのトラッキング

ビュー以外のイベントをトラッキングするには、`TealiumEvent(eventName:dataLayer:)`のインスタンスを`track()`メソッドに渡します。`TealiumEvent`は、データレイヤーに`tealium_event`として表示されるイベント名と、オプションのデータ辞書で構成されています。



イベントをトラッキングするには：  
```kotlin
val tealEvent = TealiumEvent(&#34;user_login&#34;, mutableMapOf(&#34;customer_id&#34; to &#34;1234567890&#34;))
tealium.track(tealEvent);
```



イベントをトラッキングするには：  
```swift
let tealEvent = TealiumEvent(&#34;user_login&#34;, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])
tealium?.track(tealEvent)
```

[`track()`](/ja/platforms/ios-swift/api/tealium/#track)メソッドは、イベント名とオプションのデータ辞書を含む`TealiumDispatch`タイプの`TealiumEvent`を受け入れてイベントをトラッキングします。


## データレイヤー

[Android](/ja/platforms/android-kotlin/data-layer/)または[iOS](/ja/platforms/ios-swift/data-layer/)で、一般的なデータレイヤー値と各モジュールによって提供されるデータの管理を始めましょう。

データレイヤーにデータを追加するには：



`String` 値を構成するには、[putString()](/ja/platforms/android-kotlin/api/data-layer/#putstring) メソッドを使用します：
```kotlin
tealium.dataLayer.putString(&#34;my_string&#34;, &#34;my_string_value&#34;)
```

異なるデータタイプについても、メソッドは `put` で始まります。例えば、整数には [putInt()](/ja/platforms/android-kotlin/api/data-layer/#putint)、浮動小数点数の配列には [putDoubleArray()](/ja/platforms/android-kotlin/api/data-layer/#getdoublearray) を使用します。異なる[データタイプ](/ja/platforms/android-kotlin/data-layer/#data-types)についてのメソッドをさらに学びましょう。

1日後に期限切れになる `String` 値を構成するには：
```kotlin
tealium.dataLayer.putString(&#34;my_string&#34;, &#34;my_string_value&#34;, Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

[有効期限のタイプ](/ja/platforms/android-kotlin/data-layer/#data-expiration)についてさらに学びましょう。


任意のタイプの値を構成するには、[`add()`](/ja/platforms/ios-swift/api/tealium-data-layer/#add) メソッドを使用します：
```swift
tealium.dataLayer.add(key: &#34;my_value&#34;, value: 123456)
```

1日後に期限切れになる任意のタイプの値を構成するには：
```swift
tealium?.dataLayer.add(key: &#34;my_value&#34;, value: 123456, expiry: .afterCustom((.days, 1)))
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



Tealium AudienceStream を使用している場合、`visitorId` は訪問に関連付けられた匿名 ID です。[AudienceStream での匿名 ID]()についてさらに学びましょう。

### ユーザー識別子

既知のユーザーを識別する場合、永続的なデータ保存にユーザー識別子属性を追加します。

[AudienceStream でのユーザー識別子]()についてさらに学びましょう。



ユーザー識別子を追加するには、例えば顧客 ID を：
```kotlin
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString(&#34;customer_id&#34;, id, Expiry.FOREVER)
}
```


ユーザー識別子を追加するには、例えば顧客 ID を：
```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: &#34;customer_id&#34;, value: id, expiry: .forever)
}
```



## 検証

ログファイルを検査し、トレースを実行し、ライブイベントを表示することでデータを検証します。

### ログ

[Android](/ja/platforms/android-kotlin/install/#log-level)または[iOS](/ja/platforms/ios-swift/install/#log-level)のログについて始めましょう。



ログレベルを構成するには、[`logLevel`](/ja/platforms/android-kotlin/api/tealium-config/#loglevel) プロパティを構成します：

```kotlin
Logger.logLevel = LogLevel.DEV // または LogLevel.QA, LogLevel.PROD
```


ログレベルを構成するには、[`logLevel`](/ja/platforms/ios-swift/api/tealium-config/#loglevel) プロパティを構成します：

```swift
config.logLevel = .debug // または .info, .error, .fault, .silent
```



### トレース

[Android](/ja/platforms/android-kotlin/track/#trace)または[iOS](/ja/platforms/ios-swift/track/#trace)の[トレース](/ja/platforms/getting-started-mobile/trace/)について始めましょう。



トレースに参加するには、[joinTrace()](/ja/platforms/android-kotlin/api/tealium/#jointrace) メソッドを呼び出します：

```kotlin
Tealium[&#34;INSTANCE_NAME&#34;]?.joinTrace(&#34;TRACE_ID&#34;)
```

トレースを離れるには、[leaveTrace()](/ja/platforms/android-kotlin/api/tealium/#leavetrace) メソッドを呼び出します：

```kotlin
Tealium[&#34;INSTANCE_NAME&#34;]?.leaveTrace()
```


トレースに参加するには、[joinTrace()](/ja/platforms/ios-swift/api/tealium/#jointrace) メソッドを呼び出します：

```swift
tealium?.joinTrace(id: &#34;TRACE_ID&#34;)
```

トレースを離れるには、[leaveTrace()](/ja/platforms/ios-swift/api/tealium/#leavetrace) メソッドを呼び出します：

```swift
tealium?.leaveTrace()
```




[モバイルトレースツール](/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool)は、デバイスでスキャン可能なQRコードを提供することでトレース機能をエンリッチメントし、TealiumモバイルSDKからのイベントを迅速に表示できます。

### ライブイベント

Tealium EventStreamのライブイベント機能は、[モバイルインストールのトラブルシューティング](/ja/platforms/getting-started-mobile/troubleshooting/)の目的で全てのTealium顧客に利用可能です。

[ライブイベント]()の使用についてさらに学びましょう。