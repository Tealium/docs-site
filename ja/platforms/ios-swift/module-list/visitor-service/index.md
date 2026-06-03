---
title: VisitorServiceモジュール
description: 訪問サービスから更新された訪問プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/
---
## 使用方法

VisitorServiceモジュールは、Tealium Customer Data Hubの[Data Layer Enrichment]()機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを持っており、モバイルアプリケーションで訪問プロファイルを使用してユーザーエクスペリエンスを向上させたい場合に推奨されます。AudienceStreamのライセンスを持っていない場合は、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

VisitorServiceモジュールは、Swift Package Manager、CocoaPods、またはCarthageでインストールできます。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで、**File &gt; Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は「&#34;Up to next major&#34;」が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールのリストから`VisitorService`、`Core`、`Collect`または`TagManagement`を選択し、Xcodeプロジェクトのアプリターゲットの**Frameworks and Libraries**に追加します。

### CocoaPods

CocoaPodsでVisitorServiceモジュールをインストールするには、Podfileに以下のポッドを追加します：

```perl
pod &#39;tealium-swift/Core&#39;
pod &#39;tealium-swift/Collect&#39; //or &#39;tealium-swift/TagManagement&#39;
pod &#39;tealium-swift/VisitorService&#39;
```

[iOSのCocoaPodsインストールについての詳細](/ja/platforms/ios-swift/install/#cocoapods)を学びましょう。

### Carthage

CarthageでVisitorServiceモジュールをインストールするには、以下の手順に従います：

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに以下のフレームワークを追加します：

      ```perl
      TealiumVisitorService.framework
      ```
3. VisitorServiceモジュールを構成するために、プロジェクトに以下の必要なインポート文を追加します：

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

[iOSのCarthageインストールについての詳細](/ja/platforms/ios-swift/install/#carthage)を学びましょう。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに指定されていることを確認してください。

`config.collectors = [Collectors.VisitorService]`

## 訪問データオブジェクト

訪問プロファイルは、各属性に対してフレンドリーな名前が含まれているオブジェクトです。`currentVisit`プロパティを使用して、訪問/訪問属性タイプを区別できます。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合は`nil`が返されます。以下のリストで例を参照してください。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `arraysOfBooleans` | id: String, value: [Bool]                                                                                        | `id: &#34;5129&#34;, value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: [Double]                                                                                      | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: [String]                                                                                      | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: &#34;tealiummobile\_demo\_103&#34;, value: &#34;iOS Users&#34;`                                                                              |
| `badges`           | id: String, value: Bool                                                                                          | `id: &#34;2815&#34;, value: true`                                                                                                         |
| `booleans`         | id: String, value: Bool                                                                                          | `id: &#34;4868&#34;, value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の訪問プロファイル。現在の訪問プロファイルにはAudiencesやBadgesが含まれていません。 | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `dates`            | id: String, value: Int                                                                                           | `id: &#34;22&#34;, value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Double                                                                                        | `id: &#34;5728&#34;, value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set&lt;String&gt;                                                                                   | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                                                                               |
| `tallies`          | id: String, value: [String:Double]                                                                               | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Double                                                                                        | `[&#34;category 1&#34;: 2.0]`                                                                                                             |

AudienceやBadgeが割り当てられていない場合、`nil`が返されます。
#### `arraysOfBooleans`

| 使用法                                     | 説明                                                | タイプ               | 例                                       |
| ----------------------------------------- | -------------------------------------------------- | ------------------ | --------------------------------------- |
| `visitorProfile.arraysOfBooleans`         | 訪問プロファイルのブール値の配列をすべて返します。 | `[String: [Bool]]` | `[&#34;2333&#34;: [true,false], &#34;1123&#34;: [true,true]]` |
| `visitorProfile.arraysOfBooleans[&#34;2815&#34;]` | IDによってブール値の配列を返します。               | `[Bool]`           | `[true,true]`                           |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ブール値の配列を返す
    if let arraysOfBooleans = visitorProfile.arraysOfBooleans?[&#34;5279&#34;] {
        let numberOfPositiveBools = arraysOfBooleans.filter { $0 == true }.count
        print(numberOfPositiveBools)
    }
}
```

#### `arraysOfNumbers`  

| 使用法                                    | 説明                                               | タイプ                 | 例                                        |
| ---------------------------------------- | ------------------------------------------------- | -------------------- | ------------------------------------------ |
| `visitorProfile.arraysOfNumbers`         | 訪問プロファイルの数値の配列をすべて返します。 | `[String: [Double]]` | `[&#34;2333&#34;: [2.0, 1.0], &#34;1123&#34;: [4.82125, 3.0]]` |
| `visitorProfile.arraysOfNumbers[&#34;2815&#34;]` | IDによって数値の配列を返します。                   | `[Double]`           | `[4.82125, 3.0]`                           |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 数値の配列を返す
    if let arraysOfNumbers = visitorProfile.arraysOfNumbers?[&#34;5279&#34;] {
        arraysOfNumbers.forEach { number in
    		if number &gt; 3.0 {
    			// ... アクションを取る
    		}
        }
    }
}
```

#### `arraysOfStrings`  

| 使用法                                    | 説明                                               | タイプ                 | 例                                                                     |
| ---------------------------------------- | ------------------------------------------------- | -------------------- | ----------------------------------------------------------------------- |
| `visitorProfile.arraysOfStrings`         | 訪問プロファイルの文字列の配列をすべて返します。 | `[String: [String]]` | `[&#34;1033&#34;: [&#34;Foundation&#34;, &#34;Perfume&#34;], &#34;3390&#34;: [&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;]]` |
| `visitorProfile.arraysOfStrings[&#34;3390&#34;]` | IDによって文字列の配列を返します。                   | `[String]`           | `[&#34;Bootleg Jeans&#34;, &#34;Dresses&#34;]`                                          |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列の配列を返す
    if let arraysOfStrings = visitorProfile.arraysOfStrings?[&#34;3390&#34;] {
        arraysOfStrings.forEach { string in
    		if string.lowercased().contains(&#34;Jeans&#34;) {
    			// ... アクションを取る
    		}
        }
    }
}
```
#### `audiences`

| 使用法                             | 説明                                                                                                       | タイプ               | 例                                                                                     |
| --------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------ | --------------------------------------------------------------------------------------- |
| `visitorProfile.audiences`        | 訪問がメンバーであるすべてのオーディエンスを返します。                                                          | `[String: String]` | `[&#34;tealiummobile\_demo\_103&#34;: &#34;iOS Users&#34;, &#34;tealiummobile\_demo\_110&#34;: &#34;Visitors - Known&#34;]` |
| `visitorProfile.audiences[&#34;103&#34;]` | 渡されたIDに基づいて、訪問がオーディエンスのメンバーであるかどうかをtrue/falseで返します。 | `Bool`             | `true`                                                                                      |

オーディエンスが割り当てられていない場合は、`nil`が返されます。

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ユーザーに割り当てられた現在のオーディエンスを返す
    if let audiences = visitorProfile.audiences {
        print(&#34;Visitor audiences: \(audiences)&#34;)

        // IDによってユーザーにオーディエンスが割り当てられているかを確認する
        if audiences[&#34;account_profile_106&#34;] != nil {
            print(&#34;Visitor is a member of audience id 106&#34;)
            // ... 訪問はこのオーディエンスのメンバーです、適切なアクションを取る
        }

    }
}
```

#### `badges`  

| 使用法                           | 説明                                                                       | タイプ             | 例                        |
| ------------------------------- | ------------------------------------------------------------------------- | ---------------- | -------------------------- |
| `visitorProfile.badges`         | 訪問プロファイルのすべてのバッジを返します。                                        | `[String: Bool]` | `[&#34;2815&#34;: true, &#34;2813&#34;: true]` |
| `visitorProfile.badges[&#34;2815&#34;]` | 訪問にバッジが割り当てられているかどうかをtrue/falseで返します。 | `Bool`           | `true`                     |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // バッジの値を返す
    if let badgeAssigned = visitorProfile.badges?[&#34;5279&#34;] {
        print(badgeAssigned ? &#34;Badge id 5279 is assigned&#34; : &#34;Badge id 5945 is not assigned&#34;)
    }
}
```

バッジが割り当てられていない場合は、`nil`が返されます。

#### `booleans`

| 使用法                             | 説明                                      | タイプ             | 例                         |
| --------------------------------- | ---------------------------------------- | ---------------- | --------------------------- |
| `visitorProfile.booleans`         | 訪問プロファイルのすべてのブール値を返します。 | `[String: Bool]` | `[&#34;5784&#34;: true, &#34;1453&#34;: false]` |
| `visitorProfile.booleans[&#34;4692&#34;]` | IDによってブール値を返します。           | `Bool`           | `true`                      |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ブール値を返す
    if let booleanValue = visitorProfile.booleans?[&#34;4479&#34;] {
        if booleanValue {
        	// ... 何かをする
        }
    }
}
```
#### `currentVisit`
訪問のライフタイム属性ではなく、現在の訪問の属性にアクセスします。

| 使用法                             | 説明                                                                                                                                                                                      | タイプ                         | 例                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.currentVisit`     | 現在の訪問の属性を返します。                                                                                                                                                     | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `visitorProfile.currentVisit.###` | ###に応じて属性を返します。上記のすべてのメソッドが適用されますが、オーディエンスとバッジは除外されます。これらは訪問の属性であり、訪問には適用されません。 | 変動                         | 変動                                                                                                                            |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 現在の訪問の文字列属性を返す
    if let currentVisit = visitorProfile.currentVisit,
       let string = currentVisit.strings?[&#34;34&#34;] {
        print(string)
        // ... アクションを取る
    }
}
```

#### `dates`

| 使用法                          | 説明                                   | タイプ            | 例                                      |
| ------------------------------ | --------------------------------------------- | --------------- | -------------------------------------------- |
| `visitorProfile.dates`         | 訪問プロファイルのすべての日付を返します。 | `[String: Int]` | `[&#34;25&#34;: 1567120112000, &#34;13&#34;: 1567120145666]` |
| `visitorProfile.dates[&#34;4692&#34;]` | IDによる日付を返します。                       | `Int`           | `1567120112000`                              |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 日付値を返す
    if let date = visitorProfile.dates?[&#34;33&#34;] {
        print(date)
        // .. アクションを取る
    }
}
```

#### `numbers`

| 使用法                            | 説明                                     | タイプ               | 例                                   |
| -------------------------------- | ----------------------------------------------- | ------------------ | ----------------------------------------- |
| `visitorProfile.numbers`         | 訪問プロファイルのすべての数値を返します。 | `[String: Double]` | `[&#34;83&#34;: 0.5714285714285714, &#34;1399&#34;: 2.0]` |
| `visitorProfile.numbers[&#34;1399&#34;]` | IDによる数値を返します。                       | `Double`           | `4.82125`                                 |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 数値を返す
    if let number = visitorProfile.numbers?[&#34;1399&#34;] {
        if number &gt; 3.0 {
        	// ... アクションを取る
        }
    }
}
```

#### `setsOfStrings`

| 使用法                                  | 説明                                             | タイプ                    | 例                                                              |
| -------------------------------------- | ------------------------------------------------------- | ----------------------- | -------------------------------------------------------------------- |
| `visitorProfile.setsOfStrings`         | 訪問プロファイルのすべての文字列セットを返します。 | `[String: Set&lt;String&gt;]` | `[&#34;9938&#34;: [&#34;shirts&#34;], &#34;2300&#34;: [&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;]]` |
| `visitorProfile.setsOfStrings[&#34;2300&#34;]` | IDによる文字列セットを返します。                       | `Set&lt;String&gt;`           | `[&#34;Luxury Couch 1&#34;, &#34;Luxury Couch 2&#34;]`                               |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列セットの値を返す
    if let setOfStrings = visitorProfile.setsOfStrings?[&#34;5279&#34;] {
        if setOfStrings.contains(&#34;toys&#34;) {
        	// ... アクションを取る
        }
    }
}
```

#### `strings`

| 使用法                            | 説明                                     | タイプ     | 例                                     |
| -------------------------------- | ----------------------------------------------- | -------- | ------------------------------------------- |
| `visitorProfile.strings`         | 訪問プロファイルのすべての文字列を返します。 | `String` | `&#34;83&#34;: &#34;Toy Truck&#34;, &#34;5699&#34;: &#34;Toy Tea Set&#34;]` |
| `visitorProfile.strings[&#34;5699&#34;]` | IDによる文字列を返します。                       | `String` | `&#34;Toy Tea Set&#34;`                             |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列値を返す
    if let string = visitorProfile.strings?[&#34;5699&#34;] {
        print(string)
        // ... アクションを取る
    }
}
```

#### `tallies`

| 使用法                                      | 説明                                     | タイプ                         | 例                                                                                                        |
| ------------------------------------------ | ----------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.tallies`                   | 訪問プロファイルのすべての集計を返します。 | `[String: [String: Double]]` | `[&#34;2983&#34;: [&#34;red shirts category&#34;: 4.0, &#34;green shirts category&#34;: 2.0], &#34;5643&#34;: [&#34;girls&#34;: 3.0, &#34;womens&#34;: 1.0]]`] |
| `visitorProfile.tallies[&#34;1399&#34;]`           | IDによる集計を返します。                        | `[String: Double]`           | `[&#34;girls&#34;: 3.0, &#34;womens&#34;: 1.0]`                                                                                |
| `visitorProfile.tallies[&#34;1399&#34;][&#34;womens&#34;]` | IDによる集計値を返します。                        | `Double`                     | `3.0`                                                                                                          |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 全体の集計を返す
    if let tally = visitorProfile.tallies?[&#34;1399&#34;] {
        print(&#34;Tally id 5377: \(tally)&#34;)
    }

    // 集計IDと値のキーを使用して集計値を返す
    if let tally = visitorProfile.tallies?[&#34;5381&#34;], let tallyValue = tally[&#34;red shirts&#34;] {
        print(&#34;Tally value for id 5381 and key &#39;red shirts&#39;: \(tallyValue)&#34;)
    }
}
```

## API リファレンス

### クラス `Tealium`

VisitorServiceモジュールの一般的に使用されるメソッドとプロパティを以下にまとめます。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`cachedProfile`](#cachedprofile) | 新しいリクエストをトリガーせずに、永続保存から最近取得した訪問プロファイルを返します|
| [`requestVisitorProfile()`](#requestvisitorprofile) | VisitorServiceに現在の訪問プロファイルを即時に取得するリクエストをトリガーします |
| [`visitorService`](#visitorservice)  | VisitorServiceモジュールのプロパティ |
#### `cachedProfile`

最後に取得した訪問プロファイルを永続的な保存から取得し、新しいリクエストをトリガーせずに返します。インターネット接続がない状況で以前に成功したリクエストがあった場合に便利です。

使用例：

```swift
let profile = self.tealium?.visitorService?.cachedProfile
guard let json = try? JSONEncoder().encode(profile),
    let cachedProfileString = String(data: json, encoding: .utf8) else {
        return
}
print(cachedProfileString)
```

#### `requestVisitorProfile()`

VisitorServiceに即時リクエストをトリガーして、現在の訪問プロファイルを取得します。プロファイルが最後のフェッチ以降に更新されている場合、[`didUpdate()`](#didupdate) デリゲートメソッドが呼び出されます。

このメソッドは、訪問プロファイルの更新間隔が `0` に構成されている場合、トラックリクエストが送信されるたびに自動的に呼び出されます。更新間隔に高い値を構成している場合は、次のスケジュールされた更新を待たずにこのメソッドを呼び出してプロファイルを即座に取得することができます。

```swift
self.tealium?.visitorService?.requestVisitorProfile()
```

使用例：

```swift
func track(title: String, data: [String: Any]?) {
   let tealEvent = TealiumEvent(title, dataLayer: data)
   tealium?.track(tealEvent)
   tealium?.visitorService?.requestVisitorProfile()
}
```

#### `visitorService`

VisitorServiceモジュール。

```swift
self.tealium?.visitorService?.####
```
`####`は`visitorService`オブジェクトの任意の公開APIメソッドです。以下は完全な使用例です：

```swift
class MyHelperClass {
    var tealium: Tealium?

    public init () {
        let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
            profile: &#34;PROFILE&#34;,
            environment: &#34;ENVIRONMENT&#34;,
            datasource: &#34;DATASOURCE&#34;,
            optionalData: nil)

        config.visitorServiceDelegate = self
        config.visitorServiceRefresh = .every(10, .minutes)

        self.tealium = Tealium(config) {
            // 注意: これは初期化後の完了ブロック内です

            // self.tealiumは完了ブロック内で初期化されていることが保証されています
            self.tealium?.visitorService?.####
        }
    }
}
```

### クラス: `VisitorServiceDelegate`

VisitorServiceモジュールの一般的に使用されるメソッドとプロパティを以下にまとめます。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`didUpdate()`](#didupdate)  | プロファイルが更新されたとき、または`requestVisitorProfile()`メソッドが呼び出されたときに更新された訪問プロファイルを返すコールバックメソッドです。 |

#### `didUpdate()`

プロファイルが更新されたとき、または`requestVisitorProfile()`メソッドが呼び出されたときに更新された訪問プロファイルを返すコールバックメソッドです。これは構成された更新間隔に依存しますが、デフォルトは5分です。

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // プロファイル属性に基づいて行動します
    print(visitorProfile.audiences)
    //...
}
```

| パラメータ   | 説明 | 例                           |
| ------      | ----------- | --------------------------------- |
| `TealiumVisitorProfile` | Tealium訪問プロファイル | `visitorProfile` |


### クラス: `TealiumConfig`

VisitorServiceモジュールの一般的に使用されるメソッドとプロパティを以下にまとめます。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`visitorServiceDelegate`](#visitorservicedelegate) | `didUpdate`デリゲートメソッドを使用するためのデリゲートを構成します |
| [`visitorServiceOverrideProfile`](#visitorserviceoverrideprofile) | 訪問プロファイルを取得するためのプロファイルを上書きします |
| [`visitorServiceOverrideURL`](#visitorserviceoverrideurl) | 訪問プロファイルを取得するための基本URLを上書きします |
| [`visitorServiceRefresh`](#visitorservicerefresh) | 訪問プロファイルの取得頻度を構成します |


#### `visitorServiceDelegate`

[`didUpdate`](#didupdate) デリゲートメソッドを使用するためのデリゲートを構成します。  

```swift
config.visitorServiceDelegate = self
```

| タイプ   | 説明 | 例                           |
| ------ | ----------- | --------------------------------- |
| `Class` | プロファイル更新を担当するクラス（デリゲート） | `AnalyticsManager`, `TealiumHelper` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium VisitorServiceモジュールの構成メソッド
      config.visitorServiceDelegate = self
  }
```

```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        if let json = try? JSONEncoder().encode(visitorProfile),
           let string = String(data: json, encoding: .utf8) {
            print(string)
        }
    }
}
```

#### `visitorServiceOverrideProfile`

訪問プロファイルを取得するためのプロファイルを上書きします。Collectモジュールで使用されるプロファイルと一致させます。


```swift
config.visitorServiceOverrideProfile = &#34;PROFILE&#34;
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルを取得するためのAudience Streamプロファイルを構成します | `&#34;main&#34;` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium Visitor Serviceモジュールの構成メソッド
      config.visitorServiceOverrideProfile = &#34;main&#34;
  }
