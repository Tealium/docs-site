---
title: インストール
description: Android（Kotlin）およびiOS（Swift）用のTealium Prism SDKをインストールして初期化します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/install/
---
## 要件



* [Android Studio](https://developer.android.com/studio)
* Android SDK（Lollipop/5.0+ / APIレベル21+）
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealiumアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)


* Xcode 14.0+
* iOS 12.0+, macOS 10.14+, tvOS 12.0+, watchOS 4.0+
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealiumアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)



## インストール

Tealium Prismライブラリはモジュールに分かれています。リソースフットプリントを小さく保つために必要なモジュールのみをインストールしてください。利用可能なモジュールのリストについては、[モジュール](https://docs.tealium.com/modules/)を参照してください。



### Maven

Mavenを使用してTealium Prism Kotlinライブラリをインストールするには：

1. Tealium Maven URLをプロジェクトのトップレベルの`build.gradle`ファイルに追加します：

    ```kotlin
    dependencyResolutionManagement {
        repositories {
            // .. 他のリポジトリ
            maven {
                url = URI("https://maven.tealiumiq.com/android/releases/")
            }
        }
    }
    ```

1. プロジェクトモジュールの`build.gradle`ファイルに以下の依存関係を追加します。`platform()`エントリーにのみバージョン番号を指定する必要があります：

    ```kotlin
    implementation(platform("com.tealium.prism:prism-bom:0.4.0"))
    implementation("com.tealium.prism:prism-core")
    implementation("com.tealium.prism:prism-lifecycle")
    implementation("com.tealium.prism:prism-moments-api")
    ```



### Swiftパッケージマネージャー（推奨）

Swift Package Managerを使用してTealium Prism Swiftをインストールするには：

1. Xcodeプロジェクトで**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-prism-swift`。
1. バージョンルールを構成します。**Up to next major**を使用することをお勧めします。現在のTealium Prismライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールを選択し、モジュールをインストールするアプリターゲットを選択します。

### CocoaPods

CocoaPodsでインストールするには、Podfileに次の行を追加します：

```ruby
pod 'tealium-prism'
```

### Carthage

Carthageでインストールするには：

1. Cartfileに次の内容を追加します：
    ```bash
    github "tealium/tealium-prism-swift"
    ```
1. iOS、macOS、tvOS、およびwatchOS用のフレームワークを生成するには、次のコマンドを実行します：
    ```sh
    carthage update --use-xcframeworks
    ```
1. 必要なフレームワークをXcodeプロジェクトの**General > Embedded Binaries**セクションにドラッグします。



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

コード内の次のプレースホルダーを置き換えてください：

* `my_account`: Tealiumアカウント名（小文字）。
* `my_profile`: Tealiumプロファイル名（小文字）。
* `Environment.PROD`: Tealiumを初期化する環境（`DEV`, `QA`, `PROD`）。



Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html)インスタンスを[`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html)静的メソッドに渡します。


<blockquote>
Tealiumインスタンスをトラッキングヘルパークラスで管理することをお勧めします。これにより、Tealium iOSライブラリの単一のエントリポイントが提供され、将来のアップグレードが簡素化されます。
</blockquote>


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
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")
let tealium = Tealium.create(config: config)
```

コード内の次のプレースホルダーを置き換えてください：

* `my_account`: Tealiumアカウント名（小文字）。
* `my_profile`: Tealiumプロファイル名（小文字）。
* `prod`: Tealiumを初期化する環境（`dev`, `qa`, `prod`）。



## 構成

Prismは3層の構成優先順位システムを使用します。構成は次の優先順位でマージされます：

| 層 | 優先順位 | 説明 |
| :--- | :--- | :--- |
| プログラム | 1（最高） | セキュリティクリティカルなIDおよび環境ロック。上書きできません。 |
| リモートJSON | 2 | バッチサイズやサンプリングなどの運用構成のリアルタイム更新。 |
| ローカルJSON | 3（最低） | アプリにバンドルされたデフォルトのフォールバック構成。 |

この優先順位順序は、重要またはセキュリティに敏感な構成が低優先順位のソースによって誤って上書きされることがないようにします。

### リモートおよびローカル構成



`TealiumConfig.Builder`を使用してリモートおよびローカル構成を構成します：

```kotlin
val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(Modules.collect())
).build()
```


<blockquote>
リモート構成は、アカウント、プロファイル、および環境に基づいて自動的にフェッチされます。Kotlin SDKはこれらの値から構成URLを解決します。
</blockquote>



リモート構成URLを指定するには`settingsUrl`パラメータを使用し、ローカルのフォールバックとして`settingsFile`パラメータを使用します：

```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

リモート構成を使用しない場合、またはそれらの構成のローカルコピーを異なるデフォルトで提供する場合は、`settingsFile`を指定し、`settingsUrl`を省略します。


### ログレベル



ログレベルを構成するには、`TealiumConfig` ビルダーの構成で `setLogLevel()` を呼び出します：

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

詳細については、[LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html)を参照してください。


ログレベルを構成するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html)の強制構成ビルダーで `setMinLogLevel()` を呼び出します：

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

利用可能なログレベル：`.trace`, `.debug`, `.info`, `.warn`, `.error`, `.silent`。



### モジュール固有の強制構成



`TealiumConfig.Builder`でモジュール固有の構成を構成します：

```kotlin
val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(
        Modules.collect(),
        Modules.lifecycle(),
       )
).configureSettings { settings ->
    settings.setLogLevel(LogLevel.DEBUG)
}.build()
```


各モジュールは `Modules.collect { }` クロージャパターンを使用して追加のプログラム構成を指定できます。これにより、ローカルおよびリモートの構成が上書きされ、リモートで変更することはできません。

次の例は、Collectモジュールの構成を指定しています。プログラムで構成されていない他の構成はリモートで更新できます。

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile("custom_profile")
        .setOverrideDomain("custom_domain")
}
```

