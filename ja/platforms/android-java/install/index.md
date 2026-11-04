---
title: インストール
description: Android（Java）向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-java/install/
---
## 要件

* [Android Studio](https://developer.android.com/studio)
* Android（KitKat／4.4以降／APIレベル19以降）
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Tealiumのライブラリ、トラッキングメソッド、および実装のベストプラクティスについて理解を深めるには、Tealium for Androidの[サンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Samples)を参照してください。

## コードの取得

[Tealium Androidライブラリ](https://github.com/Tealium/tealium-android)をクローンします。ダウンロードする代わりにライブラリをクローンすると、今後のリリースへの更新が容易になります。


<blockquote>
Android向けTealiumのクラスとメソッドの完全な一覧については、[Tealium API](https://tealium.github.io/tealium-android/)を参照してください。
</blockquote>


## インストール

Mavenを使用するか、手動でAndroid向けTealium SDKをインストールします。

### Maven

Mavenを使用してTealium for Androidライブラリをインストールするには（推奨）：

1. プロジェクトの最上位の`build.gradle`ファイルにTealium Maven URLを追加します。

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
            implementation 'com.tealium:library:5.8.0'
      }
      ```

### 手動

Tealium for Androidライブラリを手動でインストールするには：

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

2. `tealium-5.x.x.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。  

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。      
      ```groovy
      dependencies {
            implementation(name:'tealium-5.6.1', ext:'aar')
      }
      ```

## 初期化

初期化するには、アプリの`onCreate()`メソッドに次の変更を加えます。

1. [`Tealium.Config`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/#class-tealium-config)オブジェクトのインスタンスを作成します。  
      ```java
      Tealium.Config tealConfig = Tealium.Config.create(
            this,
            "ACCOUNT",
            "PROFILE",
            "ENVIRONMENT");
      ```

2. [`setDatasourceId()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/#setdatasourceid)など、必要な追加メソッドを呼び出して構成データを指定します。
      ```java
      tealConfig.setDatasourceId("DATASOURCE_ID");
      ```

3. [`setupInstance()`](https://docs.tealium.com/ja/platforms/android-java/api/life-cycle/#setupinstance)メソッドを呼び出して、アプリのライフサイクルインスタンスを構成します。
      ```java
      LifeCycle.setupInstance("INSTANCE_NAME", config, true);
      ```

4. [`createInstance()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#createinstance)メソッドを呼び出してTealiumインスタンスを作成し、構成インスタンスをコンストラクター引数として渡します。    
      ```java
      tealium = Tealium.createInstance("INSTANCE_NAME", tealConfig);
      ```


<blockquote>
バージョン5.5.1以降でCollectが有効になっている場合、データは`Tealium.Config`オブジェクトで指定されたプロファイルに送信されます。以前のバージョンでは、データはデフォルトプロファイル（`"main"`）に送信されます。
</blockquote>


## ログレベル

ログレベルはリモートパブリッシュ構成によって制御され、初期化時に構成した環境から推定されます。

バージョン5.3.1以降では、次の例のように[`setForceOverrideLogLevel()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/#setforceoverrideloglevel)メソッドを使用して、ローカルでログレベルを上書きできます。

```java
tealConfig.setForceOverrideLogLevel("LOG_LEVEL");
```

## Cookie

モバイルプロファイルでタグ管理を有効にしている場合は、Cookieを有効にする必要があります。

Cookie管理を有効にするには、初期化ステートメントの後に次のコードを追加します。

```java
config.getEventListeners().add(createCookieEnablerListener());
private static WebViewCreatedListener createCookieEnablerListener() {
    return new WebViewCreatedListener() {
        @Override
        public void onWebViewCreated(WebView webView) {
            final CookieManager mgr = CookieManager.getInstance();
            // Accept all cookies
            mgr.setAcceptCookie(true);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
                mgr.setAcceptThirdPartyCookies(webView, true);
            }
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB_MR1) {
                CookieManager.setAcceptFileSchemeCookies(true);
            }
            Log.d(TAG, "WebView " + webView + " created and cookies enabled.");
        }
    };
}
```

このコードにより、タグ管理の`Webview`がファーストパーティ、サードパーティ、およびファイルスキームのCookieを[受け入れる](https://developer.android.com/reference/android/webkit/CookieManager.html#acceptCookie())ことができます。


<blockquote>
バージョン5.1.0以降では、`CookieManager`はデフォルトで**有効**です。バージョン5.0.4以前では、`CookieManager`はデフォルトで**無効**です。
</blockquote>


## イベントのバッチ処理

イベントのバッチ処理を有効にするには、[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)に移動し、バッチサイズを1より大きい値に構成します。キュー内のイベント数がバッチサイズと等しくなると、イベントがディスパッチされます。

イベントのディスパッチは、_バッチタイムアウト_構成に基づいてトリガーすることもできます。この構成により、バッチサイズに達しなかった場合でも、一定時間が経過するとキューがディスパッチされます。[`setSecondsBeforeBatchTimeout()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/#setsecondsbeforebatchtimeout)メソッドを呼び出して、バッチタイムアウトを構成します。

バッチサイズとバッチタイムアウトのチェックを上書きするには、[`requestFlush()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#requestflush)メソッドを呼び出して、キューを直ちにフラッシュします。


<blockquote>
デバイスがオフラインの場合、または同意マネージャーが有効になっている場合、フラッシュの上書きは機能しません。
</blockquote>



## マルチプロセスアプリ

#### Android 9以降のマルチプロセスアプリケーション

Android 9では、マルチプロセスアプリケーションにおける`WebView`のデータディレクトリに関する動作が変更されました。この変更により、`WebView`は複数のプロセス間で単一のデータディレクトリを共有しなくなりました。通常、`WebView`を使用するすべてのActivityは、同じプロセス内で実行することを推奨します。  

タグ管理モジュールを使用し、追加の`WebView`インスタンスを実装する場合は、アプリのクラッシュを防ぐため、Tealiumインスタンスを作成する前に`WebView.setDataDirectorySuffix()`を呼び出すことを推奨します。

タグ管理モジュールのCookieやWebデータにアクセスする必要がある場合は、`CookieManager.getCookie()`メソッドと`CookieManager.setCookie()`メソッドを使用して、プロセス間でコピーします。

詳しくは、[プロセスごとに分離されたWebベースのデータディレクトリ](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs)を参照してください。