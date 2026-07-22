---
title: VisitorServiceモジュール
description: 訪問サービスから更新された訪問プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/visitor-service/
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

VisitorServiceモジュールは、CocoaPodsまたはCarthageでインストールできます。

### CocoaPods

CocoaPodsでVisitorServiceモジュールをインストールするには、Podfileに以下のpodsを追加します：

```ruby
pod 'tealium-swift/TealiumCore'
pod 'tealium-swift/TealiumCollect' //or 'tealium-swift/TealiumTagManagement'
pod 'tealium-swift/TealiumVisitorService'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podと、ディスパッチサービスpods（`TealiumCollect`または`TealiumTagManagement`のいずれか）に依存しています。iOSのCocoaPodsインストールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)。

### Carthage

CarthageでVisitorServiceモジュールをインストールするには、以下の手順に従います：

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに以下のフレームワークを追加します：

      ```ruby
      TealiumVisitorService.framework
      ```
3. VisitorServiceモジュールを構成するために、プロジェクトに以下の必要なインポートステートメントを追加します：

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`と少なくとも1つのディスパッチサービス（`TealiumCore`または`TealiumTagManagement`）に依存しています。追加のインポートステートメントは必要ありません。

iOSのCarthageインストールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)。

## 訪問データオブジェクト

訪問プロファイルは、各属性タイプのネイティブ構造体を含むオブジェクトです。訪問プロファイルオブジェクト内には、訪問/訪問属性タイプを区別するための`currentVisit`プロパティがあります。オーディエンスを除き、各属性値はIDを使用してサブスクリプトでアクセス可能です。`audiences`属性は、サブスクリプトを介してクエリされたオーディエンスのメンバーであるかどうかを`true`/`false`で単純に返します。以下のリストで例を参照してください。

**属性タイプ**

| パラメータ | プロパティ |  値 |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: [Bool] | `id: "5129", value: [true,false,true,true]` |
| `arraysOfNumbers` | id: String, value: [Double] | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings` | id: String, value: [String] | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `audiences` | id: String, name: String | `id: "tealiummobile\_demo\_103", name: "iOS Users"` |
| `badges` | id: String, value: Bool | `id: "2815", value: true` |
| `booleans` | id: String, value: Bool | `id: "4868", value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルにはオーディエンスやバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: [DateTime(id: "5376", value: 1567536668080), DateTime(id: "10", value: 1567536668000)], booleans: [Boolean(id: "4530", value: true], numbers: [Number(id: "32", value: 3.8)])` |
| `dates` | id: String, value: Int | `id: "22", value: 1567120112000` |
| `numbers` | id: String, value: Double | `id: "5728", value: 4.82125` |
| `setOfStrings` | id: String, value: Set[String] | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]` |
| `strings` | id: String, value: String | `id: "5380", value: "green shirts"` |
| `tallies` | id: String, value: [TallyValue] |  `id: "57", [[key: "category 1" count: 2.0], key: "category 2", count: 1.0]]` |
| `tallyValue` | key: String, count: Double | `[key: "category 1" count: 2.0]` |

#### `arraysOfBooleans`
カスタムサブスクリプションを使用して、idによるブール値の配列をクエリできます。

