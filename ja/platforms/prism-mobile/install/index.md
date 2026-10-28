---
title: インストール
description: Android（Kotlin）、iOS（Swift）、React Native向けTealium Prism SDKをインストールして初期化します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/install/
---
Tealium Prism SDKは、一連のモジュールとして配布されています。アプリに必要なモジュールのみをインストールし、Tealiumアカウントの認証情報を使用してSDKを初期化します。

## 要件



* [Android Studio](https://developer.android.com/studio)
* Android SDK（Marshmallow／6.0以降／APIレベル23以降）
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealiumアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)


* Xcode 16.0以降
* iOS 13.0以降、macOS 10.15以降、tvOS 13.0以降、watchOS 7.0以降
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealiumアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)


* New Architecture（TurboModules）を使用するReact Native 0.85
* Android APIレベル24以降
* iOS 15.1以降
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealiumアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)



## インストール

Tealium Prismライブラリは複数のモジュールに分割されています。リソース使用量を抑えるため、必要なモジュールのみをインストールしてください。利用可能なモジュールの一覧については、[モジュール](https://docs.tealium.com/modules/)を参照してください。



### Maven

Mavenを使用してTealium Prism Kotlinライブラリをインストールするには、次の手順を実行します。

1. プロジェクトの`settings.gradle`ファイルにTealium Maven URLを追加します。

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

1. プロジェクトモジュールの`build.gradle`ファイルに、次の依存関係を追加します。バージョン番号を指定する必要があるのは、`platform()`エントリのみです。

    ```kotlin
    implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
    implementation("com.tealium.prism:prism-core")
    implementation("com.tealium.prism:prism-lifecycle")
    implementation("com.tealium.prism:prism-context-api")
    ```



### Swift Package Manager（推奨）

Swift Package Managerを使用してTealium Prism Swiftをインストールするには、次の手順を実行します。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-prism-swift`を入力します。
1. バージョンルールを構成します。**Up to next major**の使用を推奨します。現在のTealium Prismライブラリのバージョンが一覧に表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールするモジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

### CocoaPods

CocoaPodsを使用してインストールするには、Podfileに次の行を追加します。

```ruby
pod 'tealium-prism'
```



npmを使用してコアパッケージをインストールします。

```bash
npm install @tealium/prism-react-native
```

Lifecycleモジュールをインストールするには、次のコマンドを実行します。

```bash
npm install @tealium/prism-react-native-lifecycle
```

iOSのネイティブ依存関係をインストールします。

```bash
cd ios && pod install
```

Androidでは追加の手順は必要ありません。



## 初期化




Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/)インスタンスを[`Tealium.create()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/)メソッドに渡します。アプリのグローバルアプリケーションクラス内にある`onCreate()`メソッドでTealium Kotlinライブラリを初期化することを推奨します。

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

コード内の次のプレースホルダーを置き換えます。

* `my_account`：小文字のTealiumアカウント名。
* `my_profile`：小文字のTealiumプロファイル名。
* `Environment.PROD`：Tealiumを初期化する環境（`DEV`、`QA`、または`PROD`）。



Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html)インスタンスを静的メソッド[`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html)に渡します。


<blockquote>
Tealium iOSライブラリへの単一のエントリポイントを提供し、今後のアップグレードを簡素化するトラッキングヘルパークラスを使用して、`Tealium`インスタンスを管理することを推奨します。
</blockquote>


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

コード内の次のプレースホルダーを置き換えます。

* `my_account`：小文字のTealiumアカウント名。
* `my_profile`：小文字のTealiumプロファイル名。
* `prod`：Tealiumを初期化する環境（`dev`、`qa`、または`prod`）。


Tealiumを初期化するには、アカウント、プロファイル、環境を指定して[`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create)を呼び出します。アプリの起動時にインスタンスを1つ作成し、アプリ全体で共有することを推奨します。

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

コード内の次のプレースホルダーを置き換えます。

