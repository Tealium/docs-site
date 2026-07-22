---
title: ライフサイクルモジュール
description: アプリのライフサイクルイベントと関連データを自動的に追跡します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/lifecycle/
---## 使用法

ライフサイクルモジュールは、アプリのライフサイクルイベントと関連データを自動的に追跡します。ライブラリが初めてロードされたときに起動イベントがトリガーされ、`UIApplicationWillResignActive`通知でスリープイベントが、`UIApplicationDidBecomeActive`でウェイクイベントがトリガーされます。

このモジュールの使用は、Adobe Analyticsを使用している場合に推奨されます。それ以外の場合でも、オプションですが、追加でキャプチャされるイベント（起動/ウェイク/スリープ）が他のベンダーの実装に役立つかもしれません。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## 要件

`UIKit`の依存関係がターゲットアプリに追加されている場合、それ以上の構成や実装は必要ありません。その他のプラットフォームビルド（watchOS、macOS）では、ライフサイクルモジュールの機能を手動でトリガーすることができます（[API Reference](https://docs.tealium.com/ja/platforms/ios-swift/module-list/lifecycle/#api-reference)を参照）。

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してライフサイクルモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0+でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールする最も簡単で推奨される方法です：

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`"Up to next major"`が推奨されます。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`Lifecycle`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットに追加します。**Frameworks and Libraries**の下にあります。

[iOS用のSwift Package Managerのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)について詳しくはこちらをご覧ください。

### CocoaPods

CocoaPodsでライフサイクルモジュールをインストールするには、以下のpodをPodfileに追加します：  
```perl
pod 'tealium-swift/Lifecycle'
```

[iOS用のCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)について詳しくはこちらをご覧ください。

### Carthage

Carthageでライフサイクルモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```perl
      TealiumLifecycle.framework
      ```
3. ライフサイクルライブラリをインポートするには、プロジェクトに次のインポート文を追加します：   
      ```swift
      import TealiumLifecycle
      ```

[iOS用のCarthageのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)について詳しくはこちらをご覧ください。

## 構成

ライフサイクルモジュールをインスタンス化するには、SDKを初期化するときに`TealiumConfig`オブジェクトで指定する必要があります：

```swift
import TealiumCore
import TealiumInAppPurchase

let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           datasource: "DATASOURCE")

config.collectors = [Collectors.Lifecycle]
tealium = Tealium(config: config) { _ in }
```


<blockquote>
必要なコレクターを正しく指定する方法については、[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを参照してください。
</blockquote>


## データレイヤー
モジュールが有効な間、次の変数が各トラッキング呼び出しで送信されます：

| 変数名                     | タイプ | 説明                                                                        | 例              |
|------------------------------------|-----------------------------------------------------------------------------------|---------|----------------------|
| `lifecycle_diddetect_crash`        | `Boolean` | この起動/ウェイクイベント中にクラッシュが検出されたかどうか。真の場合のみ記入されます。       | [`"true"`, `"false"`]                 |
| `lifecycle_dayofweek_local`        | `Number`  |呼び出しが行われたローカルの曜日、例えば1=日曜日、2=月曜日。                   | `13`                   |
| `lifecycle_dayssincelaunch`        | `Number`  |初回起動からの日数（整数）。                                      | `23`                   |
| `lifecycle_dayssinceupdate`        | `Number`  |最後に検出されたアプリバージョンの更新からの日数（整数）。              | `46`                   |
| `lifecycle_dayssincelastwake`      | `Number`  | 最後に検出されたウェイクからの日数（整数）。                               | `1`                    |
| `lifecycle_firstlaunchdate`        | `String` | 最初に検出された起動/ウェイクのGMTタイムスタンプ。UTC時間からのISO 8601形式。   | `"2013-07-11T17:55:04Z"` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | `String` |GMTタイムスタンプをMM/DD/YYYY形式でフォーマットしたもの。                                             | `"01/18/2012" `          |
| `lifecycle_hourofday_local`        | `String` |呼び出しが行われたローカルの時間（24時間形式）。                               | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunch`          | `String` |呼び出しが最初の起動/ウェイク呼び出しである場合のみ存在します。                                  | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunchupdate` | `Boolean` |呼び出しが検出された更新後の最初の起動/ウェイクである場合のみ存在します。                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwakemonth`    | `Boolean` |呼び出しが月の最初の起動/ウェイクである場合のみ存在します。                                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwaketoday`    | `Boolean` | 呼び出しがその日の最初の起動/ウェイクである場合のみ存在します。                       | [`"true"`, `"false"`] |
| `lifecycle_launchcount`         | `Number`  |あなたのアプリのこのバージョンの起動回数（最後の更新以降）。                                       | `3`    |
| `lifecycle_priorsecondsawake`   | `Number`  |アプリが最後の起動以降に起きていた全秒数。以前のすべてのウェイクからの合計。`lifecycle_type:launch`呼び出しのみで送信されます。  | `126`  |
| `lifecycle_secondsawake`        | `Number`  |最近のウェイク/起動以降、アプリが起きていた全秒数。                                                                             | `30`   |
| `lifecycle_sleepcount`          | `Number`  |あなたのアプリがスリープに入った回数の合計（更新されるとリセットされます）。                                                                    | `5`    |
| `lifecycle_totalcrashcount`     | `Number`  |インストール以降にカウントされたクラッシュの合計数（アプリが削除されるとのみリセットされます）。                                                             | `21`   |
| `lifecycle_totallaunchcount`    | `Number`  |インストール以降の起動回数の合計（アプリが削除されるとのみリセットされます）。                                             | `3`     |
| `lifecycle_totalsecondsawake`   | `Number`  |アプリがインストール以降に起きて/アクティブ状態になっていた秒数の合計（アプリが削除されるとのみリセットされます）。 | `36`    |
| `lifecycle_totalsleepcount`     | `Number`  |アプリがインストール以降にバックグラウンドに入った回数の合計（アプリが削除されるとのみリセットされます）。    | `400` |
| `lifecycle_totalwakecount`      | `Number`  |インストール以降の起動+ウェイクの合計数（アプリが削除されるとのみリセットされます）。 |  `"563"` |
| `lifecycle_updatelaunchdate`    | `String`  |バージョン更新が検出された後の最初のウェイク/起動のGMTタイムスタンプ。     |  `"2014-09-08T18:10:01Z"` |
| `lifecycle_type`                | `String`  |ライフサイクル呼び出しのタイプ。 | [`"launch"`, `"wake"`, `"sleep"` ]                |
| `lifecycle_wakecount`           | `Number`  |あなたのアプリのこのバージョンの起動+ウェイクの合計数（更新されるとリセットされます）。  | `"29"`                 |

## クラッシュ検出

ライフサイクルモジュールは基本的なクラッシュ検出を行いますが、クラッシュの原因についての詳細は収集しません。スリープイベントが先行せずにライフサイクル起動イベントが見られるたびにクラッシュを記録します。
通常、アプリがユーザーによって閉じられると、OSからの通知がライフサイクルのスリープイベントをトリガーしますが、アプリがクラッシュすると、これが発生する時間がなく、したがって、スリープイベントは発生しません。クラッシュ後の次回の起動時に、`lifecycle_diddetectcrash`変数が`true`に構成され、`lifecycle_totalcrashcount`変数が1増加します。

より高度なクラッシュ検出が必要な場合、クラッシュレポーターモジュールは各クラッシュの詳細とクラッシュの理由を提供します。これは現在、iOSのみでサポートされています。

## API リファレンス

以下のAPIメソッドは、`UIKit`をサポートしていないプラットフォームを対象としている場合にのみ使用する必要があります。

### `launchDetected()`
ライフサイクルのレコードを起動イベントで更新し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledAtLaunchTime {
    tealium?.lifecycle?.launchDetected()

}
```

### `wakeDetected()`
ライフサイクルのレコードをウェイクイベントで更新し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledWhenAppStarts {
    tealium?.lifecycle?.wakeDetected()

}
```

<blockquote>
`wakeDetected()`の呼び出しは、同じ関数内の`launchDetected()`の後に安全に追加されます。モジュールは、インスタンス化されたインスタンスごとに単一の起動イベントのみを受け入れます。
</blockquote>



### `sleepDetected()`
ライフサイクルのレコードをスリープイベントで更新し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledBeforeAppTerminated {
    tealium?.lifecycle?.sleepDetected()
}
```

### `dictionary`

ライフサイクルデータを`[String: Any]`の辞書として読み取り専用でアクセスできるプロパティ。

```
// ライフサイクルデータ辞書から合計ウェイクカウントを取得
let wakeCount = tealium?.lifecycle?.dictionary?["lifecycle_totalwakecount"]
```