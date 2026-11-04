---
title: VisitorService モジュール
description: ビジターサービスから更新されたビジタープロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/
---

## 使用方法

VisitorService モジュールは、Tealium Customer Data Hub の[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスを保有しており、ビジタープロファイルを使用してモバイルアプリケーションのユーザー体験を向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスを保有していない場合、ビジタープロファイルは返されないため、このモジュールの使用は推奨されません。

次のプラットフォームがサポートされています。

* iOS
* tvOS
* watchOS
* macOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してVisitorServiceモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
1. バージョンルールを構成します。通常は`"Up to next major"`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールするモジュールのリストから`VisitorService`、`Core`、および`Collect`または`TagManagement`のいずれかを選択し、Xcodeプロジェクトの**Frameworks and Libraries**で各アプリターゲットに追加します。

### CocoaPods

CocoaPodsを使用してVisitorServiceモジュールをインストールするには、次のPodをPodfileに追加します。  

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' //or 'tealium-swift/TagManagement'
pod 'tealium-swift/VisitorService'
```

詳しくは、[iOS向けCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。

### Carthage

Carthageを使用してVisitorServiceモジュールをインストールするには、次の手順に従います。

1. Xcodeで、アプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  

      ```perl
      TealiumVisitorService.framework
      ```
3. VisitorServiceモジュールを構成するには、次の必須import文をプロジェクトに追加します。  

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

詳しくは、[iOS向けCarthageのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティにモジュールが指定されていることを確認します。

`config.collectors = [Collectors.VisitorService]`

## ビジターデータオブジェクト

ビジタープロファイルは、各属性のわかりやすい名前を含むオブジェクトです。`currentVisit`プロパティを使用すると、ビジター属性と訪問属性のタイプを区別できます。添字を使用して、IDごとに各属性値へアクセスします。属性が存在しない場合は`nil`が返されます。例については、次のリストを参照してください。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `arraysOfBooleans` | id: String、value: [Bool]                                                                                        | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String、value: [Double]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String、value: [String]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String、value: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String、value: Bool                                                                                          | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String、value: Bool                                                                                          | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問のvisitorProfileに含まれるすべての属性。現在の訪問プロファイルにはAudiencesまたはBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String、value: Int                                                                                           | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String、value: Double                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String、value: Set<String>                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String、value: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String、value: [String:Double]                                                                               | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String、value: Double                                                                                        | `["category 1": 2.0]`                                                                                                             |


<blockquote>
AudienceまたはBadgeが割り当てられていない場合は、`nil`が返されます。
</blockquote>

#### `arraysOfBooleans`

| 使用方法                                  | 説明                                                         | 型                 | 例                                            |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------ | --------------------------------------------- |
| `visitorProfile.arraysOfBooleans`         | 訪問プロファイル内のすべてのブール値配列を返します。       | `[String: [Bool]]` | `["2333": [true,false], "1123": [true,true]]` |
| `visitorProfile.arraysOfBooleans["2815"]` | ID に基づいてブール値の配列を返します。                      | `[Bool]`           | `[true,true]`                                 |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of booleans value
    if let arraysOfBooleans = visitorProfile.arraysOfBooleans?["5279"] {
        let numberOfPositiveBools = arraysOfBooleans.filter { $0 == true }.count
        print(numberOfPositiveBools)
    }
}
```

#### `arraysOfNumbers`  

| 使用方法                                 | 説明                                                     | 型                   | 例                                             |
| ---------------------------------------- | -------------------------------------------------------- | -------------------- | ---------------------------------------------- |
| `visitorProfile.arraysOfNumbers`         | 訪問プロファイル内のすべての数値配列を返します。       | `[String: [Double]]` | `["2333": [2.0, 1.0], "1123": [4.82125, 3.0]]` |
| `visitorProfile.arraysOfNumbers["2815"]` | ID に基づいて数値の配列を返します。                      | `[Double]`           | `[4.82125, 3.0]`                               |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of numbers value
    if let arraysOfNumbers = visitorProfile.arraysOfNumbers?["5279"] {
        arraysOfNumbers.forEach { number in
    		if number > 3.0 {
    			// ... take action
    		}
        }
    }
}
```

#### `arraysOfStrings`  

| 使用方法                                 | 説明                                                       | 型                   | 例                                                                          |
| ---------------------------------------- | ---------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------- |
| `visitorProfile.arraysOfStrings`         | 訪問プロファイル内のすべての文字列配列を返します。       | `[String: [String]]` | `["1033": ["Foundation", "Perfume"], "3390": ["Bootleg Jeans", "Dresses"]]` |
| `visitorProfile.arraysOfStrings["3390"]` | ID に基づいて文字列の配列を返します。                      | `[String]`           | `["Bootleg Jeans", "Dresses"]`                                              |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an array of strings value
    if let arraysOfStrings = visitorProfile.arraysOfStrings?["3390"] {
        arraysOfStrings.forEach { string in
    		if string.lowercased().contains("Jeans") {
    			// ... take action
    		}
        }
    }
}
```

