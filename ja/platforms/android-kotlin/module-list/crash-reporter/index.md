---
title: クラッシュレポーターモジュール
description: アプリケーションのクラッシュ追跡イベントを提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/crash-reporter/
---
## インストール

Maven（推奨）または手動でクラッシュレポーターモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：  
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```
2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとクラッシュレポーターのMaven依存関係を追加します：  
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-crash-reporter:1.1.1&#39;
      }
      ```

### 手動

クラッシュレポーターを手動でインストールするには：

1. Tealiumの[クラッシュレポーター](https://github.com/Tealium/tealium-kotlin/tree/master/crashreporter)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.crashreporter-1.1.1.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.crashreporter-1.1.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## 初期化

次の例に示すように、クラッシュレポーターモジュールを初期化します：

```kotlin
val config = TealiumConfig(application,
              &#34;ACCOUNT&#34;,
              &#34;PROFILE&#34;,
              ENVIRONMENT,
              modules = mutableSetOf(Modules.CrashReporter), // Crash Reporter module
              dispatchers = mutableSetOf(Dispatchers.Collect,
              Dispatchers.TagManagement,
              Dispatchers.RemoteCommands)
)
```

クラッシュレポーターのスタックトレースを切り捨てるには、構成オプション `truncateCrashReporterStackTraces` を `true` に構成します（デフォルトは `false`）。

```java
config.truncateCrashReporterStackTraces = true
```

## トラッキングされるイベント

初期化されると、クラッシュレポーターモジュールは自動的にクラッシュデータをキャプチャします。スレッドが突然終了すると、`.uncaughtExceptionHandler()`が呼び出され、クラッシュ情報がディスクに保存されます。次回の起動時に、保存されたクラッシュ情報が他のイベントと一緒にディスパッチされます。

クラッシュイベントは `tealium_event=&#34;crash&#34;` としてトラッキングされます。

クラッシュレポーターはシングルトンインスタンスの呼び出しです。現在、ハンドラのチェーン化はサポートされていません。

## データレイヤー

クラッシュレポーターモジュールは、イベント内で以下のクラッシュ属性を送信します：

| 変数            | タイプ           | 説明                                                                                          |
|:----------------|:-----------------|:-----------------------------------------------------------------------------------------------------|
| `crash_cause`   | String           | 例外のタイプ                                                                                   |
| `crash_count`   | Number           | インストール以降の各クラッシュに対するインクリメントカウンター                                                  |
| `crash_name`    | String           | 例外メッセージ                                                                                |
| `crash_threads` | Array of Strings | クラッシュしたスレッドのデータを含むJSON文字列の配列、スレッドIDとスタックトレースを含む |
| `crash_uuid`    | String           | 各クラッシュイベントに対する16文字の一意のID                                                          |

例：

```json
{
  &#34;tealium_event&#34; : &#34;crash&#34;,
  &#34;crash_cause&#34;   : &#34;java.lang.RuntimeException&#34;,
  &#34;crash_count&#34;   : &#34;1&#34;,
  &#34;crash_name&#34;    : &#34;Connection refused by server&#34;,
  &#34;crash_threads&#34; : [
    &#34;{ \&#34;crashed\&#34;: \&#34;true\&#34;, \&#34;state\&#34;: \&#34;RUNNABLE\&#34;, \&#34;threadNumber\&#34;: \&#34;1\&#34;, \&#34;threadId\&#34;: \&#34;main\&#34;, \&#34;priority\&#34;: \&#34;5\&#34;, \&#34;stack\&#34;:  [ { \&#34;fileName\&#34;: \&#34;MainActivity.java\&#34;, \&#34;className\&#34;: \&#34;com.tealium.libraryproject.MainActivity$1\&#34;, \&#34;methodName\&#34;: \&#34;onClick\&#34;, \&#34;lineNumber\&#34;: \&#34;38\&#34; }] }&#34;
  ],
  &#34;crash_uuid&#34;    : &#34;3c91d707-949e-445f-8ad1-4d6e200bfd6f&#34;
}
```

