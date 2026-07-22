---
title: VisitorServiceモジュール
description: 訪問サービスから更新された訪問プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/
---
## 使用方法

VisitorServiceモジュールは、Tealium Customer Data Hubの[Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/)機能を実装しています。

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

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は「"Up to next major"」が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールのリストから`VisitorService`、`Core`、`Collect`または`TagManagement`を選択し、Xcodeプロジェクトのアプリターゲットの**Frameworks and Libraries**に追加します。

### CocoaPods

CocoaPodsでVisitorServiceモジュールをインストールするには、Podfileに以下のポッドを追加します：

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' //or 'tealium-swift/TagManagement'
pod 'tealium-swift/VisitorService'
```

[iOSのCocoaPodsインストールについての詳細](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を学びましょう。

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

[iOSのCarthageインストールについての詳細](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を学びましょう。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに指定されていることを確認してください。

`config.collectors = [Collectors.VisitorService]`

## 訪問データオブジェクト

訪問プロファイルは、各属性に対してフレンドリーな名前が含まれているオブジェクトです。`currentVisit`プロパティを使用して、訪問/訪問属性タイプを区別できます。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合は`nil`が返されます。以下のリストで例を参照してください。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `arraysOfBooleans` | id: String, value: [Bool]                                                                                        | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: [Double]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: [String]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Bool                                                                                          | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Bool                                                                                          | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の訪問プロファイル。現在の訪問プロファイルにはAudiencesやBadgesが含まれていません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Int                                                                                           | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Double                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set<String>                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: [String:Double]                                                                               | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Double                                                                                        | `["category 1": 2.0]`                                                                                                             |


<blockquote>
AudienceやBadgeが割り当てられていない場合、`nil`が返されます。
</blockquote>

#### `arraysOfBooleans`

| 使用法                                     | 説明                                                | タイプ               | 例                                       |
| ----------------------------------------- | -------------------------------------------------- | ------------------ | --------------------------------------- |
| `visitorProfile.arraysOfBooleans`         | 訪問プロファイルのブール値の配列をすべて返します。 | `[String: [Bool]]` | `["2333": [true,false], "1123": [true,true]]` |
| `visitorProfile.arraysOfBooleans["2815"]` | IDによってブール値の配列を返します。               | `[Bool]`           | `[true,true]`                           |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ブール値の配列を返す
    if let arraysOfBooleans = visitorProfile.arraysOfBooleans?["5279"] {
        let numberOfPositiveBools = arraysOfBooleans.filter { $0 == true }.count
        print(numberOfPositiveBools)
    }
}
```

#### `arraysOfNumbers`  

| 使用法                                    | 説明                                               | タイプ                 | 例                                        |
| ---------------------------------------- | ------------------------------------------------- | -------------------- | ------------------------------------------ |
| `visitorProfile.arraysOfNumbers`         | 訪問プロファイルの数値の配列をすべて返します。 | `[String: [Double]]` | `["2333": [2.0, 1.0], "1123": [4.82125, 3.0]]` |
| `visitorProfile.arraysOfNumbers["2815"]` | IDによって数値の配列を返します。                   | `[Double]`           | `[4.82125, 3.0]`                           |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 数値の配列を返す
    if let arraysOfNumbers = visitorProfile.arraysOfNumbers?["5279"] {
        arraysOfNumbers.forEach { number in
    		if number > 3.0 {
    			// ... アクションを取る
    		}
        }
    }
}
```

#### `arraysOfStrings`  

| 使用法                                    | 説明                                               | タイプ                 | 例                                                                     |
| ---------------------------------------- | ------------------------------------------------- | -------------------- | ----------------------------------------------------------------------- |
| `visitorProfile.arraysOfStrings`         | 訪問プロファイルの文字列の配列をすべて返します。 | `[String: [String]]` | `["1033": ["Foundation", "Perfume"], "3390": ["Bootleg Jeans", "Dresses"]]` |
| `visitorProfile.arraysOfStrings["3390"]` | IDによって文字列の配列を返します。                   | `[String]`           | `["Bootleg Jeans", "Dresses"]`                                          |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列の配列を返す
    if let arraysOfStrings = visitorProfile.arraysOfStrings?["3390"] {
        arraysOfStrings.forEach { string in
    		if string.lowercased().contains("Jeans") {
    			// ... アクションを取る
    		}
        }
    }
}
```
#### `audiences`