#### `audiences`

| 使用方法                          | 説明                                                                                                   | 型                 | 例                                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------ | ------------------------------------------------------------------------------------------- |
| `visitorProfile.audiences`        | 訪問がメンバーになっているすべてのオーディエンスを返します。                                       | `[String: String]` | `["tealiummobile\_demo\_103": "iOS Users", "tealiummobile\_demo\_110": "Visitors - Known"]` |
| `visitorProfile.audiences["103"]` | 渡された ID に基づき、訪問がそのオーディエンスのメンバーであるかどうかを真偽値で返します。          | `Bool`             | `true`                                                                                      |


<blockquote>
オーディエンスが割り当てられていない場合は、`nil` が返されます。
</blockquote>


使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return the current Audiences for which the user is assigned
    if let audiences = visitorProfile.audiences {
        print("Visitor audiences: \(audiences)")

        // Check if an Audience is assigned to a user by id
        if audiences["account_profile_106"] != nil {
            print("Visitor is a member of audience id 106")
            // ... Visitor is a member of this audience, take appropriate action
        }

    }
}
```

#### `badges`  

| 使用方法                        | 説明                                                                                   | 型               | 例                             |
| ------------------------------- | -------------------------------------------------------------------------------------- | ---------------- | ------------------------------ |
| `visitorProfile.badges`         | 訪問プロファイル内のすべてのバッジを返します。                                       | `[String: Bool]` | `["2815": true, "2813": true]` |
| `visitorProfile.badges["2815"]` | 訪問にそのバッジが割り当てられているかどうかを真偽値で返します。                     | `Bool`           | `true`                         |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a badge value
    if let badgeAssigned = visitorProfile.badges?["5279"] {
        print(badgeAssigned ? "Badge id 5279 is assigned" : "Badge id 5945 is not assigned")
    }
}
```


<blockquote>
バッジが割り当てられていない場合は、`nil` が返されます。
</blockquote>


#### `booleans`

| 使用方法                          | 説明                                                     | 型               | 例                              |
| --------------------------------- | -------------------------------------------------------- | ---------------- | ------------------------------- |
| `visitorProfile.booleans`         | 訪問プロファイル内のすべてのブール値を返します。       | `[String: Bool]` | `["5784": true, "1453": false]` |
| `visitorProfile.booleans["4692"]` | ID に基づいてブール値を返します。                        | `Bool`           | `true`                          |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a boolean value
    if let booleanValue = visitorProfile.booleans?["4479"] {
        if booleanValue {
        	// ... do something
        }
    }
}
```
#### `currentVisit`
訪問のライフタイム属性ではなく、現在の訪問に関する属性にアクセスします。

| 使用方法                          | 説明                                                                                                                                                                       | 型                           | 例                                                                                                                                |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.currentVisit`     | 現在の訪問をスコープとする属性を返します。                                                                                                                                 | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `visitorProfile.currentVisit.###` | ### に応じて、目的の属性を返します。オーディエンスとバッジを除き、上記と同じメソッドがすべて適用されます。これらは訪問専用の属性であり、訪問には適用されません。              | 属性によって異なる           | 属性によって異なる                                                                                                                |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a current visit string attribute
    if let currentVisit = visitorProfile.currentVisit,
       let string = currentVisit.strings?["34"] {
        print(string)
        // ... take action
    }
}
```

#### `dates`

| 使用方法                       | 説明                                           | 型              | 例                                           |
| ------------------------------ | ---------------------------------------------- | --------------- | -------------------------------------------- |
| `visitorProfile.dates`         | 訪問プロファイル内のすべての日付を返します。 | `[String: Int]` | `["25": 1567120112000, "13": 1567120145666]` |
| `visitorProfile.dates["4692"]` | ID によって日付を返します。                    | `Int`           | `1567120112000`                              |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a date value
    if let date = visitorProfile.dates?["33"] {
        print(date)
        // .. take action
    }
}
```

#### `numbers`

