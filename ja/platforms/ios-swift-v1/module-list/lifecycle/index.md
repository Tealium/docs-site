---
title: ライフサイクルモジュール
description: アプリのライフサイクルイベントと関連データを自動的に追跡します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/lifecycle/
---## 使用法

ライフサイクルモジュールは、アプリのライフサイクルイベントと関連データを自動的に追跡します。ライブラリが初めてロードされたときに起動イベントがトリガーされ、`UIApplicationWillResignActive`通知でスリープイベントが、`UIApplicationDidBecomeActive`でウェイクイベントがトリガーされます。

このモジュールの使用は、Adobe Analyticsを使用している場合に推奨されます。それ以外の場合でも、オプションですが、追加でキャプチャされるイベント（起動/ウェイク/スリープ）が他のベンダーの実装に役立つかもしれません。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## 要件

ターゲットアプリに`UIKit`の依存関係が追加されている場合、それ以上の構成や実装は必要ありません。他のプラットフォームのビルド（watchOS、macOS）では、ライフサイクルモジュールの関数を手動でトリガーすることができます（[APIリファレンス](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/lifecycle/#api-reference)を参照）。

## インストール

CocoaPodsまたはCarthageでライフサイクルモジュールをインストールします。

### CocoaPods

CocoaPodsでライフサイクルモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod 'tealium-swift/TealiumLifecycle'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。iOSのCocoaPodsインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)を参照してください。


### Carthage

Carthageでライフサイクルモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumLifecycle.framework
      ```
3. ライフサイクルライブラリをインポートするには、プロジェクトに次のインポート文を追加します：   
      ```swift
      import TealiumLifecycle
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポート文は必要ありません。iOSのCarthageインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)を参照してください。

## データレイヤー
モジュールが有効な間、次の変数が各トラッキング呼び出しで送信されます：

| 変数名  | 型 | 説明  | 例 |
|------------------------------------|-----------------------------------------------------------------------------------|---------|----------------------|
| `lifecycle_diddetect_crash`        | `Boolean` | この起動/ウェイクイベント中にクラッシュが検出されたかどうか。真の場合のみ記入されます。       | [`"true"`, `"false"`]                 |
| `lifecycle_dayofweek_local`        | `Number`  |呼び出しが行われた地元の曜日、例えば1=日曜日、2=月曜日。                   | `13`                   |
| `lifecycle_dayssincelaunch`        | `Number`  |初回起動からの日数（整数）。                                      | `23`                   |
| `lifecycle_dayssinceupdate`        | `Number`  |最後に検出されたアプリバージョンの更新からの日数（整数）。              | `46`                   |
| `lifecycle_dayssincelastwake`      | `Number`  | 最後に検出されたウェイクからの日数（整数）。                               | `1`                    |
| `lifecycle_firstlaunchdate`        | `String` | 最初に検出された起動/ウェイクのGMTタイムスタンプ（UTCからのISO 8601形式）。   | `"2013-07-11T17:55:04Z"` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | `String` |GMTタイムスタンプをMM/DD/YYYY形式でフォーマットしたもの。                                             | `"01/18/2012" `          |
| `lifecycle_hourofday_local`        | `String` |呼び出しが行われた地元の時間（24時間形式）。                               | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunch`          | `String` |呼び出しが最初の起動/ウェイク呼び出しである場合のみ存在します。                                  | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunchupdate` | `Boolean` |呼び出しが検出された更新後の最初の起動/ウェイクである場合のみ存在します。                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwakemonth`    | `Boolean` |呼び出しが月の最初の起動/ウェイクである場合のみ存在します。                                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwaketoday`    | `Boolean` | 呼び出しがその日の最初の起動/ウェイクである場合のみ存在します。                       | [`"true"`, `"false"`] |
| `lifecycle_launchcount`         | `Number`  |あなたのアプリのこのバージョンの起動回数（最後の更新以降）。                                       | `3`    |
| `lifecycle_priorsecondsawake`   | `Number`  |最後の起動以降、アプリが起動していた全秒数。以前のすべてのウェイクからの合計。`lifecycle_type:launch`呼び出しのみで送信されます。  | `126`  |
| `lifecycle_secondsawake`        | `Number`  |最近のウェイク/起動以降、アプリが起動していた全秒数。                                                                             | `30`   |
| `lifecycle_sleepcount`          | `Number`  |あなたのアプリがスリープに入った回数の合計（更新されるとリセットされます）。                                                                    | `5`    |
| `lifecycle_totalcrashcount`     | `Number`  |インストール以降にカウントされたクラッシュの合計数（アプリが削除されるとのみリセットされます）。                                                             | `21`   |
| `lifecycle_totallaunchcount`    | `Number`  |インストール以降の起動回数の合計（アプリが削除されるとのみリセットされます）                                             | `3`     |
| `lifecycle_totalsecondsawake`   | `Number`  |アプリがインストールされて以降、アプリが起動/アクティブ状態にあった秒数の合計（アプリが削除されるとのみリセットされます）。 | `36`    |
| `lifecycle_totalsleepcount`     | `Number`  |アプリがバックグラウンドに入った回数の合計（アプリが削除されるとのみリセットされます）。    | `400` |
| `lifecycle_totalwakecount`      | `Number`  |インストール以降の起動+ウェイクの合計数（アプリが削除されるとのみリセットされます）。 |  `"563"` |
| `lifecycle_updatelaunchdate`    | `String`  |バージョン更新が検出された後の最初のウェイク/起動のGMTタイムスタンプ。     |  `"2014-09-08T18:10:01Z"` |
| `lifecycle_type`                | `String`  |ライフサイクル呼び出しのタイプ。 | [`"launch"`, `"wake"`, `"sleep"` ]                |
| `lifecycle_wakecount`           | `Number`  |あなたのアプリのこのバージョンの起動+ウェイクの合計数（更新されるとリセットされます）。  | `"29"`                 |

