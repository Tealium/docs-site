---
title: ライフサイクルトラッキングモジュール
description: アプリのライフサイクル追跡イベントを提供します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/lifecycle-tracking/
---
## インストール

ライフサイクルトラッキングモジュールは、Maven または手動でインストールできます。

### Maven

Maven を使用してライフサイクルトラッキングモジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の `build.gradle` ファイルに、次の Maven リポジトリを追加します。
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

2. プロジェクトモジュールの `build.gradle` ファイルに、次の Maven 依存関係を追加します。
      ```groovy
      dependencies {
      // only add if not already present
      implementation 'com.tealium:library:5.8.0'
      // add lifecycle to list of dependencies
      implementation 'com.tealium:lifecycle:1.1.4'
      }
      ```

### 手動

ライフサイクルトラッキングモジュールを手動でインストールするには、次の手順を実行します。

1. Tealium の[ライフサイクルトラッキングモジュール](https://github.com/Tealium/tealium-android/tree/master/Modules/LifeCycle)をダウンロードします。

2. `tealium.lifecycle-1.1.4.aar` ファイルを、プロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリの依存関係を追加します。
      ```groovy
      dependencies {
            implementation(name:'tealium.lifecycle-1.1.4', ext:'aar')
      }
      ```

## 自動追跡イベント

このモジュールは、`lifecycle_type` 変数によって構成される次のライフサイクルイベントを追跡します。

| ライフサイクルイベント | 説明 |
| --- | --- |
| `launch` | 最初に発生した `onActivityResumed` で生成されます。`onActivityResumed` より前に `onActivityPaused` が呼び出された場合（`Activity` のライフサイクルの途中でライブラリが初期化された場合）、モジュールの作成時刻を使用して `launch` イベントが生成されます。 |
| `sleep` | `onActivityPaused` が呼び出された後、`onActivityResumed` が呼び出されないまま5秒が経過すると生成されます。新しいビューが表示されていないため、アプリケーションがバックグラウンドに移行したことを示します。 |
| `wake` | 最後の `onActivityPaused` から5秒以上経過した後、`onActivityResumed` の実行中に生成されます。これは、ビューの変更ではなく、アプリがフォアグラウンドに移行したために `onActivityResumed` が呼び出されたことを示します。 |

Tealium のライフサイクルトラッキングは、利用状況をアクティビティのライフサイクルにのみ関連付けます。

このライブラリは [Application.ActivityLifecycleCallbacks](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html) API を利用し、[onActivityResumed](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityResumed%28android.app.Activity%29) および [onActivityPaused](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityPaused%28android.app.Activity%29) で条件を評価します。

次のコードで有効にします。

```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
boolean isAutoTracking = true;

// Additional instance for Lifecycle Tracking
LifeCycle.setupInstance("INSTANCE_NAME", config, isAutoTracking);
// Standard Tealium instance
Tealium.createInstance("INSTANCE_NAME", config);
```

## 手動追跡イベント

特定のライフサイクルパラダイムや、一般的ではないライフサイクルトラッキングで使用できます。この方法は、ほとんどの実装では推奨されません。ライフサイクルを手動で追跡できるようにするには、ライフサイクルの初期化コードを更新して、`isAutoTracking` を `false` に構成します。

`launch` イベントを手動で追跡するには、`trackLaunchEvent()` メソッドを呼び出します。

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map<String, String> data = new HashMap<>();
    data.put("boot_time", "5ms");

    lifeCycle.trackLaunchEvent(data);
}
```

`sleep` イベントを手動で追跡するには、`trackSleepEvent()` メソッドを呼び出します。

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map<String, String> data = new HashMap<>();
    data.put("foreground_time", "4000ms");

    lifeCycle.trackSleepEvent(data);
}
```