| 使用方法                         | 説明                                           | 型                 | 例                                        |
| -------------------------------- | ---------------------------------------------- | ------------------ | ----------------------------------------- |
| `visitorProfile.numbers`         | 訪問プロファイル内のすべての数値を返します。 | `[String: Double]` | `["83": 0.5714285714285714, "1399": 2.0]` |
| `visitorProfile.numbers["1399"]` | ID によって数値を返します。                    | `Double`           | `4.82125`                                 |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a number value
    if let number = visitorProfile.numbers?["1399"] {
        if number > 3.0 {
        	// ... take action
        }
    }
}
```


#### `setsOfStrings`

| 使用方法                               | 説明                                                   | 型                      | 例                                                                   |
| -------------------------------------- | ------------------------------------------------------ | ----------------------- | -------------------------------------------------------------------- |
| `visitorProfile.setsOfStrings`         | 訪問プロファイル内の文字列セットをすべて返します。   | `[String: Set<String>]` | `["9938": ["shirts"], "2300": ["Luxury Couch 1", "Luxury Couch 2"]]` |
| `visitorProfile.setsOfStrings["2300"]` | ID によって文字列セットを返します。                    | `Set<String>`           | `["Luxury Couch 1", "Luxury Couch 2"]`                               |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an set of strings value
    if let setOfStrings = visitorProfile.setsOfStrings?["5279"] {
        if setOfStrings.contains("toys") {
        	// ... take action
        }
    }
}
```


#### `strings`

| 使用方法                         | 説明                                             | 型       | 例                                          |
| -------------------------------- | ------------------------------------------------ | -------- | ------------------------------------------- |
| `visitorProfile.strings`         | 訪問プロファイル内のすべての文字列を返します。 | `String` | `"83": "Toy Truck", "5699": "Toy Tea Set"]` |
| `visitorProfile.strings["5699"]` | ID によって文字列を返します。                    | `String` | `"Toy Tea Set"`                             |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return a string value
    if let string = visitorProfile.strings?["5699"] {
        print(string)
        // ... take action
    }
}
```

#### `tallies`

| 使用方法                                   | 説明                                           | 型                           | 例                                                                                                             |
| ------------------------------------------ | ---------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `visitorProfile.tallies`                   | 訪問プロファイル内のすべての集計を返します。 | `[String: [String: Double]]` | `["2983": ["red shirts category": 4.0, "green shirts category": 2.0], "5643": ["girls": 3.0, "womens": 1.0]]`] |
| `visitorProfile.tallies["1399"]`           | ID によって集計を返します。                    | `[String: Double]`           | `["girls": 3.0, "womens": 1.0]`                                                                                |
| `visitorProfile.tallies["1399"]["womens"]` | ID によって集計値を返します。                  | `Double`                     | `3.0`                                                                                                          |

使用例：

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Return an entire tally
    if let tally = visitorProfile.tallies?["1399"] {
        print("Tally id 5377: \(tally)")
    }

    // Return a tally value by using the tally id and the key for the value you want
    if let tally = visitorProfile.tallies?["5381"], let tallyValue = tally["red shirts"] {
        print("Tally value for id 5381 and key 'red shirts': \(tallyValue)")
    }
}
```

## API リファレンス

### `Tealium` クラス