## クラッシュ検出

ライフサイクルモジュールは基本的なクラッシュ検出を行いますが、クラッシュの原因についての詳細は収集しません。スリープイベントが先行せずにライフサイクルの起動イベントが見られるたびに、クラッシュを記録します。

通常、アプリがユーザーによって閉じられると、OSからの通知がライフサイクルのスリープイベントをトリガーしますが、アプリがクラッシュすると、これが発生する時間がありません。したがって、スリープイベントは発生しません。クラッシュ後の次の起動時に、`lifecycle_diddetectcrash`変数が`true`に構成され、`lifecycle_totalcrashcount`変数が1増加します。

より高度なクラッシュ検出が必要な場合、Crash Reporterモジュールは各クラッシュの詳細とクラッシュの理由を提供します。これは現在、iOSのみでサポートされています。

## APIリファレンス
`UIKit`をサポートしていないプラットフォームを対象としている場合のみ、これらのAPIメソッドを使用する必要があります。

### `launchDetected()`
起動イベントでライフサイクルレコードを更新し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledAtLaunchTime {
    tealium?.lifecycle()?.launchDetected()

}
```

### `wakeDetected()`
ウェイクイベントでライフサイクルレコードを更新し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledWhenAppStarts {
    tealium?.lifecycle()?.wakeDetected()

}
```

<blockquote>
`wakeDetected()`の呼び出しは、同じ関数内で`launchDetected()`の後に安全に追加できます。モジュールは、インスタンス化されたインスタンスごとに単一の起動イベントのみを受け入れます。
</blockquote>



### `sleepDetected()`
アプリ終了前に呼び出されるメソッドで、スリープイベントを記録し、ライフサイクルイベントのディスパッチをトリガーします。

```
func someMethodCalledBeforeAppTerminated {
    tealium?.lifecycle()?.sleepDetected()
}
```

### `dictionary`

ライフサイクルデータを`[String: Any]`の辞書として読み取り専用で提供するプロパティ。

```
// ライフサイクルデータ辞書からトータルウェイクカウントを取得します
let wakeCount = tealium?.lifecycle()?.dictionary?["lifecycle_totalwakecount"]
```