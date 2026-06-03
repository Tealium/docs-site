---
title: インストール
description: Android (Java) 向け Tealium SDK のインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/android-java/install/
---
## 要件

* [Android Studio](https://developer.android.com/studio)
* Android（KitKat/4.4以降/APIレベル19以上）
* [Tealium iQモバイルプロファイル]()
* [Tealium Customer Data Hubアカウント]()

## サンプルアプリ

当社のライブラリ、トラッキングメソッド、ベストプラクティスの実装に精通していただけるよう、Android向けTealiumの[サンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Samples)をご確認いただけるようになっています。

## コードの取得

[Tealium Androidライブラリ](https://github.com/Tealium/tealium-android)をクローンします。ライブラリをダウンロードせずクローンすることで、今後のリリースに向けたアップデートがしやすくなります。

Android向けTealiumクラスおよびメソッドの完全なリストについては、[Tealium API](https://tealium.github.io/tealium-android/)を参照してください。

## インストール

Android向けTealium SDKをMavenによって、または手動でインストールします。

### Maven

Tealium for AndroidライブラリをMavenによってインストールするには（推奨）：

1. Tealium MavenのURLを、プロジェクトの最上位にある`build.gradle`ファイルに追加します。

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

2. プロジェクトモジュールの`build.gradle`ファイルに、以下のようにMavenの依存関係を追加します。

```groovy
dependencies {
      implementation &#39;com.tealium:library:5.8.0&#39;
}
```

### 手動

Tealium for Androidライブラリを手動でインストールするには：

1. `flatDir`をプロジェクトのルートにある`build.gradle`ファイルに追加します。
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

2. `tealium-5.x.x.aar`を`&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。
```groovy
dependencies {
      implementation(name:&#39;tealium-5.6.1&#39;, ext:&#39;aar&#39;)
}
```

## 初期化

初期化するには、次の変更をアプリの`onCreate()`メソッドに加えます。

1. [`Tealium.Config`](/ja/platforms/android-java/api/tealium-config/#class-tealium-config) オブジェクトのインスタンスを作成します。
```java
Tealium.Config tealConfig = Tealium.Config.create(
        this,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        &#34;ENVIRONMENT&#34;);
```

2. 追加の必要なメソッド ( [`setDatasourceId()`](/ja/platforms/android-java/api/tealium-config/#setdatasourceid)など) を呼び出して、構成データを構成します。
```java
tealConfig.setDatasourceId(&#34;DATASOURCE_ID&#34;);
```

3. [`setupInstance()`](/ja/platforms/android-java/api/life-cycle/#setupinstance) メソッドを呼び出して、アプリのライフサイクル インスタンスを構成します。
```java
LifeCycle.setupInstance(&#34;INSTANCE_NAME&#34;, config, true);
```

4. [`createInstance()`](/ja/platforms/android-java/api/tealium/#createinstance) メソッドを呼び出して Tealium インスタンスを作成し、構成インスタンスをコンストラクタ引数として渡します。
```java
tealium = Tealium.createInstance(&#34;INSTANCE_NAME&#34;, tealConfig);
```

Collectがバージョン5.5.1以降で有効になっている場合、データは`Tealium.Config`オブジェクトで提供されるプロファイルに送信されます。それより前のバージョンでは、データはデフォルトのプロファイル（`&#34;main&#34;`）に送信されます。

## ログレベル

ログレベルはリモート公開構成により管理され、初期化の際に構成された環境から推測されます。

バージョン 5.3.1 以降、次の例に示すように [`setForceOverrideLogLevel()`](/ja/platforms/android-java/api/tealium-config/#setforceoverrideloglevel) メソッドを使用して、ログ レベルをローカルでオーバーライドすることができます。

```java
tealConfig.setForceOverrideLogLevel(&#34;LOG_LEVEL&#34;);
```

## Cookie

モバイルプロファイルでTag Managementを有効にしている場合は、Cookieを有効にする必要があります。

初期化ステートメントの後に次のコードを追加して、Cookie管理をアクティベートします。

```java
config.getEventListeners().add(createCookieEnablerListener());
private static WebViewCreatedListener createCookieEnablerListener() {
    return new WebViewCreatedListener() {
        @Override
        public void onWebViewCreated(WebView webView) {
            final CookieManager mgr = CookieManager.getInstance();
            // Accept all cookies
            mgr.setAcceptCookie(true);
            if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.LOLLIPOP) {
                mgr.setAcceptThirdPartyCookies(webView, true);
            }
            if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.HONEYCOMB_MR1) {
                CookieManager.setAcceptFileSchemeCookies(true);
            }
            Log.d(TAG, &#34;WebView &#34; &#43; webView &#43; &#34; created and cookies enabled.&#34;);
        }
    };
}
```

このコードを使用すると、タグ管理`Webview`は、ファーストパーティ、サードパーティ、およびファイルスキームのCookieを[受け入れる](https://developer.android.com/reference/android/webkit/CookieManager.html#acceptCookie()ことができます。

バージョン5.1.0以降では、`CookieManager`がデフォルトで**有効**になっています。バージョン5.0.4以前では、`CookieManager`がデフォルトで**無効**になっています。

## イベントバッチ処理

イベントバッチ処理を有効にするには、[モバイル公開構成]()に移動して、バッチサイズを1より大きい値に構成します。キュー内のイベントの数がバッチサイズと等しくなると、イベントがディスパッチされます。

イベントのディスパッチは、_バッチタイムアウト_構成に基づいてトリガーすることもできます。この構成により、バッチサイズに達していない場合でも、一定の時間が経過したときにキューがディスパッチされるようになります。バッチ タイムアウトを構成するには、メソッド [`setSecondsBeforeBatchTimeout()`](/ja/platforms/android-java/api/tealium-config/#setsecondsbeforebatchtimeout)を呼び出します。

バッチ サイズとバッチ タイムアウト チェックをオーバーライドするには、メソッド [`requestFlush()`](/ja/platforms/android-java/api/tealium/#requestflush)を呼び出してキューを即座にフラッシュします。

デバイスがオフラインであるか、Consent Managerが有効になっている場合は、フラッシュオーバーライドを行っても効果がありません。


## マルチプロセスアプリ

#### Android 9以降のマルチプロセスアプリケーション

Android 9では、マルチプロセスアプリケーションにおける`WebView`データディレクトリに関する挙動が変更されました。この変更により、複数の`WebView`がマルチプロセスで1つのデータディレクトリを共有しなくなりました。通常は、1つの`WebView`を共通して使用するActivityはいずれも、同一のプロセスで実行されます。

Tag Management モジュールを使用して `WebView`の追加のインスタンスを実装する場合は、アプリがクラッシュしないよう、Tealium のインスタンスを作成する前に `WebView.setDataDirectorySuffix()` を呼び出すことを推奨しています。

Tag Management モジュールから Cookie とウェブ データにアクセスする必要がある場合は、 `CookieManager.getCookie()` と `CookieManager.setCookie()` メソッドを使用して、プロセス間でコピーします。

詳しく知るには、 [プロセスで分けられたウェブベース データ ディレクトリ](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs) を参照します。


