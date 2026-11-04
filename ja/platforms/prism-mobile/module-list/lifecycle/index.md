---
title: ライフサイクルモジュール
description: 起動、復帰、スリープなどのアプリのライフサイクルイベントを追跡します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/
---
## 仕組み

Lifecycleモジュールは、アプリのライフサイクルイベントを追跡し、追跡対象イベントにライフサイクル指標を追加します。Lifecycleモジュールは、アプリの起動、フォアグラウンドへの移行（復帰）、バックグラウンドへの移行（スリープ）を自動的に検出します。

### イベント名

このモジュールは、次のライフサイクルイベントを追跡します。

| イベント | 説明 |
| :--- | :--- |
| `launch` | セッション内でアプリが初めて起動したときに追跡されます。 |
| `wake` | アプリがフォアグラウンドに戻ったときに追跡されます。 |
| `sleep` | アプリがバックグラウンドに移行したときに追跡されます。 |

### クラッシュ検出

Lifecycleモジュールは、先行するsleepイベントなしでlaunchイベントが発生した場合に、クラッシュが発生したと推測します。次回の起動時に、`lifecycle_diddetectcrash`が`true`に構成され、`lifecycle_totalcrashcount`が増加します。

### データレイヤー

デフォルトでは、次の変数はライフサイクルイベントにのみ追加されます。すべてのトラッキング呼び出しに追加するには、`setDataTarget`に`.allEvents`（Swift）または`LifecycleDataTarget.AllEvents`（Kotlin）を渡します。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `lifecycle_dayofweek_local` | 呼び出しが行われたローカルの曜日（1 = 日曜日、7 = 土曜日） | `2` |
| `lifecycle_dayssincelaunch` | アプリの初回起動からの経過日数（整数単位） | `23` |
| `lifecycle_dayssinceupdate` | 最後に検出されたアプリバージョンの更新からの経過日数（整数単位） | `46` |
| `lifecycle_dayssincelastwake` | 最後に検出された復帰からの経過日数（整数単位） | `1` |
| `lifecycle_diddetectcrash` | 先行するsleepイベントの欠落からクラッシュが推測された場合にのみ存在します | `"true"` |
| `lifecycle_firstlaunchdate` | 最初に検出された起動のGMTタイムスタンプ（ISO 8601形式） | `"2013-07-11T17:55:04Z"` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | 最初に検出された起動のGMTタイムスタンプ（MM/DD/YYYY形式） | `"01/17/2012"` |
| `lifecycle_hourofday_local` | 呼び出しが行われたローカル時刻（24時間形式） | `"12"` |
| `lifecycle_isfirstlaunch` | 初回の起動呼び出しにのみ存在します | `"true"` |
| `lifecycle_isfirstlaunchupdate` | 検出されたアプリバージョンの更新後、最初の起動にのみ存在します | `"true"` |
| `lifecycle_isfirstwakemonth` | その月の最初の起動または復帰にのみ存在します | `"true"` |
| `lifecycle_isfirstwaketoday` | その日の最初の起動または復帰にのみ存在します | `"true"` |
| `lifecycle_launchcount` | 現在のアプリバージョンでの起動回数（更新時にリセット） | `3` |
| `lifecycle_secondsawake` | 最後の復帰または起動以降、アプリがアクティブだった秒数（整数）。`sleep`イベントとともに送信されます。 | `30` |
| `lifecycle_priorsecondsawake` | 現在の起動前にアプリがアクティブだった秒数（整数）。以前の復帰全体を集計した値です。`launch`イベントとともに送信されます。 | `126` |
| `lifecycle_sleepcount` | 現在のアプリバージョンでアプリがスリープ状態になった回数（更新時にリセット） | `5` |
| `lifecycle_totalcrashcount` | インストール以降に推測されたクラッシュの合計回数 | `21` |
| `lifecycle_totallaunchcount` | インストール以降の起動の合計回数 | `3` |
| `lifecycle_totalsecondsawake` | インストール以降、アプリがフォアグラウンドにあった合計秒数 | `36` |
| `lifecycle_totalsleepcount` | インストール以降、アプリがバックグラウンドに移行した合計回数 | `400` |
| `lifecycle_totalwakecount` | インストール以降の起動および復帰の合計回数 | `563` |
| `lifecycle_type` | ライフサイクルイベントの種類 | `"launch"`, `"wake"`, `"sleep"` |
| `lifecycle_updatelaunchdate` | バージョン更新後、最初の起動または復帰のGMTタイムスタンプ（ISO 8601形式） | `"2014-09-08T18:10:01Z"` |
| `lifecycle_wakecount` | 現在のアプリバージョンでの起動および復帰の合計回数（更新時にリセット） | `29` |

## インストール



`build.gradle`ファイルに`prism-lifecycle`依存関係を追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-lifecycle")
```


リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用して、`TealiumPrismLifecycle`をSwift Package Managerの依存関係として追加します。



## 初期化

モジュールを初期化するには、`TealiumConfig`の`modules`リストに追加します。



```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.lifecycle(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                               Modules.lifecycle(),
                               // other modules...
                           ])
```



## 手動トラッキング

ライフサイクルイベントを手動で追跡するには、自動ライフサイクルトラッキングを無効にして、次のメソッドを使用します。



```kotlin
Modules.lifecycle { settings ->
    settings.setAutoTrackingEnabled(false)
}
```


```swift
Modules.lifecycle { settings in
    settings.setAutoTrackingEnabled(false)
}
```



任意のデータオブジェクトを指定して、ライフサイクルイベントメソッドを呼び出します。


<blockquote>
自動ライフサイクルトラッキングが有効な状態でこれらのメソッドを呼び出すと、エラーが発生します。
</blockquote>




```kotlin
tealium.lifecycle.launch(dataObject)
tealium.lifecycle.wake(dataObject)
tealium.lifecycle.sleep(dataObject)
```


```swift
tealium.lifecycle().launch(dataObject)
tealium.lifecycle().wake(dataObject)
tealium.lifecycle().sleep(dataObject)
```