* `my_account`：小文字のTealiumアカウント名。
* `my_profile`：小文字のTealiumプロファイル名。
* `Environment.prod`：Tealiumを初期化する環境（`Environment.dev`、`Environment.qa`、または`Environment.prod`）。



## 構成

Prismは、次の優先順位で3つのソースからの構成をマージします。

| 方法 | 優先度 | 使用する場合 |
| :--- | :--- | :--- |
| プログラムによる構成 | 1（最高） | 実行時に計算される値、またはコード内で固定する必要がある構成。 |
| リモート構成 | 2 | モジュール、バリア、変換、ルールなどの標準的な運用構成。 |
| ローカルJSON | 3 | アプリに同梱されるフォールバック用のデフォルト構成。 |

この優先順位により、重要な構成やセキュリティ上重要な構成が、優先度の低いソースによって誤って上書きされることを防ぎます。
### リモート構成とローカル構成



`TealiumConfig.Builder` を使用して、リモート構成とローカル構成を構成します。

```kotlin
val config = TealiumConfig.Builder(
   application = application,
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(Modules.collect())
).setSettingsFile("my_settings.json")
 .setSettingsUrl("https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
 .build()
```


<blockquote>
SDK は、アカウント、プロファイル、環境から構成 URL を生成しません。リモート構成を取得するには、公開済み構成ファイルの URL を `setSettingsUrl()` に渡します。詳細については、[モバイル構成の公開](https://docs.tealium.com/publish-mobile-settings/)を参照してください。
</blockquote>



リモート構成 URL を指定するには `settingsUrl` パラメータを使用し、ローカルフォールバックには `settingsFile` パラメータを使用します。

```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json")
let tealium = Tealium.create(config: config)
```

リモート構成を使用しない場合、または異なるデフォルト値を提供するためにそれらの構成のローカルコピーを使用する場合は、`settingsFile` でローカル構成ファイルを指定し、`settingsUrl` を省略します。


`settingsFile` と `settingsUrl` を `Tealium.create()` の第4引数と第5引数として渡します。構成の優先順位は、ローカルファイル < リモート URL < プログラムによる構成です。

```javascript
const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.prod,
  "my_settings.json",    // local settings file (optional)
  "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json" // remote URL (optional)
);
```

ローカル構成ファイルのみを使用するには、`settingsUrl` 引数を省略するか、`undefined` を渡します。



### ログレベル



ログレベルを構成するには、`TealiumConfig` ビルダーの構成で `setLogLevel()` を呼び出します。

```kotlin
val config = TealiumConfig.Builder(...)
  .configureCoreSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

詳細については、[LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html) を参照してください。


ログレベルを構成するには、[`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html) の強制構成ビルダーで `setMinLogLevel()` を呼び出します。

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

使用可能なログレベルは、`.trace`、`.debug`、`.info`、`.warn`、`.error`、`.silent` です。


ログレベルを構成するには、[`LogLevel`](https://docs.tealium.com/tealium-prism-react-native/types/LogLevel.html) を [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create) の第6引数として渡します。使用しない構成引数には `undefined` を渡します。

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



### モジュール固有の強制構成


<blockquote>
React Native は、モジュールごとのプログラムによる構成をサポートしていません。Tealium モバイルプロファイルまたは構成 JSON でモジュールを構成してください。
</blockquote>




`TealiumConfig.Builder` でモジュール固有の構成を構成します。

```kotlin
val config = TealiumConfig.Builder(
   application = application,
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(
        Modules.collect(),
        Modules.lifecycle(),
       )
).configureCoreSettings { settings ->
    settings.setLogLevel(LogLevel.DEBUG)
}.build()
```


各モジュールでは、`Modules.collect { }` クロージャーパターンを使用して、追加のプログラムによる構成を指定できます。この方法で指定した構成はローカル構成とリモート構成を上書きし、リモートから変更することはできません。

次の例では、Collect モジュールの構成を指定します。プログラムで構成されていないその他の構成は、リモートで更新できます。

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile("custom_profile")
        .setOverrideDomain("custom_domain")
}
```