| 使用法                             | 説明                                                                                                       | タイプ               | 例                                                                                     |
| --------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------ | --------------------------------------------------------------------------------------- |
| `visitorProfile.audiences`        | 訪問がメンバーであるすべてのオーディエンスを返します。                                                          | `[String: String]` | `["tealiummobile\_demo\_103": "iOS Users", "tealiummobile\_demo\_110": "Visitors - Known"]` |
| `visitorProfile.audiences["103"]` | 渡されたIDに基づいて、訪問がオーディエンスのメンバーであるかどうかをtrue/falseで返します。 | `Bool`             | `true`                                                                                      |


<blockquote>
オーディエンスが割り当てられていない場合は、`nil`が返されます。
</blockquote>


使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ユーザーに割り当てられた現在のオーディエンスを返す
    if let audiences = visitorProfile.audiences {
        print("Visitor audiences: \(audiences)")

        // IDによってユーザーにオーディエンスが割り当てられているかを確認する
        if audiences["account_profile_106"] != nil {
            print("Visitor is a member of audience id 106")
            // ... 訪問はこのオーディエンスのメンバーです、適切なアクションを取る
        }

    }
}
```

#### `badges`  

| 使用法                           | 説明                                                                       | タイプ             | 例                        |
| ------------------------------- | ------------------------------------------------------------------------- | ---------------- | -------------------------- |
| `visitorProfile.badges`         | 訪問プロファイルのすべてのバッジを返します。                                        | `[String: Bool]` | `["2815": true, "2813": true]` |
| `visitorProfile.badges["2815"]` | 訪問にバッジが割り当てられているかどうかをtrue/falseで返します。 | `Bool`           | `true`                     |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // バッジの値を返す
    if let badgeAssigned = visitorProfile.badges?["5279"] {
        print(badgeAssigned ? "Badge id 5279 is assigned" : "Badge id 5945 is not assigned")
    }
}
```


<blockquote>
バッジが割り当てられていない場合は、`nil`が返されます。
</blockquote>


#### `booleans`

| 使用法                             | 説明                                      | タイプ             | 例                         |
| --------------------------------- | ---------------------------------------- | ---------------- | --------------------------- |
| `visitorProfile.booleans`         | 訪問プロファイルのすべてのブール値を返します。 | `[String: Bool]` | `["5784": true, "1453": false]` |
| `visitorProfile.booleans["4692"]` | IDによってブール値を返します。           | `Bool`           | `true`                      |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // ブール値を返す
    if let booleanValue = visitorProfile.booleans?["4479"] {
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
| `visitorProfile.currentVisit`     | 現在の訪問の属性を返します。                                                                                                                                                     | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `visitorProfile.currentVisit.###` | ###に応じて属性を返します。上記のすべてのメソッドが適用されますが、オーディエンスとバッジは除外されます。これらは訪問の属性であり、訪問には適用されません。 | 変動                         | 変動                                                                                                                            |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 現在の訪問の文字列属性を返す
    if let currentVisit = visitorProfile.currentVisit,
       let string = currentVisit.strings?["34"] {
        print(string)
        // ... アクションを取る
    }
}
```

#### `dates`

| 使用法                          | 説明                                   | タイプ            | 例                                      |
| ------------------------------ | --------------------------------------------- | --------------- | -------------------------------------------- |
| `visitorProfile.dates`         | 訪問プロファイルのすべての日付を返します。 | `[String: Int]` | `["25": 1567120112000, "13": 1567120145666]` |
| `visitorProfile.dates["4692"]` | IDによる日付を返します。                       | `Int`           | `1567120112000`                              |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 日付値を返す
    if let date = visitorProfile.dates?["33"] {
        print(date)
        // .. アクションを取る
    }
}
```

