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
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとクラッシュレポーターのMaven依存関係を追加します：  
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-crash-reporter:1.1.1'
      }
      ```

### 手動

クラッシュレポーターを手動でインストールするには：

1. Tealiumの[クラッシュレポーター](https://github.com/Tealium/tealium-kotlin/tree/master/crashreporter)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.crashreporter-1.1.1.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.crashreporter-1.1.1', ext:'aar')
      }
      ```

## 初期化

次の例に示すように、クラッシュレポーターモジュールを初期化します：

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
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

クラッシュイベントは `tealium_event="crash"` としてトラッキングされます。


<blockquote>
クラッシュレポーターはシングルトンインスタンスの呼び出しです。現在、ハンドラのチェーン化はサポートされていません。
</blockquote>


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
  "tealium_event" : "crash",
  "crash_cause"   : "java.lang.RuntimeException",
  "crash_count"   : "1",
  "crash_name"    : "Connection refused by server",
  "crash_threads" : [
    "{ \"crashed\": \"true\", \"state\": \"RUNNABLE\", \"threadNumber\": \"1\", \"threadId\": \"main\", \"priority\": \"5\", \"stack\":  [ { \"fileName\": \"MainActivity.java\", \"className\": \"com.tealium.libraryproject.MainActivity$1\", \"methodName\": \"onClick\", \"lineNumber\": \"38\" }] }"
  ],
  "crash_uuid"    : "3c91d707-949e-445f-8ad1-4d6e200bfd6f"
}
```

