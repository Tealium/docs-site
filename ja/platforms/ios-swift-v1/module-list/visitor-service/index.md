---
title: VisitorServiceモジュール
description: Visitor Serviceから更新された訪問プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/visitor-service/
---

## 使用方法

VisitorServiceモジュールは、Tealium Customer Data Hubの[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスを保有しており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させたい場合は、このモジュールの使用をお勧めします。Customer Data Platform（CDP）のライセンスを保有していない場合、訪問プロファイルは返されないため、このモジュールの使用は推奨されません。

次のプラットフォームがサポートされています。

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageを使用してVisitorServiceモジュールをインストールします。

### CocoaPods

CocoaPodsを使用してVisitorServiceモジュールをインストールするには、次のpodをPodfileに追加します。  

```ruby
pod 'tealium-swift/TealiumCore'
pod 'tealium-swift/TealiumCollect' //or 'tealium-swift/TealiumTagManagement'
pod 'tealium-swift/TealiumVisitorService'
```

フレームワークは自動的にインスタンス化されます。このフレームワークは、`TealiumCore` podと、いずれか1つのディスパッチサービスpod（`TealiumCollect`または`TealiumTagManagement`）に依存します。iOSでのCocoaPodsによるインストールについては、[詳細をご覧ください](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)。

### Carthage

Carthageを使用してVisitorServiceモジュールをインストールするには、次の手順に従います。

1. XcodeでアプリターゲットのGeneral構成ページを開きます。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  

      ```ruby
      TealiumVisitorService.framework
      ```
3. VisitorServiceモジュールをセットアップするには、次の必須import文をプロジェクトに追加します。  

      ```swift
      import TealiumCore
      import TealiumCollect //or import TealiumTagManagement
      import TealiumVisitorService
      ```

フレームワークは自動的にインスタンス化されます。このフレームワークは、`TealiumCore`と、少なくとも1つのディスパッチサービス（`TealiumCore`または`TealiumTagManagement`）に依存します。追加のimport文は必要ありません。

iOSでのCarthageによるインストールについては、[詳細をご覧ください](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)。

## 訪問データオブジェクト

訪問プロファイルは、属性タイプごとのネイティブ構造体を含むオブジェクトです。訪問プロファイルオブジェクトには、訪問属性タイプと訪問属性タイプを区別できる`currentVisit`プロパティがあります。オーディエンスを除き、各属性値には添字を使用してIDでアクセスできます。`audiences`属性は、添字で照会したオーディエンスに訪問が属しているかどうかに応じて、単純に`true`/`false`を返します。例については、以下の一覧を参照してください。

**属性タイプ**

| パラメータ | プロパティ | 値 |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: [Bool] | `id: "5129", value: [true,false,true,true]` |
| `arraysOfNumbers` | id: String, value: [Double] | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings` | id: String, value: [String] | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `audiences` | id: String, name: String | `id: "tealiummobile\_demo\_103", name: "iOS Users"` |
| `badges` | id: String, value: Bool | `id: "2815", value: true` |
| `booleans` | id: String, value: Bool | `id: "4868", value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルには、オーディエンスまたはバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: [DateTime(id: "5376", value: 1567536668080), DateTime(id: "10", value: 1567536668000)], booleans: [Boolean(id: "4530", value: true], numbers: [Number(id: "32", value: 3.8)])` |
| `dates` | id: String, value: Int | `id: "22", value: 1567120112000` |
| `numbers` | id: String, value: Double | `id: "5728", value: 4.82125` |
| `setOfStrings` | id: String, value: Set[String] | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]` |
| `strings` | id: String, value: String | `id: "5380", value: "green shirts"` |
| `tallies` | id: String, value: [TallyValue] |  `id: "57", [[key: "category 1" count: 2.0], key: "category 2", count: 1.0]]` |
| `tallyValue` | key: String, count: Double | `[key: "category 1" count: 2.0]` |

#### `arraysOfBooleans`
カスタム添字を使用すると、IDによってブール値の配列を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.arraysOfBooleans` | 訪問プロファイル内のブール値の配列をすべて返します。 | `[BooleanArray]` | `[BooleanArray(id: "2333", value: [true,false]), BooleanArray(id: "1123", value: [true,true])]` |
| `profile.arraysOfBooleans["2815"]` | IDによってブール値の配列を返します。 | `[Bool]` | `true` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of booleans value
        if let arraysOfBooleans = profile.arraysOfBooleans?["5279"] {
            let numberOfPositiveBools = arraysOfBooleans.map { $0 == true }.count
            print(numberOfPositiveBools)
        }
}
```

#### `arraysOfNumbers`
カスタム添字を使用すると、IDによって数値の配列を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.arraysOfNumbers` | 訪問プロファイル内の数値の配列をすべて返します。 | `[NumberArray]` | `[NumberArray(id: "2333", value: [2.0, 1.0]), NumberArray(id: "1123", value: [4.82125, 3.0])]`|
| `profile.arraysOfNumbers["2815"]` | IDによって数値の配列を返します。 | `[Double]` | `[4.82125, 3.0]` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of numbers value
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
カスタム添字を使用すると、IDによって文字列の配列を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.arraysOfStrings` | 訪問プロファイル内の文字列の配列をすべて返します。 | `[StringArray]` | `[StringArray(id: "1033", value: ["Foundation", "Perfume"), StringArray(id: "3390", value: ["Bootleg Jeans", "Dresses"])]` |
| `profile.arraysOfStrings["3390"]` | IDによって文字列の配列を返します。 | `[String]` | `["Bootleg Jeans", "Dresses"]` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an array of strings value
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
カスタムサブスクリプトを使用すると、オーディエンスIDおよびオーディエンス名に基づいて、訪問がオーディエンスのメンバーであるかどうかを確認できます。

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.audiences` | 訪問がメンバーであるすべてのオーディエンスを返します。 | `[Audience]` | `[Audience(id: "tealiummobile\_demo\_103", name: "iOS Users"), Audience(id: "tealiummobile\_demo\_110", name: "Visitors - Known")]` |
| `profile.audiences[id: "103"]` | 渡されたIDに基づいて、訪問がオーディエンスのメンバーであるかどうかを真偽値で返します。 | `Bool` | `true`|
| `profile.audiences[name: "ios users"]` | 渡された名前に基づいて、訪問がオーディエンスのメンバーであるかどうかを真偽値で返します。名前では大文字と小文字が区別されません。 | `Bool` | `false` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return the current Audiences for which the user is assigned
        if let currentVisitorAudiences = profile.audiences {
            print("Visitor audiences: \(currentVisitorAudiences)")

            // Check if an Audience is assigned to a user by id
            if currentVisitorAudiences[id: "106"] {
                print("Visitor is a member of audience id 106")
                // ... Visitor is a member of this audience, take appropriate action
            }

            // Check if an Audience is assigned to a user by name
            if currentVisitorAudiences[name: "ios users"] {
                print("Visitor is a member of audience iOS Users")
                // ... Visitor is a member of this audience, take appropriate action
            }
        }
}
```

#### `badges`
カスタムサブスクリプトを使用すると、IDに基づいてバッジ値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.badges` | 訪問プロファイル内のすべてのバッジを返します。 | `[Badge]` | `[Badge(id: "2815", value: true), Badge(id: "2813", value: false)]`|
| `profile.badges["2815"]` | 訪問にバッジが割り当てられているかどうかを真偽値で返します。 | `Bool` | `true` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a badge value
        if let badgeAssigned = profile.badges?["5279"] {
            print(badgeAssigned ? "Badge id 5279 is assigned" : "Badge id 5945 is not assigned")
        }
}
```

#### `booleans`
カスタムサブスクリプトを使用すると、IDに基づいてブール値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.booleans` | 訪問プロファイル内のすべてのブール値を返します。 | `[Boolean]` | `[Boolean(id: "5784", value: true), Boolean(id: "1453", value: false)]` |
| `profile.booleans["4692"]` | IDに基づいてブール値を返します。 | `Bool` | `true` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a boolean value
        if let booleanValue = profile. booleans?["4479"] {
            if booleanValue {
            	// ... do something
            }
        }
}
```

#### `currentVisit`
訪問のライフタイム属性ではなく、現在の訪問に関する属性にアクセスします。

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile. currentVisit` | 現在の訪問をスコープとする属性を返します。 | `TealiumCurrentVisitProfile` | `TealiumCurrentVisitProfile (dates: [DateTime(id: "5376", value: 1567536668080), DateTime(id: "10", value: 1567536668000)], booleans: [Boolean(id: "4530", value: true], numbers: [Number(id: "32", value: 3.8)])` |
| `profile. currentVisit. ###` | ###に応じて、目的の属性を返します。上記と同じメソッドをすべて使用できますが、オーディエンスとバッジは除きます。これらは訪問専用の属性であり、訪問には適用されません。 | 場合により異なります | 場合により異なります |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a current visit string attribute
        if let currentVisit = profile.currentVisit,
           let string = currentVisit.strings?["34"] {
            print(string)
            // ... take action
        }
}
```

#### `dates`
カスタムサブスクリプトを使用すると、IDに基づいて日付値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.dates` | 訪問プロファイル内のすべての日付を返します。 | `[DateTime]` | `[DateTime(id: "22", value: 1567120112000), DateTime(id: "13", value: 1567120113245)]`|
| `profile.dates["4692"]` | IDに基づいて日付を返します。 | `Int` | `1567120112000` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a date value
        if let date = profile.dates?["33"] {
            print(date)
            // .. take action
        }
}
```

#### `numbers`
カスタムサブスクリプトを使用すると、IDに基づいて数値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.numbers` | 訪問プロファイル内のすべての数値を返します。 | `[Number]` | `[Number(id: "83", value: 0.5714285714285714), Number(id: "1399", value: 2.0)]` |
| `profile.numbers["1399"]` | IDに基づいて数値を返します。 | `Double` | `4.82125` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a number value
        if let number = profile. numbers?["1399"] {
            if number > 3.0 {
            	// ... take action
            }
        }
}
```


#### `setsOfStrings`

カスタムサブスクリプトを使用すると、IDに基づいて文字列セットの値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.setsOfStrings` | 訪問プロファイル内のすべての文字列セットを返します。 | `[SetOfStrings]` | `[SetOfStrings(id: "9938", value: ["shirts"]), SetOfStrings(id: "2300", value: ["Luxury Couch 1", "Luxury Couch 2"])]` |
| `profile.setsOfStrings["2300"]` | IDに基づいて文字列セットを返します。 | `Set<String>`| `["Luxury Couch 1", "Luxury Couch 2"]` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an set of strings value
        if let setOfStrings = profile.setsOfStrings?["5279"] {
            if setOfStrings.contains("toys") {
            	// ... take action
            }
        }
}
```


#### `strings`
カスタムサブスクリプトを使用すると、IDに基づいて文字列値を照会できます。  

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.strings` | 訪問プロファイル内のすべての文字列を返します。 | `[VisitorString]` | `[Number(id: "83", value: "Toy Truck"), Number(id: "5699", value: "Toy Tea Set")]`|
| `profile.strings["5699"]` | IDに基づいて文字列を返します。 | `String` | `"Toy Tea Set"` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return a string value
        if let string = profile.strings?["5699"] {
            print(string)
            // ... take action
        }
}
```
#### `tallies` と `tallyValue`
カスタム添字を使用すると、ID で集計を照会したり、ID で集計値を照会したりできます。

| 使用方法 | 説明 | 型 | 例 |
| --- | --- | --- | --- |
| `profile.tallies` | 訪問プロファイル内のすべての集計を返します。 | `[Tally]` | `[Tally(id: "2983", value: [TallyValue(key: "red shirts category", count: 4.0), TallyValue(key: "green shirts category", count: 2.0)]), Tally(id: "5643", value: [TallyValue(key: "girls", count: 3.0), TallyValue(key: "womens", count: 1.0)]`]
| `profile.tallies[tally: "1399"]` | ID で集計を返します。 | `[TallyValue]` | `[TallyValue(key: "girls", count: 3.0), TallyValue(key: "womens", count: 1.0)]` |
| `profile.tallies[tally: "1399", key: "womens"]` | ID で集計を返します。 | `Double` | `3.0` |

使用例：

```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // Return an entire tally
        if let tally = profile.tallies?["1399"] {
            print("Tally id 5377: \(tally)")
        }

        // Return a tally value by using the tally ID and the key for the value  you want
        if let tallyValue = profile.tallies?[tally: "5381", key: "red shirts"]{
            print("Tally value for id 5381 and key 'red shirts': \(tallyValue)")
        }
}
```

## API リファレンス

### クラス `Tealium`

更新された訪問プロファイルを操作するために、以下の API メソッドを使用できます。

#### `visitorService()`


使用例：

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
			// Note: this is inside the completion block after initialization

			// self.tealium is guaranteed to be initialized inside the completion block

			self.tealium?.visitorService()?.#### // where #### is any public API method on the visitorProfile object - see other methods for examples
		}
	}
}
```

#### `requestVisitorProfile()`

このメソッドは VisitorService へのリクエストを直ちにトリガーし、現在のプロファイルを取得します。前回の取得以降にプロファイルが更新されている場合、`profileDidUpdate` デリゲートメソッドが呼び出されます。

訪問プロファイルの更新間隔が `0` に構成されている場合、このメソッドはトラッキングリクエストが送信されるたびに自動的に呼び出されます。更新間隔により大きい値を構成している場合は、次回のスケジュール済み更新を待たずに、このメソッドを呼び出してプロファイルを即座に取得できます。

```swift
self.tealium?.visitorService()?.requestVisitorProfile()
```

使用例：

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

新しいリクエストをトリガーせずに、永続保存から直近に取得した訪問プロファイルを返します。インターネット接続がないものの、以前にリクエストが正常に完了している場合に役立ちます。

例：

```swift
self.tealium?.visitorService()?.getCachedProfile(completion: { profile in
                guard let profile = profile else { return }
                if let json = try? JSONEncoder().encode(profile), let string = String(data: 					json, encoding: .utf8) {
                    print(string)
   		}
})
```

| パラメータ | 説明 | 値の例 |
| --- | --- | --- |
| completion: TealiumVisitorProfile? | |  |

#### `removeAllVisitorServiceDelegates()`

すべての訪問プロファイルデリゲートを削除します。

```swift
self.tealium?.visitorService()?.removeAllVisitorServiceDelegates()
```

#### `addVisitorServiceDelegate()`

`VisitorServiceDelegate` に準拠する新しいクラスを追加します。


```swift
self.tealium?.visitorService()?.addVisitorServiceDelegate(self)
```

| パラメータ | 説明 | 例 |
| --- | --- | --- |
| `VisitorServiceDelegate` に準拠するクラスである delegate | | `ViewController, TealiumHelper` |

#### `removeSingleDelegate()`

特定の訪問プロファイルデリゲートを削除します。

例：

```swift
self.tealium?.visitorService()?.removeSingleDelegate(self)
```
| パラメータ | 説明 | 値の例 |
| --- | --- | --- |
| `VisitorServiceDelegate` に準拠するクラスである delegate | | `ViewController, TealiumHelper` |


### クラス：`TealiumVisitorServiceDelegate`

#### `profileDidUpdate()`

このメソッドは、訪問プロファイルが更新されるたびに呼び出されます。通常、`requestVisitorProfile()` メソッドが使用されるたびに呼び出されます。


```swift
func profileDidUpdate(profile: TealiumVisitorProfile?) {
        guard let profile = profile else { return }

        // act on profile attributes
        print(profile.audiences)

        ...
}
```

### クラス：`TealiumConfig`

#### `setVisitorServiceRefresh()`

訪問プロファイルを取得する頻度を構成できます。この構成のデフォルト値は 5 分です。頻度を調整するには、このメソッドを使用します。すべてのトラッキング呼び出しに `requestVisitorProfile` メソッドを追加した場合でも、この値を 0 に構成しない限り、プロファイルは毎回取得されません。

```swift
let config = TealiumConfig(...)
config.setVisitorServiceRefresh(3)
```

| パラメータ | 説明 | 例 |
| --- | --- | --- |
| interval | 訪問プロファイルを取得する頻度。整数、分単位。（デフォルト：`5`）| `3`  |

#### `addVisitorServiceDelegate()`

```swift
config.addVisitorServiceDelegate(self)
```
`profileDidUpdate` デリゲートメソッドを使用するため、VisitorService デリゲートの配列にデリゲートを追加します。複数のオブジェクトをデリゲートとして割り当てることができます。

| パラメータ | 説明 | 例 |
| --- | --- | --- |
| プロファイル更新を担当するクラス（デリゲート） | | `ViewController, TealiumHelper` |

#### `getVisitorServiceDelegates()`

VisitorService モジュールに割り当てられているデリゲートの一覧を返します。


```swift
config.getVisitorServiceDelegates()
```

#### `setVisitorServiceOverrideProfile()`

訪問プロファイルを取得するプロファイルを上書きします。Collect モジュールでデータ収集に使用するプロファイルと一致させる必要があります。


```swift
config. setVisitorServiceOverrideProfile("PROFILE")
```

#### `setVisitorServiceOverrideURL()`

```swift
config. setVisitorServiceOverrideURL("https://overridden-subdomain.yourdomain.com/")
```
訪問プロファイルの取得元となるベース URL を上書きします。ACCOUNT、PROFILE、および訪問 ID は URL に自動的に追加されます。


## リリースノート

1.8.0

* 初回リリース