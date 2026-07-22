---
title: ライフサイクル追跡モジュール
description: アプリのライフサイクル追跡イベントを提供します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/lifecycle-tracking/
---
## インストール

Mavenまたは手動でライフサイクル追跡モジュールをインストールします。

### Maven

Mavenを使用してライフサイクル追跡モジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      // すべてのサブプロジェクト/モジュールに共通の構成オプションを追加するトップレベルのビルドファイル。
      allprojects {
      repositories {
            mavenCentral()
            // Tealium Mavenリポジトリディレクティブ
            maven {
            url "https://maven.tealiumiq.com/android/releases/"
            }
      }
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、次のMaven依存関係を追加します：
      ```groovy
      dependencies {
      // まだ追加されていない場合のみ追加
      implementation 'com.tealium:library:5.8.0'
      // ライフサイクルを依存関係リストに追加
      implementation 'com.tealium:lifecycle:1.1.4'
      }
      ```

### 手動

ライフサイクル追跡モジュールを手動でインストールするには、次の手順を実行します：

1. Tealiumの [ライフサイクル追跡モジュール](https://github.com/Tealium/tealium-android/tree/master/Modules/LifeCycle) モジュールをダウンロードします。

2. ファイル `tealium.lifecycle-1.1.4.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium.lifecycle-1.1.4', ext:'aar')
      }
      ```

## 自動追跡イベント

モジュールは、`lifecycle_type` 変数によって構成される次のライフサイクルイベントを追跡します：

| ライフサイクルイベント | 説明 |
| --- | --- |
| `launch` | 最初の `onActivityResumed` が発生したときに生成されます。`onActivityPaused` が `onActivityResumed` の前に呼び出される場合（ライブラリが `Activity` ライフサイクルの途中で初期化される場合）、モジュール作成時間が `launch` イベントを生成するために使用されます。 |
| `sleep` | `onActivityPaused` が呼び出されてから5秒後、そして `onActivityResumed` が呼び出されなかった場合に生成されます。これは、新しいビューが表示されていないため、アプリケーションがバックグラウンドに移動したことを示しています。 |
| `wake` |  最後の `onActivityPaused` から5秒以上経過して `onActivityResumed` が発生したときに生成されます。これは、アプリがフォアグラウンドに移動しているため、`onActivityResumed` が呼び出され、ビューの変更がないことを示しています。 |

Tealiumのライフサイクル追跡は、使用状況をアクティビティライフサイクルとだけ関連付けます。

ライブラリは [Application.ActivityLifecycleCallbacks](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html) APIを利用し、その条件を [onActivityResumed](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityResumed%28android.app.Activity%29) と [onActivityPaused](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityPaused%28android.app.Activity%29) で評価します。

次のコードで有効にします：

```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
boolean isAutoTracking = true;

// ライフサイクル追跡のための追加インスタンス
LifeCycle.setupInstance("INSTANCE_NAME", config, isAutoTracking);
// 標準のTealiumインスタンス
Tealium.createInstance("INSTANCE_NAME", config);
```

## 手動追跡イベント

特定のライフサイクルパラダイムと非標準的なライフサイクル追跡に利用可能です。このアプローチは、ほとんどの実装には推奨されません。手動のライフサイクル追跡を許可するには、ライフサイクルの初期化コードを更新して `isAutoTracking` を `false` に構成します。

`launch` イベントを手動で追跡するには、`trackLaunchEvent()` メソッドを呼び出します：

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map<String, String> data = new HashMap<>();
    data.put("boot_time", "5ms");

    lifeCycle.trackLaunchEvent(data);
}
```

`sleep` イベントを手動で追跡するには、`trackSleepEvent()` メソッドを呼び出します：

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map<String, String> data = new HashMap<>();
    data.put("foreground_time", "4000ms");

    lifeCycle.trackSleepEvent(data);
}
```

`wake` イベントを手動で追跡するには、`trackWakeEvent()` メソッドを呼び出します：

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
Tealiumと添付されたLifeCycleマルチトンは、Tealium iQの公開構成によりリモートで停止可能です。インスタンスを取得してそのメソッドを呼び出すときにNullチェックを実行してください。
</blockquote>


## クラッシュ検出

`launch` イベントが `wake` イベントに続くか、その逆の場合、これはアプリが正常に `sleep` しなかったため、クラッシュが発生したことを示しています。前述のシーケンスがTealiumライブラリのシャットダウンのために発生した場合、これはクラッシュイベントとは見なされません。

クラッシュイベントが検出されると、`launch` または `wake` イベントデータに `lifecycle_diddetectcrash` 変数が追加されます。

```javascript
{
    "lifecycle_type" : "launch",
    "lifecycle_diddetectcrash" : "true",
    //...
}
```

## データレイヤー

ライフサイクル追跡モジュールは、リストされたライフサイクルイベントタイプ（`launch`、`wake`、`sleep`）に対して以下の追加変数を追加します：

| 変数 | タイプ | 説明 | 例 | イベント |
| --- | --- | --- | --- | --- |
| `lifecycle_ dayofweek_local` | `Number` | コールが行われたローカルの曜日、例えば1=日曜日、2=月曜日 | `2` | all |
| `lifecycle_ dayssincelaunch` | `Number` | 最初の起動からの日数（整数増分）| `23` | all |
| `lifecycle_ dayssinceupdate` | `Number` | 最後に検出されたアプリバージョンの更新からの日数（整数増分）| `46` | all |
| `lifecycle_ dayssincelastwake` | `Number` | 最後に検出された起動からの日数（整数増分） | `1` | all |
| `lifecycle_ diddetectcrash` | `Boolean` | 前回のスリープイベントが欠けていることから推測されるクラッシュ（起動イベントがウェイクイベントに続く場合のみ存在） | [`true`, `false`] | launch |
| `lifecycle_ firstlaunchdate` | `String` | 最初に検出された起動/ウェイクのGMTタイムスタンプ（UTCからのISO 8601形式） | `"2013-07-11T17:55:04Z"`  | all  |
| `lifecycle_ firstlaunchdate_ MMDDYYYY ` | `String` | MM/DD/YYYY形式のGMTタイムスタンプ  | `"01/17/2012"` |  all |
| `lifecycle_ hourofday_local` | `String` | コールが行われたローカルの時間（24時間形式）  | `"12"` |  all |
| `lifecycle_ isfirstlaunch` | `Boolean` |コールが最初の起動コールである場合のみ存在 | [`true`, `false`] | launch |
| `lifecycle_ isfirstlaunchupdate` | `Boolean` |検出された更新後の最初の起動である場合のみ存在  | [`true`, `false`] | launch |
| `lifecycle_ isfirstwakemonth` | `Boolean` |コールが月の最初の起動/ウェイクである場合のみ存在 | [`true`, `false`] | launch, wake  |
| `lifecycle_ isfirstwaketoday` | `Boolean` |コールが日の最初の起動/ウェイクである場合のみ存在   | [`true`, `false`] | launch, wake |
| `lifecycle_ launchcount` | `Number` |あなたのアプリのこのバージョンの起動の総数（最後の更新以降） |  `3` |  all |
| `lifecycle_ secondsawake` | `Number` |最後の起動/ウェイク以降、アプリがスリープ解除していた全秒数（`lifecycle_type:sleep` または `lifecycle_type:terminate` コールでのみ送信） |  `30` | all  |
| `lifecycle_ priorsecondsawake ` | `Number` |最後の起動以降、アプリがスリープ解除していた全秒数 - すべての前回のウェイクからの合計（`lifecycle_type:launch` コールでのみ送信）  | `126` |  all |
| `lifecycle_ sleepcount` | `Number` |あなたのアプリがスリープに入った回数の総数（更新されるとリセット） |  `5`  |  all |
| `lifecycle_ totalcrashcount` | `Number` |インストール以降のクラッシュの総数（アプリが削除されるまでリセットされません）  |`21 ` |  全て |
| `lifecycle_ totallaunchcount` | `Number` |インストール以降の起動回数の総数（アプリが削除されるまでリセットされません）  | `3`  |  全て |
| `lifecycle_ totalsecondsawake` | `Number` |アプリが起動/アクティブ状態になってからの総秒数（アプリが削除されるまでリセットされません） | `36` |  全て |
| `lifecycle_ totalsleepcount` |`Number` | アプリがバックグラウンドに移行した回数の総数（アプリが削除されるまでリセットされません） |  `400` |  全て |
| `lifecycle_ totalwakecount` | `Number` |インストール以降の起動回数 + 起動回数の総数（アプリが削除されるまでリセットされません）  |`563` |  全て |
| `lifecycle_type` | `String` | ライフサイクル呼び出しのタイプ |  [`"initial"`, `"launch"`, `"wake"`, `"sleep"`, `"terminate"`] |  全て |
| `lifecycle_ updatelaunchdate` | `String` |バージョンアップデートが検出された後の最初の起動/起動のGMTタイムスタンプ | `"2014-09-08T18:10:01Z"` |  全て |
| `lifecycle_ wakecount` | `Number` | このバージョンのアプリでの起動回数 + 起動回数の総数（更新されるとリセットされます） | ` 29` |  全て |


## API リファレンス

ライフサイクルトラッキングモジュールのメソッドの完全なリファレンスについては、Tealium SDK for Android APIの [`LifeCycle`](https://tealium.github.io/tealium-android/com/tealium/lifecycle/LifeCycle.html) クラスを参照してください。