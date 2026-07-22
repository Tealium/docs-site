---
title: ライフサイクルトラッキングモジュール
description: アプリのライフサイクルトラッキングイベントを提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/lifecycle-tracking/
---
## インストール

Mavenまたは手動でライフサイクルトラッキングモジュールをインストールします。

### Maven

Mavenを使用してライフサイクルトラッキングモジュールをインストールするには、次の手順を実行します。

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します:
      ```groovy
      // Top-level build file where you add configuration options common to all sub-projects/modules.
      allprojects {
          repositories {
            mavenCentral()
            // Tealium Maven repo directive
            maven {
                url "https://maven.tealiumiq.com/android/releases/"
            }
          }
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、次のMaven依存関係を追加します:
      ```groovy
      dependencies {
          // 既に存在しない場合のみ追加
          implementation 'com.tealium:kotlin-core:1.6.0'
          // ライフサイクルを依存関係のリストに追加
          implementation 'com.tealium:kotlin-lifecycle:1.2.0'
      }
      ```

### 手動

ライフサイクルトラッキングモジュールを手動でインストールするには、次の手順を実行します。

1. Tealiumの [Lifecycle Tracking Module](https://github.com/Tealium/tealium-kotlin/tree/master/lifecycle) モジュールをダウンロードします。

2. `tealium-kotlin.lifecycle-1.2.0.aar` ファイルをプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.lifecycle-1.2.0', ext:'aar')
      }
      ```

## 自動トラッキングされるイベント

モジュールは、`lifecycle_type` 変数で構成される以下のライフサイクルイベントをトラッキングします:

| ライフサイクルイベント | 説明                                                                                                                                                                                                                                                      |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `launch`              | 最初の `onActivityResumed` が発生したときに生成されます。`onActivityResumed` よりも `onActivityPaused` が先に呼び出される場合（ライブラリが `Activity` ライフサイクルの途中で初期化された場合）、モジュールの作成時刻が `launch` イベントの生成に使用されます。 |
| `sleep`               | `onActivityPaused` が呼び出されてから5秒後に `onActivityResumed` が呼び出されなかった場合に生成されます。これは、新しいビューが表示されなかったためにアプリがバックグラウンドに移行したことを示します。                                                              |
| `wake`                | 最後の `onActivityPaused` から5秒以上経過した `onActivityResumed` 中に生成されます。これは、`onActivityResumed` がビューの変更ではなくアプリのフォアグラウンド化のために呼び出されたことを示します。                                                        |

Tealiumのライフサイクルトラッキングは、アクティビティのライフサイクルとの関連付けのみを行います。

このライブラリは、[Application.ActivityLifecycleCallbacks](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html) APIを利用し、[onActivityResumed](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityResumed%28android.app.Activity%29) および [onActivityPaused](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityPaused%28android.app.Activity%29) で条件を評価します。

以下のコードで有効になります:

```kotlin
val config = TealiumConfig(
                applicaiton,
                "accountName",
                "profileName",
                Environment.DEV,
                modules = mutableSetOf(Modules.Lifecycle)
                )
```


## 手動トラッキングされるイベント

特定のライフサイクルパラダイムや非標準的なライフサイクルトラッキングに使用できます。ほとんどの実装にはおすすめしません。手動ライフサイクルトラッキングを許可するには、ライフサイクルの初期化コードで `isAutoTrackingEnabled` を `false` に構成します。

### 構成オプション

```kotlin
val config = TealiumConfig(...)

config.isAutoTrackingEnabled = false
```

`launch` イベントを手動でトラッキングするには、`trackLaunchEvent()` メソッドを呼び出します:

```kotlin
tealium.lifecycle?.trackLaunchEvent()
```

`sleep` イベントを手動でトラッキングするには、`trackSleepEvent()` メソッドを呼び出します:

```kotlin
tealium.lifecycle?.trackSleepEvent()
```

`wake` イベントを手動でトラッキングするには、`trackWakeEvent()` メソッドを呼び出します:

```kotlin
tealium.lifecycle?.trackWakeEvent()
```

## クラッシュ検出

`launch` イベントが `wake` イベントの後に続くか、その逆の場合、これはアプリが正常に `sleep` しなかったことを示し、クラッシュが発生したことを示します。前述のシーケンスがTealiumライブラリのシャットダウンによるものである場合、これはクラッシュイベントとは見なされません。

クラッシュイベントが検出されると、`launch` または `wake` イベントのデータに `lifecycle_diddetectcrash` 変数が追加されます。

```javascript
{
    "lifecycle_type" : "launch",
    "lifecycle_diddetectcrash" : "true",
    //...
}
```

## データレイヤー

ライフサイクルトラッキングモジュールは、次の追加変数をリストされたライフサイクルイベントタイプ（`launch`、`wake`、`sleep`）に追加します:

| 変数                                    | タイプ    | 説明                                                                                                                                   | 例                                                             | イベント      |
|:----------------------------------------|:----------|:--------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------|:-------------|
| `lifecycle_ dayofweek_local`            | `Number`  | 呼び出しが行われたローカルの曜日。1=日曜日、2=月曜日など                                                                                   | `2`                                                           | すべて         |
| `lifecycle_ dayssincelaunch`            | `Number`  | 整数の増分で最初の起動からの日数                                                                                                       | `23`                                                          | すべて         |
| `lifecycle_ dayssinceupdate`            | `Number`  | 整数の増分で最後に検出されたアプリのバージョンの更新からの日数                                                                             | `46`                                                          | すべて         |
| `lifecycle_ dayssincelastwake`          | `Number`  | 整数の増分で最後に検出された起動からの日数                                                                                               | `1`                                                           | すべて         |
| `lifecycle_ diddetectcrash`             | `Boolean` | 前の `sleep` イベントがないことから推測されるクラッシュ（`launch` イベントが `wake` イベントに続く場合のみ存在）                                                                 | [`true`, `false`]                                             | launch       |
| `lifecycle_ firstlaunchdate`            | `String`  | ISO 8601形式のUTC時間からの最初の検出された起動/起床のGMTタイムスタンプ                                                                 | `"2013-07-11T17:55:04Z"`                                      | すべて         |
| `lifecycle_ firstlaunchdate_ MMDDYYYY ` | `String`  | MM/DD/YYYYとしてフォーマットされたGMTタイムスタンプ                                                                                     | `"01/17/2012"`                                                | すべて         |
| `lifecycle_ hourofday_local`            | `String`  | 呼び出しが行われたローカルの時間（24時間形式）                                                                                           | `"12"`                                                        | すべて         |
| `lifecycle_ isfirstlaunch`              | `Boolean` | 呼び出しが最初の起動呼び出しである場合のみ存在                                                                                           | [`true`, `false`]                                             | launch       |
| `lifecycle_ isfirstlaunchupdate`        | `Boolean` | 呼び出しが最初の更新後の起動である場合のみ存在                                                                                           | [`true`, `false`]                                             | launch       |
| `lifecycle_ isfirstwakemonth`           | `Boolean` | 呼び出しが月の最初の起動/起床である場合のみ存在                                                                                         | [`true`, `false`]                                             | launch, wake |
| `lifecycle_ isfirstwaketoday`           | `Boolean` | 呼び出しが日の最初の起動/起床である場合のみ存在                                                                                         | [`true`, `false`]                                             | launch, wake |
| `lifecycle_ launchcount`                | `Number`  | このバージョンのアプリの総起動回数（最後の更新以降）                                                                                     | `3`                                                           | すべて         |
| `lifecycle_ secondsawake`               | `Number`  | 最後の起動/起床からのアプリの起動時間（`lifecycle_type:sleep` または `lifecycle_type:terminate` 呼び出しのみ送信）                      | `30`                                                          | すべて         |
| `lifecycle_ priorsecondsawake `         | `Number`  | 最後の起動からのアプリの起動時間（`lifecycle_type:launch` 呼び出しのみ送信）                                                               | `126`                                                         | すべて         |
| `lifecycle_ sleepcount`                 | `Number`  | アプリがバックグラウンドに移行した回数の合計（更新されるとリセットされる）                                                                   | `5`                                                           | すべて         |
| `lifecycle_ totalcrashcount`            | `Number`  | インストール後のクラッシュの合計数（アプリが削除されるまでリセットされない）                                                                 | `21 `                                                         | すべて         |
| `lifecycle_ totallaunchcount`           | `Number`  | インストール後の起動の合計数（アプリが削除されるまでリセットされない）                                                                       | `3`                                                           | すべて         |
| `lifecycle_ totalsecondsawake`          | `Number`  | アプリの起動/アクティブ状態の合計秒数（アプリが削除されるまでリセットされない）                                                             | `36`                                                          | すべて         |
| `lifecycle_ totalsleepcount`            | `Number`  | アプリがバックグラウンドに移行した回数の合計（アプリが削除されるまでリセットされない）                                                       | `400`                                                         | すべて         |
| `lifecycle_ totalwakecount`             | `Number`  | 起動の合計数 + 起床の合計数（アプリが削除されるまでリセットされない）                                                                      | `563`                                                         | すべて         |
| `lifecycle_type`                        | `String`  | ライフサイクル呼び出しのタイプ                                                                                                          | [`"initial"`, `"launch"`, `"wake"`, `"sleep"`, `"terminate"`] | すべて         |
| `lifecycle_ updatelaunchdate`           | `String`  | バージョンの更新後に最初の起動/起床が検出されたGMTタイムスタンプ                                                                           | `"2014-09-08T18:10:01Z"`                                      | すべて         |
| `lifecycle_ wakecount`                  | `Number`  | このバージョンのアプリの起動数 + 起床数の合計（更新されるとリセットされる）                                                                  | `29`                                                         | すべて         |


## APIリファレンス

ライフサイクルトラッキングモジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android APIの [`LifeCycle`](https://docs.tealium.com/ja/platforms/android-kotlin/api/lifecycle/) クラスを参照してください。