以下に、VisitorService モジュールでよく使用されるメソッドとプロパティの概要を示します。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| [`cachedProfile`](#cachedprofile) | 新しいリクエストをトリガーせずに、永続保存から直近に取得された訪問プロファイルを返します |
| [`requestVisitorProfile()`](#requestvisitorprofile) | 現在の訪問プロファイルを取得するため、VisitorService へのリクエストを即座にトリガーします |
| [`visitorService`](#visitorservice) | VisitorService モジュールのプロパティ |
#### `cachedProfile`

永続保存から最後に取得した訪問プロファイルを返します。新しいリクエストはトリガーされません。インターネット接続がないものの、以前にリクエストが正常に完了している場合に役立ちます。

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

VisitorService に即時リクエストを送信し、現在の訪問プロファイルを取得します。前回の取得後にプロファイルが更新されている場合は、[`didUpdate()`](#didupdate) デリゲートメソッドが呼び出されます。

訪問プロファイルの更新間隔が `0` に構成されている場合、このメソッドはトラッキングリクエストが送信されるたびに自動的に呼び出されます。更新間隔にそれより大きな値を構成している場合は、次回のスケジュールされた更新を待たずにプロファイルを取得するため、このメソッドを呼び出すことができます。

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

VisitorService モジュールです。

```swift
self.tealium?.visitorService?.####
```

`####` は、`visitorService` オブジェクトの任意のパブリック API メソッドです。完全な使用例を次に示します。

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
            // Note: this is inside the completion block after initialization

            // self.tealium is guaranteed to be initialized inside the completion block
            self.tealium?.visitorService?.####
        }
    }
}
```

### クラス：`VisitorServiceDelegate`

VisitorService モジュールでよく使用されるメソッドとプロパティの概要を次に示します。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| [`didUpdate()`](#didupdate) | プロファイルが更新されたときに、更新後の訪問プロファイルを返すコールバックメソッドです。 |

#### `didUpdate()`

プロファイルが更新されたとき、または `requestVisitorProfile()` メソッドが呼び出されたときに、更新後の訪問プロファイルを返すコールバックメソッドです。この動作は、デフォルトで5分に構成されている更新間隔の値によって異なります。

```swift
func didUpdate(visitorProfile: TealiumVisitorProfile) {
    // Act on profile attributes
    print(visitorProfile.audiences)
    //...
}
```

| パラメータ | 説明 | 例 |
| ------ | ----------- | --------------------------------- |
| `TealiumVisitorProfile` | Tealium 訪問プロファイル | `visitorProfile` |


### クラス：`TealiumConfig`

VisitorService モジュールでよく使用されるメソッドとプロパティの概要を次に示します。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| [`visitorServiceDelegate`](#visitorservicedelegate) | `didUpdate` デリゲートメソッドを使用するデリゲートを構成します |
| [`visitorServiceOverrideProfile`](#visitorserviceoverrideprofile) | 訪問プロファイルの取得元となるプロファイルを上書きします |
| [`visitorServiceOverrideURL`](#visitorserviceoverrideurl) | 訪問プロファイルの取得元となるベース URL を上書きします |
| [`visitorServiceRefresh`](#visitorservicerefresh) | 訪問プロファイルを取得する頻度を構成します |


#### `visitorServiceDelegate`

[`didUpdate`](#didupdate) デリゲートメソッドを使用するデリゲートを構成します。

```swift
config.visitorServiceDelegate = self
```

| 型 | 説明 | 例 |
| ------ | ----------- | --------------------------------- |
| `Class` | プロファイルの更新を処理するクラス（デリゲート） | `AnalyticsManager`、`TealiumHelper` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium VisitorService module config methods
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

訪問プロファイルの取得元となるプロファイルを上書きします。Collect モジュールでのデータ収集に使用するプロファイルと一致させてください。


```swift
config.visitorServiceOverrideProfile = "PROFILE"
```

| 型 | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルの取得元となる AudienceStream プロファイルを構成します | `"main"` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideProfile = "main"
  }
```

#### `visitorServiceOverrideURL`

訪問プロファイルの取得元となるベース URL を上書きします。ACCOUNT、PROFILE、および訪問 ID は URL に自動的に追加されます。


```swift
config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
```

| 型 | 説明 | 例 |
| --- | --- | --- |
| `String` | 訪問プロファイルの取得元となる URL を構成します | `"https://overridden-subdomain.yourdomain.com/"` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceOverrideURL = "https://overridden-subdomain.yourdomain.com/"
  }
```

#### `visitorServiceRefresh`

このプロパティを使用して、訪問プロファイルを取得する頻度を調整します。デフォルト値は5分です。すべてのトラッキング呼び出しに `requestVisitorProfile()` メソッドを追加しても、この値を `0` に構成しない限り、毎回プロファイルが取得されるわけではありません。

```swift
let config = TealiumConfig(...)
config.visitorServiceRefresh = .every(3, .seconds)
```

`RefreshInterval` のオプション：`seconds`、`minutes`、または `hours`

| パラメータ | 説明 | 例 |
| ---------- | -------------------------------------------------------------------------------------- | ------- |
| `.every(Int, RefreshInterval)` | 訪問プロファイルを取得する頻度（デフォルト：`.every(5, .minutes)`） | `.every(15, .seconds)` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Visitor Service module config methods
      config.visitorServiceRefresh = .every(3, .seconds)
  }
```
## リリースノート

2.0.0

**影響の大きい変更**

* パフォーマンス向上のため TealiumVisitorProfile を更新
* 簡素化のためマルチキャストデリゲート機能を削除
* キャッシュ済みプロファイルメソッドから完了ハンドラーを削除

**影響の小さい変更**

* 更新間隔のオプションを追加
* 一貫性を保つためクラス名を更新
* デリゲートメソッドのシグネチャを更新
* テストを改善

1.8.0

* 初回リリース