`wake` イベントを手動で追跡するには、`trackWakeEvent()` メソッドを呼び出します。

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map<String, String> data = new HashMap<>();
    data.put("background_time", "600000ms");

    lifeCycle.trackWakeEvent(data);
}
```


<blockquote>
Tealium および関連付けられた LifeCycle マルチトンは、タグ管理のパブリッシュ構成によってリモートから無効化できます。インスタンスを取得してそのメソッドを呼び出す際は、Null チェックを実行してください。
</blockquote>


## クラッシュ検出

`launch` イベントの後に `wake` イベントが続いた場合、またはその逆の場合は、アプリが正常に `sleep` しなかったため、クラッシュが発生したことを示します。前述のシーケンスが Tealium ライブラリのシャットダウンによって発生した場合、クラッシュイベントとは見なされません。

クラッシュイベントが検出されると、`launch` または `wake` イベントのデータに `lifecycle_diddetectcrash` 変数が追加されます。

```javascript
{
    "lifecycle_type" : "launch",
    "lifecycle_diddetectcrash" : "true",
    //...
}
```
## データレイヤー

Lifecycle Trackingモジュールは、指定されたライフサイクルイベントタイプ（`launch`、`wake`、`sleep`）に対して、以下の変数を追加します。

| 変数 | 型 | 説明 | 例 | イベント |
| --- | --- | --- | --- | --- |
| `lifecycle_ dayofweek_local` | `Number` | 呼び出しが行われたローカルの曜日。例：1=日曜日、2=月曜日 | `2` | すべて |
| `lifecycle_ dayssincelaunch` | `Number` | 初回起動からの経過日数（整数単位）| `23` | すべて |
| `lifecycle_ dayssinceupdate` | `Number` | 最後に検出されたアプリのバージョン更新からの経過日数（整数単位）| `46` | すべて |
| `lifecycle_ dayssincelastwake` | `Number` | 最後に検出されたウェイクからの経過日数（整数単位） | `1` | すべて |
| `lifecycle_ diddetectcrash` | `Boolean` | 直前のスリープイベントが欠落していることから推測されたクラッシュ（ウェイクイベントの後に起動イベントが続く場合にのみ存在） | [`true`, `false`] | launch |
| `lifecycle_ firstlaunchdate` | `String` | 最初に検出された起動／ウェイクのGMTタイムスタンプ（UTCを基準としたISO 8601形式） | `"2013-07-11T17:55:04Z"` | すべて |
| `lifecycle_ firstlaunchdate_ MMDDYYYY ` | `String` | MM/DD/YYYY形式のGMTタイムスタンプ | `"01/17/2012"` | すべて |
| `lifecycle_ hourofday_local` | `String` | 呼び出しが行われたローカル時刻の時間（24時間形式） | `"12"` | すべて |
| `lifecycle_ isfirstlaunch` | `Boolean` | 呼び出しが初回の起動呼び出しである場合にのみ存在 | [`true`, `false`] | launch |
| `lifecycle_ isfirstlaunchupdate` | `Boolean` | 更新が検出された後の最初の起動呼び出しである場合にのみ存在 | [`true`, `false`] | launch |
| `lifecycle_ isfirstwakemonth` | `Boolean` | その月の最初の起動／ウェイク呼び出しである場合にのみ存在 | [`true`, `false`] | launch、wake |
| `lifecycle_ isfirstwaketoday` | `Boolean` | その日の最初の起動／ウェイク呼び出しである場合にのみ存在 | [`true`, `false`] | launch、wake |
| `lifecycle_ launchcount` | `Number` | 現在のアプリバージョンでの起動回数の合計（最後の更新以降） | `3` | すべて |
| `lifecycle_ secondsawake` | `Number` | 最後のウェイク／起動以降、アプリが起動状態だった秒数（整数）。`lifecycle_type:sleep`または`lifecycle_type:terminate`の呼び出しでのみ送信 | `30` | すべて |
| `lifecycle_ priorsecondsawake ` | `Number` | 最後の起動以降、アプリが起動状態だった秒数（整数）。それ以前のすべてのウェイクからの合計を集計（`lifecycle_type:launch`の呼び出しでのみ送信） | `126` | すべて |
| `lifecycle_ sleepcount` | `Number` | アプリがスリープ状態になった回数の合計（更新時にリセット） | `5` | すべて |
| `lifecycle_ totalcrashcount` | `Number` | インストール以降にカウントされたクラッシュ回数の合計（アプリが削除された場合にのみリセット） |`21 ` | すべて |
| `lifecycle_ totallaunchcount` | `Number` | インストール以降の起動回数の合計（アプリが削除された場合にのみリセット） | `3` | すべて |
| `lifecycle_ totalsecondsawake` | `Number` | アプリのインストール以降、アプリがウェイク／アクティブ状態だった秒数の合計（アプリが削除された場合にのみリセット） | `36` | すべて |
| `lifecycle_ totalsleepcount` |`Number` | アプリのインストール以降、アプリがバックグラウンドに移行した回数の合計（アプリが削除された場合にのみリセット） | `400` | すべて |
| `lifecycle_ totalwakecount` | `Number` | インストール以降の起動回数とウェイク回数の合計（アプリが削除された場合にのみリセット） |`563` | すべて |
| `lifecycle_type` | `String` | ライフサイクル呼び出しのタイプ | [`"initial"`, `"launch"`, `"wake"`, `"sleep"`, `"terminate"`] | すべて |
| `lifecycle_ updatelaunchdate` | `String` | バージョン更新が検出された後、最初に行われたウェイク／起動のGMTタイムスタンプ | `"2014-09-08T18:10:01Z"` | すべて |
| `lifecycle_ wakecount` | `Number` | 現在のアプリバージョンでの起動回数とウェイク回数の合計（更新時にリセット） | ` 29` | すべて |


## APIリファレンス

Lifecycle Trackingモジュールのメソッドに関する完全なリファレンスについては、Tealium SDK for Android APIの[`LifeCycle`](https://tealium.github.io/tealium-android/com/tealium/lifecycle/LifeCycle.html)クラスを参照してください。