| 使用法 | 説明 |  タイプ | 例 |
| --- | --- | --- | --- |
| `profile.arraysOfBooleans` | 訪問プロファイルのすべてのブール値の配列を返します。 | `[BooleanArray]` | `[BooleanArray(id: "2333", value: [true,false]), BooleanArray(id: "1123", value: [true,true])]` |
| `profile.arraysOfBooleans["2815"]` | idによるブール値の配列を返します。 | `[Bool]` | `true` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // ブール値の配列を返す
        if let arraysOfBooleans = profile.arraysOfBooleans?["5279"] {
            let numberOfPositiveBools = arraysOfBooleans.map { $0 == true }.count
            print(numberOfPositiveBools)
        }
}
```

#### `arraysOfNumbers`
カスタムサブスクリプションを使用して、idによる数値の配列をクエリできます。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.arraysOfNumbers` | 訪問プロファイルのすべての数値の配列を返します。 | `[NumberArray]` | `[NumberArray(id: "2333", value: [2.0, 1.0]), NumberArray(id: "1123", value: [4.82125, 3.0])]`|
| `profile.arraysOfNumbers["2815"]` | idによる数値の配列を返します。 | `[Double]` | `[4.82125, 3.0]` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile is profile else { return }

        // 数値の配列を返す
        if let arraysOfNumbers = profile. arraysOfNumbers?["5279"] {
            arraysOfNumbers.forEach { number in
        		if number > 3.0 {
        			// ... take action
        		}
            }
        }
}
```

#### `arraysOfStrings`
カスタムサブスクリプションを使用して、idによる文字列の配列をクエリできます。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.arraysOfStrings` | 訪問プロファイルのすべての文字列の配列を返します。 | `[StringArray]` | `[StringArray(id: "1033", value: ["Foundation", "Perfume"), StringArray(id: "3390", value: ["Bootleg Jeans", "Dresses"])]` |
| `profile.arraysOfStrings["3390"]` | idによる文字列の配列を返します。 | `[String]` | `["Bootleg Jeans", "Dresses"]` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 文字列の配列を返す
        if let arraysOfStrings = profile.arraysOfStrings?["3390"] {
            arraysOfStrings.forEach { string in
        		if string.lowercased().contains("Jeans") {
        			// ... take action
        		}
            }
        }
}
```
#### `audiences`
カスタムサブスクリプションにより、訪問のオーディエンスIDと名前に基づいてオーディエンスメンバーシップのチェックが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.audiences` | 訪問がメンバーである全オーディエンスを返します。 | `[Audience]` | `[Audience(id: "tealiummobile\_demo\_103", name: "iOS Users"), Audience(id: "tealiummobile\_demo\_110", name: "Visitors - Known")]` |
| `profile.audiences[id: "103"]` | IDに基づいて訪問がオーディエンスのメンバーかどうかをtrue/falseで返します。 | `Bool` | `true`|
| `profile.audiences[name: "ios users"]` | 名前に基づいて訪問がオーディエンスのメンバーかどうかをtrue/falseで返します。名前は大文字小文字を区別しません。 | `Bool` | `false` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 現在割り当てられているオーディエンスを返す
        if let currentVisitorAudiences = profile.audiences {
            print("Visitor audiences: \(currentVisitorAudiences)")

            // IDによってユーザーに割り当てられたオーディエンスをチェック
            if currentVisitorAudiences[id: "106"] {
                print("Visitor is a member of audience id 106")
                // ... このオーディエンスのメンバーであれば適切なアクションを取る
            }

            // 名前によってユーザーに割り当てられたオーディエンスをチェック
            if currentVisitorAudiences[name: "ios users"] {
                print("Visitor is a member of audience iOS Users")
                // ... このオーディエンスのメンバーであれば適切なアクションを取る
            }
        }
}
```

#### `badges`
カスタムサブスクリプションにより、IDによるバッジ値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.badges` | 訪問プロファイルの全バッジを返します。 | `[Badge]` | `[Badge(id: "2815", value: true), Badge(id: "2813", value: false)]`|
| `profile.badges["2815"]` | 訪問にバッジが割り当てられているかどうかをtrue/falseで返します。 | `Bool` | `true` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // バッジ値を返す
        if let badgeAssigned = profile.badges?["5279"] {
            print(badgeAssigned ? "Badge id 5279 is assigned" : "Badge id 5945 is not assigned")
        }
}
```

#### `booleans`
カスタムサブスクリプションにより、IDによるブール値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.booleans` | 訪問プロファイルの全ブール値を返します。 | `[Boolean]` | `[Boolean(id: "5784", value: true), Boolean(id: "1453", value: false)]` |
| `profile.booleans["4692"]` | IDによるブール値を返します。 | `Bool` | `true` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile is profile else { return }

        // ブール値を返す
        if let booleanValue = profile.booleans?["4479"] {
            if booleanValue {
            	// ... 何かをする
            }
        }
}
```

#### `currentVisit`
訪問のライフタイム属性ではなく、現在の訪問に関する属性へのアクセス。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.currentVisit` | 現在の訪問に関する属性を返します。 | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile (dates: [DateTime(id: "5376", value: 1567536668080), DateTime(id: "10", value: 1567536668000)], booleans: [Boolean(id: "4530", value: true)], numbers: [Number(id: "32", value: 3.8)])` |
| `profile.currentVisit.###` | ###に応じて属性を返します。上記にリストされたメソッドはすべて適用されますが、オーディエンスとバッジは訪問属性専用であり、訪問には適用されません。 | 変動 | 変動 |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 現在の訪問の文字列属性を返す
        if let currentVisit = profile.currentVisit,
           let string = currentVisit.strings?["34"] {
            print(string)
            // ... アクションを取る
        }
}
```

#### `dates`
カスタムサブスクリプションにより、IDによる日付値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.dates` | 訪問プロファイルの全日付を返します。 | `[DateTime]` | `[DateTime(id: "22", value: 1567120112000), DateTime(id: "13", value: 1567120113245)]`|
| `profile.dates["4692"]` | IDによる日付を返します。 | `Int` | `1567120112000` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 日付値を返す
        if let date = profile.dates?["33"] {
            print(date)
            // .. アクションを取る
        }
}
```

#### `numbers`
カスタムサブスクリプションにより、IDによる数値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.numbers` | 訪問プロファイルの全数値を返します。 | `[Number]` | `[Number(id: "83", value: 0.5714285714285714), Number(id: "1399", value: 2.0)]` |
| `profile.numbers["1399"]` | IDによる数値を返します。 | `Double` | `4.82125` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 数値を返す
        if let number = profile.numbers?["1399"] {
            if number > 3.0 {
            	// ... アクションを取る
            }
        }
}
```

#### `setsOfStrings`

カスタムサブスクリプションにより、IDによる文字列セットのクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.setsOfStrings` | 訪問プロファイルの全文字列セットを返します。 | `[SetOfStrings]` | `[SetOfStrings(id: "9938", value: ["shirts"]), SetOfStrings(id: "2300", value: ["Luxury Couch 1", "Luxury Couch 2"])]` |
| `profile.setsOfStrings["2300"]` | IDによる文字列セットを返します。 | `Set<String>`| `["Luxury Couch 1", "Luxury Couch 2"]` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile is profile else { return }

        // 文字列セットの値を返す
        if let setOfStrings = profile.setsOfStrings?["5279"] {
            if setOfStrings.contains("toys") {
            	// ... アクションを取る
            }
        }
}
```

#### `strings`
カスタムサブスクリプションにより、IDによる文字列値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.strings` | 訪問プロファイルの全文字列を返します。 | `[VisitorString]` | `[Number(id: "83", value: "Toy Truck"), Number(id: "5699", value: "Toy Tea Set")]`|
| `profile.strings["5699"]` | IDによる文字列を返します。 | `String` | `"Toy Tea Set"` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 文字列値を返す
        if let string = profile.strings?["5699"] {
            print(string)
            // ... アクションを取る
        }
}
```
#### `tallies` と `tallyValue`
カスタム添字を使用して、IDによる集計のクエリとIDによる集計値のクエリが可能です。

| 使用法 | 説明 |  タイプ | 例  |
| --- | --- | --- | --- |
| `profile.tallies` | 訪問プロファイルのすべての集計を返します。 | `[Tally]` | `[Tally(id: "2983", value: [TallyValue(key: "red shirts category", count: 4.0), TallyValue(key: "green shirts category", count: 2.0)]), Tally(id: "5643", value: [TallyValue(key: "girls", count: 3.0), TallyValue(key: "womens", count: 1.0)]`]
| `profile.tallies[tally: "1399"]` | IDによる集計を返します。 | `[TallyValue]` | `[TallyValue(key: "girls", count: 3.0), TallyValue(key: "womens", count: 1.0)]` |
| `profile.tallies[tally: "1399", key: "womens"]` | IDによる集計を返します。 | `Double` | `3.0` |

使用例:

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // 全体の集計を返す
        if let tally = profile.tallies?["1399"] {
            print("Tally id 5377: \(tally)")
        }

        // 集計IDと値のキーを使用して集計値を返す
        if let tallyValue = profile.tallies?[tally: "5381", key: "red shirts"]{
            print("Tally value for id 5381 and key 'red shirts': \(tallyValue)")
        }
}
```

## API リファレンス

### クラス `Tealium`

以下のAPIメソッドが訪問プロファイルの更新に対して利用可能です。

#### `visitorService()`

使用例:

```swift
class MyHelperClass {
    var tealium: Tealium?

    public init () {
        let config = TealiumConfig(account: "ACCOUNT",
                                   profile: "PROFILE",
                                   environment: "ENVIRONMENT",
                                   datasource: "DATASOURCE",
                                   optionalData: nil)
        config.addVisitorServiceDelegate(self)                           
	     config.setVisitorServiceRefresh(interval: 10)		
		self.tealium = Tealium(config) {
			// 初期化後の完了ブロック内

			// self.tealiumは完了ブロック内で初期化が保証されています

			self.tealium?.visitorService()? // visitorProfileオブジェクトの公開APIメソッドを参照してください
		}
	}
}
```

#### `requestVisitorProfile()`

このメソッドは、VisitorServiceに現在のプロファイルを即時に要求します。プロファイルが最後のフェッチ以降に更新されていた場合、`profileDidUpdate`デリゲートメソッドが呼び出されます。

このメソッドは、トラックリクエストが送信されるたびに自動的に呼び出されますが、訪問プロファイルの更新間隔を`0`に構成していない限り、毎回プロファイルが取得されるわけではありません。更新間隔を高い値に構成している場合は、次のスケジュールされた更新を待たずにこのメソッドを呼び出してプロファイルを即座に取得することができます。

```swift
self.tealium?.visitorService()?.requestVisitorProfile()
```

使用例:

```swift
func track(title: String, data: [String: Any]?) {
        tealium?.track(title: title, data: data, completion: { success, \_, error in
            if error != nil {
                print("*** Track not completed because of error: \n\(String(describing: error))")
            }
            if success {
                print("*** Track with VisitorService completed ***")
                self.tealium?.visitorProfile()?.requestVisitorProfile()

            }
        })
    }
```

#### `getCachedProfile()`

最近取得した訪問プロファイルを永続保存から返します。新たなリクエストをトリガーせずに、インターネット接続がない状況でも以前の成功したリクエストがあれば役立ちます。

例:

```swift
self.tealium?.visitorService()?.getCachedProfile(completion: { profile in
                guard let profile = profile else { return }
                if let json = try? JSONEncoder().encode(profile), let string = String(data: json, encoding: .utf8) {
                    print(string)
   		}
})
```

| パラメータ | 説明 | 例値 |
| --- | --- | --- |
| completion: TealiumVisitorProfile? | |  |

#### `removeAllVisitorServiceDelegates()`

すべての訪問プロファイルデリゲートを削除します。

```swift
self.tealium?.visitorService()?.removeAllVisitorServiceDelegates()
```

#### `addVisitorServiceDelegate()`

`VisitorServiceDelegate`に準拠する新しいクラスを追加します。

```swift
self.tealium?.visitorService()?.addVisitorServiceDelegate(self)
```

| パラメータ | 説明 | 例  |
| --- | --- | --- |
| delegate: `VisitorServiceDelegate`に準拠するクラス | | `ViewController, TealiumHelper` |

#### `removeSingleDelegate()`

特定の訪問プロファイルデリゲートを削除します。

例:

```swift
self.tealium?.visitorService()?.removeSingleDelegate(self)
```
| パラメータ | 説明 | 例値 |
| --- | --- | --- |
| delegate: `VisitorServiceDelegate`に準拠するクラス | | `ViewController, TealiumHelper` |


### クラス: `TealiumVisitorServiceDelegate`

#### `profileDidUpdate()`

訪問プロファイルが更新されたときにこのメソッドが呼び出されます。これは、`requestVisitorProfile()`メソッドが使用されるたびにほとんどの場合呼び出されます。

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile is profile else { return }

        // プロファイル属性に対応する
        print(profile.audiences)

        ...
}
```

### クラス: `TealiumConfig`

#### `setVisitorServiceRefresh()`

訪問プロファイルの取得頻度を構成します。この構成のデフォルト値は5分です。このメソッドを使用して頻度を調整します。`requestVisitorProfile`メソッドをすべてのトラッキングコールに追加しても、この構成を0に構成しない限り、プロファイルは毎回取得されません。

```swift
let config = TealiumConfig(...)
config.setVisitorServiceRefresh(3)
```

| パラメータ | 説明 | 例  |
| --- | --- | --- |
| interval | 訪問プロファイルを取得する頻度。整数、分。(デフォルト: `5`)| `3`  |

#### `addVisitorServiceDelegate()`

```swift
config.addVisitorServiceDelegate(self)
```
`profileDidUpdate`デリゲートメソッドを使用するために、VisitorServiceデリゲートの配列にデリゲートを追加します。複数のオブジェクトがデリゲートとして割り当てられることがあります。

| パラメータ | 説明 | 例  |
| --- | --- | --- |
| プロファイル更新を担当するクラス (delegate) | | `ViewController, TealiumHelper` |

#### `getVisitorServiceDelegates()`

VisitorServiceモジュールに割り当てられたデリゲートのリストを返します。

```swift
config.getVisitorServiceDelegates()
```

#### `setVisitorServiceOverrideProfile()`

訪問プロファイルを取得するプロファイルを上書きします。Collectモジュールで使用されるプロファイルと一致する必要があります。

```swift
config.setVisitorServiceOverrideProfile("PROFILE")
```

#### `setVisitorServiceOverrideURL()`

```swift
config.setVisitorServiceOverrideURL("https://overridden-subdomain.yourdomain.com/")
```
訪問プロファイルが取得される基本URLを上書きします。ACCOUNT、PROFILE、および訪問IDは自動的にURLに追加されます。


## リリースノート

1.8.0

* 初回リリース
