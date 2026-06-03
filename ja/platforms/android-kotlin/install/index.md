---
title: インストール
description: Tealium SDK for Android (Kotlin)のインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/install/
---
## 必要条件

* [Android Studio](https://developer.android.com/studio)
* Android SDK (Lollipop/5.0&#43; / API Level 21&#43;)
* [Tealium iQ モバイルプロファイル]()
* [Tealium Customer Data Hub アカウント]()

## サンプルアプリ

Android (Kotlin) の[サンプルアプリ](https://github.com/Tealium/tealium-kotlin/tree/master/mobile)を探索して、Tealiumライブラリ、イベントのトラッキング、およびベストプラクティスの実装についての知識を深めましょう。

さらに、Tealiumの機能を中央のヘルパークラスに抽象化することをお勧めします。私たちの[サンプルヘルパークラス](https://github.com/Tealium/tealium-kotlin/blob/master/mobile/src/main/java/com/tealium/mobile/TealiumHelper.kt)を探索してください。

## コードの取得

[Tealium Android ライブラリ](https://github.com/Tealium/tealium-kotlin)をクローンします。ライブラリをダウンロードするよりもクローンする方が、将来のリリースに更新しやすくなります。

Android用Tealiumクラスとメソッドの完全なリストについては、[Tealium API](/ja/platforms/android-kotlin/api/)を参照してください。

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
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに次のMaven依存関係を追加します：

      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
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
                  dirs &#39;libs&#39;
              }
            }
      }
      ```  

2. `tealium-kotlin-1.5.x.aar`を`&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に追加します。  

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：      
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin-1.6.0&#39;, ext:&#39;aar&#39;)
      }
      ```

## 初期化

Tealiumを初期化するには、[`TealiumConfig`](/ja/platforms/android-kotlin/api/tealium-config/)インスタンスを構成し、それを[`Tealium`](/ja/platforms/android-kotlin/api/tealium/)インスタンスに渡します。アプリのグローバルアプリケーションクラスの`onCreate()`メソッド内でTealium Kotlinライブラリを初期化することをお勧めします。

トラッキングヘルパークラスを使用して[`Tealium`](/ja/platforms/android-kotlin/api/tealium/#class-tealium)インスタンスを管理し、Tealium Kotlinライブラリのシングルポイントエントリを提供し、将来のアップグレードを簡素化します。

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
                      dispatchers = mutableSetOf(Dispatchers.Collect)
                    )
    tealium = Tealium.create(&#34;tealium_instance&#34;, tealiumConfig)
  }
}
```
次の項目を置き換えてください：
* `ACCOUNT`: ライブラリを初期化するために使用するTealiumアカウント名（小文字）。
* `PROFILE`: ライブラリを初期化するために使用するTealiumプロファイル名（小文字）。
* `DATASOURCE_ID`: TealiumデータソースID。