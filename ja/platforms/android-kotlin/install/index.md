---
title: インストール
description: Tealium SDK for Android (Kotlin)のインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/install/
---
## 必要条件

* [Android Studio](https://developer.android.com/studio)
* Android SDK (Lollipop/5.0+ / API Level 21+)
* [Tealium iQ モバイルプロファイル](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub アカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Android (Kotlin) の[サンプルアプリ](https://github.com/Tealium/tealium-kotlin/tree/master/mobile)を探索して、Tealiumライブラリ、イベントのトラッキング、およびベストプラクティスの実装についての知識を深めましょう。

さらに、Tealiumの機能を中央のヘルパークラスに抽象化することをお勧めします。私たちの[サンプルヘルパークラス](https://github.com/Tealium/tealium-kotlin/blob/master/mobile/src/main/java/com/tealium/mobile/TealiumHelper.kt)を探索してください。

## コードの取得

[Tealium Android ライブラリ](https://github.com/Tealium/tealium-kotlin)をクローンします。ライブラリをダウンロードするよりもクローンする方が、将来のリリースに更新しやすくなります。


<blockquote>
Android用Tealiumクラスとメソッドの完全なリストについては、[Tealium API](https://docs.tealium.com/ja/platforms/android-kotlin/api/)を参照してください。
</blockquote>


## インストール

Tealium Kotlinライブラリはモジュールに分かれています。可能な限りインストールサイズを小さく保つために、必要な機能を実現するために必要なモジュールのみをインストールすることをお勧めします。

Mavenまたは手動でTealium Kotlinライブラリをインストールします。

### Maven

Android用TealiumライブラリをMavenでインストールするには（推奨）：

1. Tealium Maven URLをプロジェクトのトップレベルの`build.gradle`ファイルに追加します：

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

2. プロジェクトモジュールの`build.gradle`ファイルに次のMaven依存関係を追加します：

      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
      }
      ```

### 手動

Android用Tealiumライブラリを手動でインストールするには：

1. `flatDir`をプロジェクトルートの`build.gradle`ファイルに追加します：  
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

2. `tealium-kotlin-1.5.x.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。  

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：      
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin-1.6.0', ext:'aar')
      }
      ```

## 初期化

Tealiumを初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/)インスタンスを構成し、それを[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/)インスタンスに渡します。アプリのグローバルアプリケーションクラスの`onCreate()`メソッド内でTealium Kotlinライブラリを初期化することをお勧めします。


<blockquote>
トラッキングヘルパークラスを使用して[`Tealium`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#class-tealium)インスタンスを管理し、Tealium Kotlinライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。
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
次の項目を置き換えてください：
* `ACCOUNT`: ライブラリを初期化するために使用するTealiumアカウント名（小文字）。
* `PROFILE`: ライブラリを初期化するために使用するTealiumプロファイル名（小文字）。
* `DATASOURCE_ID`: TealiumデータソースID。