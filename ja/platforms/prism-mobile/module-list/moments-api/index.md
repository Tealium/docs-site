---
title: Context APIモジュール
description: Tealium Prism SDKのContext APIモジュール（旧Moments API）を使用して、リアルタイムの訪問プロファイルデータを取得します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/moments-api/
---
Context APIモジュール（旧Moments API）は、[Tealium Context APIサービス](https://docs.tealium.com/about-context-api/)との統合を提供します。これを使用して、パーソナライゼーションとインサイトのためのリアルタイムの訪問プロファイルデータを取得します。このモジュールは、構成されたContext APIエンジンからオーディエンス、バッジ、および属性を返します。

## インストール



`build.gradle`ファイルに`prism-moments-api`依存関係を追加します：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-moments-api")
```


リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用してSwift Package Manager依存関係として`TealiumPrismMomentsAPI`を追加するか、CocoaPodsのためにPodfileに追加します：

```ruby
pod 'tealium-prism'
```



## 初期化

`TealiumConfig`の`modules`リストにモジュールを追加します。


<blockquote>
Moments APIモジュールを初期化するには、地域を構成する必要があります。
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.momentsAPI {
            setRegion(MomentsApiRegion.UsEast)
        }
    )
).build()
```


```swift
let config = TealiumConfig(
    account: "ACCOUNT",
    profile: "PROFILE",
    environment: "prod",
    modules: [
        Modules.momentsAPI(forcingSettings: { builder in
            builder.setRegion(.usEast)
        }),
        // 他のモジュール...
    ]
)
```



## 訪問データの取得

エンジンIDを指定して`fetchEngineResponse()`を呼び出し、訪問プロファイルデータを取得します。このメソッドはリアクティブな`Single`を返し、結果を購読します。



```kotlin
tealium.momentsAPI().fetchEngineResponse("your-engine-id")
    .subscribe { result ->
        result.onSuccess { response ->
            println("Audiences: ${response.audiences}")
            println("Badges: ${response.badges}")
            println("Properties: ${response.properties}")
            println("Flags: ${response.flags}")
            println("Dates: ${response.dates}")
            println("Metrics: ${response.metrics}")
        }
        result.onFailure { error ->
            println("Failed to fetch engine response: $error")
        }
    }
```


```swift
tealium.momentsAPI().fetchEngineResponse(engineID: "your-engine-id").subscribe { result in
    switch result {
    case .success(let response):
        print("Audiences: \(response.audiences ?? [])")
        print("Badges: \(response.badges ?? [])")
        print("Properties: \(response.properties ?? [:])")
        print("Flags: \(response.flags ?? [:])")
        print("Dates: \(response.dates ?? [:])")
        print("Metrics: \(response.metrics ?? [:])")
    case .failure(let error):
        print("Failed to fetch engine response: \(error)")
    }
}
```



### 訪問属性

`EngineResponse`オブジェクトには、Context APIエンジンによって返される訪問属性が含まれています。

| 属性 | Kotlinの型 | Swiftの型 | 説明 |
|:---------|:------------|:-----------|:------------|
| `audiences` | `List<String>?` | `[String]?` | 訪問が割り当てられているオーディエンス。 |
| `badges` | `List<String>?` | `[String]?` | 訪問に割り当てられたバッジ。 |
| `flags` | `Map<String, Boolean>?` | `[String: Bool]?` | 訪問に割り当てられたブール属性。 |
| `dates` | `Map<String, Long>?` | `[String: Int64]?` | 訪問に割り当てられた日付属性（ミリ秒単位のUnixタイムスタンプ）。 |
| `metrics` | `Map<String, Double>?` | `[String: Double]?` | 訪問に割り当てられた数値属性。 |
| `properties` | `Map<String, String>?` | `[String: String]?` | 訪問に割り当てられた文字列属性。 |

## 構成

### 地域

[Context APIエンジンのエンドポイント](https://docs.tealium.com/context-api-endpoint/)に合わせて地域を構成します。

| Kotlin | Swift | 生の値 |
|:-------|:------|:----------|
| `MomentsApiRegion.Germany` | `.germany` | `eu-central-1` |
| `MomentsApiRegion.UsEast` | `.usEast` | `us-east-1` |
| `MomentsApiRegion.Sydney` | `.sydney` | `ap-southeast-2` |
| `MomentsApiRegion.Oregon` | `.oregon` | `us-west-2` |
| `MomentsApiRegion.Tokyo` | `.tokyo` | `ap-northeast-1` |
| `MomentsApiRegion.HongKong` | `.hongKong` | `ap-east-1` |



```kotlin
Modules.momentsAPI {
    setRegion(MomentsApiRegion.UsEast)
}
```


```swift
Modules.momentsAPI(forcingSettings: { builder in
    builder.setRegion(.usEast)
})
```



### リファラー

セキュリティをエンリッチメントするために、リファラーURLを構成します。リファラーURLは[ドメイン許可リスト](https://docs.tealium.com/about-context-api/#domain-allow-list)と一致する必要があります。そうでない場合、Moments APIはデータを返しません。

デフォルトのリファラーURLは以下の通りです：
```
https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html
```



```kotlin
Modules.momentsAPI {
    setReferrer("https://yourcustomreferrer.example.com")
}
```


```swift
Modules.momentsAPI(forcingSettings: { builder in
    builder.setReferrer("https://yourcustomreferrer.example.com")
})
```



## 構成ビルダーの参照



詳細については、[`MomentsApiSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/momentsapi/com.tealium.prism.momentsapi/-moments-api-settings-builder/)を参照してください。

| メソッド | 説明 |
|:-------|:------------|
| `setRegion(region: MomentsApiRegion)` | Moments APIエンジンの地域を構成します。必須。 |
| `setReferrer(referrer: String)` | Moments APIリクエストのリファラーURLを構成します。 |
| `setEnabled(enabled: Boolean)` | モジュールを永久に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールが初期化される順序を構成します。 |


詳細については、[`MomentsAPISettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismMomentsAPI/Classes/MomentsAPISettingsBuilder.html)を参照してください。

| メソッド | 説明 |
|:-------|:------------|
| `setRegion(_:)` | Moments APIエンジンの地域を構成します。必須。 |
| `setReferrer(_:)` | Moments APIリクエストのリファラーURLを構成します。 |
| `setEnabled(_:)` | モジュールを永久に有効または無効にします。 |
| `setOrder(_:)` | モジュールが初期化される順序を構成します。 |

