---
title: Crash Reporterモジュール
description: アプリケーションのクラッシュトラッキングイベントを提供します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/crash-reporter/
---
## 要件

* [Tealium for Android](/ja/platforms/android-java/)（5.0.0以降）

## インストール

Crash ReporterモジュールをMavenによって、または手動でインストールします。

### Maven

Crash ReporterモジュールをMavenによってインストールするには：

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenレポジトリを追加します。
```groovy
// Top-level build file where you add configuration options common to all sub-projects/modules.
allprojects {
      repositories {
        mavenCentral()
        // Tealium Maven repo directive
        maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
        }
      }
  }
```

2. プロジェクトモジュールの`build.gradle`ファイルに、以下のようにMavenの依存関係を追加します。
```groovy
dependencies {
      // only add if not already present
      implementation &#39;com.tealium:library:5.8.0&#39;
      // add crash reporter to list of dependencies
      implementation &#39;com.tealium:crashreporter:1.1.0&#39;
}
```

### 手動

Crash Reporterモジュールを手動でインストールするには：

1. Tealium [Crash Reporter](https://github.com/Tealium/tealium-android/tree/master/Modules/CrashReporter)モジュールをダウンロードします。

2. ファイル `tealium.crashreporter-1.1.0.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

3. Tealiumライブラリの依存関係をプロジェクトモジュールの`build.gradle`ファイルに追加します。
```groovy
dependencies {
      implementation (name:&#39;tealium.crashreporter-1.1.0&#39;, ext:&#39;aar&#39;)
}
```


## 初期化

Crash Reporterモジュールを次の例に示すように初期化します。

```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);

//Enable Crash Reporter
CrashReporter.initialize(BuildConfig.TEALIUM_MAIN, config, true);

//Standard Tealium instance
Tealium.createInstance(&#34;INSTANCE_NAME&#34;, config);
```

## トラッキングされるイベント

Crash Reporterモジュールを初期化した後は、モジュールによってクラッシュデータが自動的にキャプチャされます。スレッドが突然終了した場合は、 `.uncaughtExceptionHandler()` が呼び出され、クラッシュ情報がディスクに保存されます。次回起動時に、保存されたクラッシュ情報が他のイベントとともにディスパッチされます。

クラッシュイベントは`tealium_event=&#34;crash&#34;`としてトラッキングされます。

Crash Reporterは単一インスタンスコールです。チェーンハンドラーは現在サポートされていません。

## データレイヤー

Crash Reporterモジュールでは、イベントの次のクラッシュ属性を送信します。

| 変数 | 型| 説明| 例|
| --- | ---| --- | --- |
| `crash_cause` | `String` | 例外の種類| `java.lang.RuntimeException` |
| `crash_count` | `Number` | インストール以降クラッシュのたびに増分されるカウンター| `1` |
| `crash_name` | `String` | 例外メッセージ|`&#34;Connection refused by server&#34;` |
| `crash_threads` | `[String]` | スレッドIDやスタックトレースなど、クラッシュしたスレッドのデータを含むJSON文字列の配列| ` [&#39;{ &#34;crashed&#34;: &#34;true&#34;, &#34;state&#34;: &#34;RUNNABLE&#34;, &#34;threadNumber&#34;: &#34;1&#34;, &#34;threadId&#34;: &#34;main&#34;, &#34;priority&#34;: &#34;5&#34;, &#34;stack&#34;:  [ { &#34;fileName&#34;: &#34;MainActivity.java&#34;, &#34;className&#34;: &#34;com.tealium.libraryproject.MainActivity$1&#34;, &#34;methodName&#34;: &#34;onClick&#34;, &#34;lineNumber&#34;: &#34;38&#34; }] }&#39;]` |
| `crash_uuid` | `String` | 各クラッシュイベントの16文字の一意ID| `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

## 統合

*  [New Relic Mobileクラッシュトラッキングコネクタ](https://community.tealiumiq.com/t5/Customer-Data-Hub/New-Relic-Mobile-Crash-Tracking-Setup-Guide/ta-p/20849)

## APIリファレンス

Crash Reporterモジュールのメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`CrashReporter`](https://tealium.github.io/tealium-android/com/tealium/crashreporter/CrashReporter.html)クラスを参照してください。
