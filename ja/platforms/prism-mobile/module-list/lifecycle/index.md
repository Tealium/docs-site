---
title: ライフサイクルモジュール
description: アプリのライフサイクルイベント（起動、起床、休止）を追跡します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/
---
## 動作原理

ライフサイクルモジュールはアプリのライフサイクルイベントを追跡し、追跡されたイベントにライフサイクルメトリクスを追加します。このモジュールは、アプリが起動されたとき、フォアグラウンドに移動したとき（起床）、バックグラウンドに移動したとき（休止）を自動的に検出します。

### イベント名

このモジュールは以下のライフサイクルイベントを追跡します：

| イベント | 説明 |
| :--- | :--- |
| `launch` | セッションで最初のアプリ開始時に追跡されます。 |
| `wake` | アプリがバックグラウンドから5秒以上前にフォアグラウンドに戻ったときに追跡されます。 |
| `sleep` | アプリがバックグラウンドに移動し、5秒以内にフォアグラウンドに戻らない場合に追跡されます。 |

### クラッシュ検出

ライフサイクルモジュールは、休止イベントが先行しない起動イベントが発生した場合にクラッシュを推測します。次の起動時には、`lifecycle_diddetectcrash`が`true`に構成され、`lifecycle_totalcrashcount`が増加します。

### データレイヤー

モジュールが有効な間、各トラッキングコールに以下の変数が追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `lifecycle_dayofweek_local` | コールが行われた地元の曜日（1 = 日曜日、7 = 土曜日） | `2` |
| `lifecycle_dayssincelaunch` | 最初のアプリ起動からの日数、整数で増加 | `23` |
| `lifecycle_dayssinceupdate` | 最後に検出されたアプリバージョン更新からの日数、整数で増加 | `46` |
| `lifecycle_dayssincelastwake` | 最後に検出された起床からの日数、整数で増加 | `1` |
| `lifecycle_diddetectcrash` | 以前の休止イベントが欠落しているためクラッシュが推測された場合にのみ存在 | `"true"` |
| `lifecycle_firstlaunchdate` | 最初に検出された起動のGMTタイムスタンプ、ISO 8601形式 | `"2013-07-11T17:55:04Z"` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | 最初に検出された起動のGMTタイムスタンプ、MM/DD/YYYY形式でフォーマット | `"01/17/2012"` |
| `lifecycle_hourofday_local` | コールが行われた地元の時間（24時間形式） | `"12"` |
| `lifecycle_isfirstlaunch` | 最初の起動コールにのみ存在 | `"true"` |
| `lifecycle_isfirstlaunchupdate` | 検出されたアプリバージョン更新後の最初の起動にのみ存在 | `"true"` |
| `lifecycle_isfirstwakemonth` | 月の最初の起動または起床にのみ存在 | `"true"` |
| `lifecycle_isfirstwaketoday` | 日の最初の起動または起床にのみ存在 | `"true"` |
| `lifecycle_launchcount` | 現在のアプリバージョンの起動回数（更新時にリセット） | `3` |
| `lifecycle_secondsawake` | 最後の起床または起動からの起床秒数。`sleep`イベントと共に送信されます。 | `30` |
| `lifecycle_priorsecondsawake` | 現在の起動前にアプリが起床していた秒数、以前の起床で集計。`launch`イベントと共に送信されます。 | `126` |
| `lifecycle_sleepcount` | 現在のアプリバージョンの休止回数（更新時にリセット） | `5` |
| `lifecycle_totalcrashcount` | インストール以来の推測されたクラッシュの総数 | `21` |
| `lifecycle_totallaunchcount` | インストール以来の起動の総数 | `3` |
| `lifecycle_totalsecondsawake` | インストール以来、アプリがフォアグラウンドにあった総秒数 | `36` |
| `lifecycle_totalsleepcount` | インストール以来、アプリがバックグラウンドに移動した総回数 | `400` |
| `lifecycle_totalwakecount` | インストール以来の起動と起床の総数 | `563` |
| `lifecycle_type` | ライフサイクルイベントのタイプ | `"launch"`, `"wake"`, `"sleep"` |
| `lifecycle_updatelaunchdate` | バージョン更新後の最初の起動または起床のGMTタイムスタンプ、ISO 8601形式 | `"2014-09-08T18:10:01Z"` |
| `lifecycle_wakecount` | 現在のアプリバージョンの起動と起床の総数（更新時にリセット） | `29` |

## インストール



`build.gradle`ファイルに`prism-lifecycle`依存関係を追加します：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-lifecycle")
```


リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用して、Swift Package Manager依存関係として `TealiumPrismLifecycle` を追加します。



## 初期化

モジュールを初期化するには、`TealiumConfig`の`modules`リストに追加します。



```kotlin
val config = TealiumConfig.Builder(
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.lifecycle(),
        // その他のモジュール...
    )
).build()
```


```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                               Modules.lifecycle(),
                               // その他のモジュール...
                           ])
```



## 手動トラッキング

自分でライフサイクルイベントをトラッキングする場合は、自動ライフサイクルトラッキングを無効にして、次の方法を使用します。



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



オプションのデータオブジェクトを使用してライフサイクルイベントメソッドを呼び出します。


<blockquote>
自動ライフサイクルトラッキングが有効な場合にこれらの方法を呼び出すとエラーが発生します。
</blockquote>




```kotlin
tealium.lifecycle.launch(dataObject)
tealium.lifecycle.wake(dataObject)
tealium.lifecycle.sleep(dataObject)
```


```swift
tealium.lifecycle.launch(dataObject)
tealium.lifecycle.wake(dataObject)
tealium.lifecycle.sleep(dataObject)
```