#### `numbers`

| 使用法                            | 説明                                     | タイプ               | 例                                   |
| -------------------------------- | ----------------------------------------------- | ------------------ | ----------------------------------------- |
| `visitorProfile.numbers`         | 訪問プロファイルのすべての数値を返します。 | `[String: Double]` | `["83": 0.5714285714285714, "1399": 2.0]` |
| `visitorProfile.numbers["1399"]` | IDによる数値を返します。                       | `Double`           | `4.82125`                                 |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 数値を返す
    if let number = visitorProfile.numbers?["1399"] {
        if number > 3.0 {
        	// ... アクションを取る
        }
    }
}
```

#### `setsOfStrings`

| 使用法                                  | 説明                                             | タイプ                    | 例                                                              |
| -------------------------------------- | ------------------------------------------------------- | ----------------------- | -------------------------------------------------------------------- |
| `visitorProfile.setsOfStrings`         | 訪問プロファイルのすべての文字列セットを返します。 | `[String: Set<String>]` | `["9938": ["shirts"], "2300": ["Luxury Couch 1", "Luxury Couch 2"]]` |
| `visitorProfile.setsOfStrings["2300"]` | IDによる文字列セットを返します。                       | `Set<String>`           | `["Luxury Couch 1", "Luxury Couch 2"]`                               |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列セットの値を返す
    if let setOfStrings = visitorProfile.setsOfStrings?["5279"] {
        if setOfStrings.contains("toys") {
        	// ... アクションを取る
        }
    }
}
```

#### `strings`

| 使用法                            | 説明                                     | タイプ     | 例                                     |
| -------------------------------- | ----------------------------------------------- | -------- | ------------------------------------------- |
| `visitorProfile.strings`         | 訪問プロファイルのすべての文字列を返します。 | `String` | `"83": "Toy Truck", "5699": "Toy Tea Set"]` |
| `visitorProfile.strings["5699"]` | IDによる文字列を返します。                       | `String` | `"Toy Tea Set"`                             |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 文字列値を返す
    if let string = visitorProfile.strings?["5699"] {
        print(string)
        // ... アクションを取る
    }
}
```

#### `tallies`

| 使用法                                      | 説明                                     | タイプ                         | 例                                                                                                        |
| ------------------------------------------ | ----------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.tallies`                   | 訪問プロファイルのすべての集計を返します。 | `[String: [String: Double]]` | `["2983": ["red shirts category": 4.0, "green shirts category": 2.0], "5643": ["girls": 3.0, "womens": 1.0]]`] |
| `visitorProfile.tallies["1399"]`           | IDによる集計を返します。                        | `[String: Double]`           | `["girls": 3.0, "womens": 1.0]`                                                                                |
| `visitorProfile.tallies["1399"]["womens"]` | IDによる集計値を返します。                        | `Double`                     | `3.0`                                                                                                          |

使用例:

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // 全体の集計を返す
    if let tally = visitorProfile.tallies?["1399"] {
        print("Tally id 5377: \(tally)")
    }

    // 集計IDと値のキーを使用して集計値を返す
    if let tally = visitorProfile.tallies?["5381"], let tallyValue = tally["red shirts"] {
        print("Tally value for id 5381 and key 'red shirts': \(tallyValue)")
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
        let config = TealiumConfig(account: "ACCOUNT",
            profile: "PROFILE",
            environment: "ENVIRONMENT",
            datasource: "DATASOURCE",
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
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
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
config.visitorServiceOverrideProfile = "PROFILE"
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルを取得するためのAudience Streamプロファイルを構成します | `"main"` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Serviceモジュールの構成メソッド
      config.visitorServiceOverrideProfile = "main"
  }
```

#### `visitorServiceOverrideURL`

訪問プロファイルを取得するための基本URLを上書きします。ACCOUNT、PROFILE、および訪問IDは自動的にURLに追加されます。


```swift
config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
```

| タイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルを取得するためのURLを構成します | `"https://overridden-subdomain.yourdomain.com/"` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Serviceモジュールの構成メソッド
      config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
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
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
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