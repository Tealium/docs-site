---
title: インストール
description: Android（Kotlin）向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/install/
---
## 要件

* [Android Studio](https://developer.android.com/studio)
* Android SDK（Lollipop／5.0以降／APIレベル21以降）
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Tealiumライブラリ、イベントのトラッキング、ベストプラクティスに基づく実装について理解を深めるには、Android（Kotlin）の[サンプルアプリ](https://github.com/Tealium/tealium-kotlin/tree/master/mobile)を参照してください。

また、Tealiumのすべての機能を中央のヘルパークラスに抽象化することを推奨します。[サンプルヘルパークラス](https://github.com/Tealium/tealium-kotlin/blob/master/mobile/src/main/java/com/tealium/mobile/TealiumHelper.kt)を参照してください。

## コードの取得

[Tealium Androidライブラリ](https://github.com/Tealium/tealium-kotlin)をクローンします。ライブラリをダウンロードするのではなくクローンすると、今後のリリースへの更新が容易になります。


<blockquote>
Android向けTealiumのクラスとメソッドの完全な一覧については、[Tealium API](https://docs.tealium.com/ja/platforms/android-kotlin/api/)を参照してください。
</blockquote>


## インストール

Tealium Kotlinライブラリは複数のモジュールに分割されています。インストールサイズを可能な限り小さく保つため、必要な機能を実現するためのモジュールのみをインストールすることを推奨します。

Tealium Kotlinライブラリは、Mavenまたは手動でインストールできます。

### Maven

Mavenを使用してTealium Androidライブラリをインストールするには（推奨）：

1. プロジェクトの最上位にある`build.gradle`ファイルに、Tealium Maven URLを追加します。

      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url "https://maven.tealiumiq.com/android/releases/"
              }
            }
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに、次のMaven依存関係を追加します。

      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
      }
      ```

### 手動

Tealium Androidライブラリを手動でインストールするには：

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します。  
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs 'libs'
              }
            }
      }
      ```  

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-kotlin-1.5.x.aar`を追加します。  

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。      
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin-1.6.0', ext:'aar')
      }
      ```

## 初期化

Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/)インスタンスを構成し、それを[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/)インスタンスに渡します。アプリのグローバルApplicationクラス内の`onCreate()`メソッドでTealium Kotlinライブラリを初期化することを推奨します。


<blockquote>
トラッキングヘルパークラスを使用して[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#class-tealium)インスタンスを管理してください。これにより、Tealium Kotlinライブラリへの単一のエントリポイントが提供され、今後のアップグレードが容易になります。
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
                      dispatchers = mutableSetOf(Dispatchers.Collect)
                    )
    tealium = Tealium.create("tealium_instance", tealiumConfig)
  }
}
```

次の値を置き換えます。

* `ACCOUNT`：ライブラリの初期化に使用するTealiumアカウント名（小文字）。
* `PROFILE`：ライブラリの初期化に使用するTealiumプロファイル名（小文字）。
* `DATASOURCE_ID`：TealiumデータソースID。

## ディスパッチャー

データをTealiumエコシステムに送信するには、次のディスパッチャーから選択します。

* **タグ管理**    
タグ管理を使用し、そのタグ管理構成ロジックを利用するには、[TagManagementディスパッチャー](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/)を追加します。
* **Collect**  
Tealium Customer Data Hubのサーバーサイドソリューションを使用するには、[Collectディスパッチャー](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collect/)を追加します。

## ログレベル

ログレベルは、`TealiumConfig`インスタンスの環境に基づいて構成されます。

別のログレベルを使用するには、[`logLevel`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#loglevel)プロパティを構成します。

```kotlin
config.logLevel = LogLevel.DEV // or LogLevel.QA, LogLevel.PROD
```

## Cookie

WebViewでは、Cookieがデフォルトで有効になっています。

## イベントのバッチ処理

イベントのバッチ処理は、`TealiumConfig`インスタンスでローカルに構成するか、[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を使用してリモートで構成できます。バッチサイズを1より大きい値に構成すると、バッチ処理が有効になります。キュー内のイベント数がバッチサイズと等しくなると、イベントがディスパッチされます。

次の例は、バッチ処理をローカルで構成する場合に利用できるオプションを示しています。

```kotlin
object TealiumHelper {
      private lateinit var tealium: Tealium

      fun init(app: Application) {
            config.overrideDefaultLibrarySettings = LibrarySettings(
                batching = Batching(
                    batchSize = 10,             // send in batches of 10 (default: 1)
                    maxQueueSize = 1000,        // maximum of 1000 queued events (default: 100)
                    expiration = TimeUnit.DAYS  // queue for a maxumum of 5 days (default: 86400)
                        .toSeconds(5).toInt()     
                )
            )
      }
}
```

## Javaからの移行

[Javaライブラリ](https://github.com/Tealium/tealium-android)からKotlinライブラリに移行すると、次の保存済みデータが自動的に移行されます。

* 同意構成
* ライフサイクルデータ
* 永続データ
  * [永続データ](https://docs.tealium.com/ja/platforms/android-java/data-management/#persistent-data)APIを使用して追加されたカスタム永続データ
  * Tealium永続データ：`app_uuid`、`tealium_visitor_id`


<blockquote>
Kotlinライブラリへの移行が完了すると、Javaライブラリのレガシーデータは削除されます。その後Javaライブラリに戻すと、新しい`tealium_visitor_id`と`app_uuid`が生成され、カスタム永続データは失われます。
</blockquote>


## Android Wear

Android Wear OSはWebViewをサポートしておらず、タグ管理モジュールはサポートされないため、Android Wearアプリでデータを収集するにはCollectモジュールを使用してください。


<blockquote>
Tealium for Androidを使用してAndroid Wearアプリを開発している場合、スタンドアロンアプリを作成することを[Googleは推奨しています](https://developer.android.com/training/wearables/apps/creating)。
</blockquote>


## マルチプロセスアプリ

#### Android 9以降のマルチプロセスアプリケーション

Android 9では、マルチプロセスアプリケーションの`WebView`データディレクトリに関する動作が変更されました。この変更により、単一のデータディレクトリが複数のプロセス間で`WebView`によって共有されなくなりました。通常、`WebView`を使用するすべてのActivityを同じプロセス内に配置する必要があります。  

タグ管理モジュールを使用し、追加の`WebView`インスタンスを実装する場合、アプリのクラッシュを防ぐため、Tealiumインスタンスを作成する前に`WebView.setDataDirectorySuffix()`を呼び出すことを推奨します。

タグ管理モジュールからCookieとWebデータにアクセスする必要がある場合は、`CookieManager.getCookie()`メソッドと`CookieManager.setCookie()`メソッドを使用して、プロセス間でコピーしてください。

詳細については、[プロセスごとに分離されたWebベースのデータディレクトリ](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs)を参照してください。