```

#### `visitorServiceOverrideURL`

訪問プロファイルを取得するための基本URLを上書きします。ACCOUNT、PROFILE、および訪問IDは自動的にURLに追加されます。


```swift
config.visitorServiceOverrideURL = &#34;https://overridden-subdomain.yourdomain.com/&#34;
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルを取得するためのURLを構成します | `&#34;https://overridden-subdomain.yourdomain.com/&#34;` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium Visitor Serviceモジュールの構成メソッド
      config.visitorServiceOverrideURL = &#34;https://overridden-subdomain.yourdomain.com/&#34;
  }
```

#### `visitorServiceRefresh`

訪問プロファイルの取得頻度を調整するためのプロパティです。デフォルト値は5分です。`requestVisitorProfile()`メソッドをすべてのトラッキングコールに追加しても、この値を0に構成しない限り、プロファイルは毎回取得されません。

```swift
let config = TealiumConfig(...)
config.visitorServiceRefresh = .every(3, .seconds)
```

`RefreshInterval` オプション: `seconds`, `minutes`, `hours`

| パラメータ | 説明                                                                            | 例 |
| ---------- | -------------------------------------------------------------------------------------- | ------- |
|`.every(Int, RefreshInterval)`   | 訪問プロファイルを取得する頻度。  (デフォルト: `.every(5, .minutes)`) | `.every(15, .seconds)`     |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                                 profile: &#34;NAME&#34;,
                                 environment: &#34;ENVIRONMENT&#34;,
                                 datasource: &#34;DATASOURCE&#34;,
                                 optionalData: nil)
      // Tealium Visitor Serviceモジュールの構成メソッド
      config.visitorServiceRefresh = .every(3, .seconds)
  }
```
## リリースノート

2.0.0

**大きな変更点**

 * TealiumVisitorProfileのパフォーマンスを向上
 * シンプルさのためにマルチキャストデリゲート機能を削除
 * キャッシュされたプロファイルメソッドから完了を削除

**小さな変更点**

* 更新間隔のオプションを追加
* クラス名を一貫性のあるものに更新
* デリゲートメソッドのシグネチャを更新
* テストの改善

1.8.0

* 初回リリース