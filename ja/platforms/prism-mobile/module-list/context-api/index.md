---
title: Context API モジュール
description: Tealium Prism SDK の Context API モジュール（旧 Moments API）を使用して、リアルタイムの訪問プロファイルデータを取得します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/context-api/
---
Context API モジュール（旧 Moments API）は、[Tealium Context API サービス](https://docs.tealium.com/about-context-api/)との統合を提供します。パーソナライゼーションや分析情報の取得に使用するリアルタイムの訪問プロファイルデータを取得できます。このモジュールは、構成済みの Context API エンジンからオーディエンス、バッジ、属性を返します。

## インストール



`build.gradle` ファイルに `prism-context-api` 依存関係を追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-context-api")
```


リポジトリ URL `https://github.com/Tealium/tealium-prism-swift` を使用して、`TealiumPrismContextAPI` を Swift Package Manager の依存関係として追加するか、CocoaPods 用の Podfile に追加します。

```ruby
pod 'tealium-prism'
```



## 初期化

`TealiumConfig` の `modules` リストにモジュールを追加します。


<blockquote>
Moments API モジュールを初期化するには、リージョンを構成する必要があります。
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.contextApi {
            it.setRegion(ContextApiRegion.UsEast)
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
        Modules.contextAPI(forcingSettings: { builder in
            builder.setRegion(.usEast)
        }),
        // other modules...
    ]
)
```



## 訪問データの取得

エンジン ID を指定して `fetchEngineResponse()` を呼び出し、訪問プロファイルデータを取得します。このメソッドはリアクティブな `Single` を返します。これをサブスクライブして結果を取得します。



```kotlin
tealium.contextApi.fetchEngineResponse("your-engine-id")
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
tealium.contextAPI().fetchEngineResponse(engineID: "your-engine-id").subscribe { result in
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

`EngineResponse` オブジェクトには、Context API エンジンから返された訪問属性が含まれます。

| プロパティ | Kotlin の型 | Swift の型 | 説明 |
|:---------|:------------|:-----------|:------------|
| `audiences` | `List<String>?` | `[String]?` | 訪問が割り当てられているオーディエンス。 |
| `badges` | `List<String>?` | `[String]?` | 訪問に割り当てられているバッジ。 |
| `flags` | `Map<String, Boolean>?` | `[String: Bool]?` | 訪問に割り当てられているブール属性。 |
| `dates` | `Map<String, Long>?` | `[String: Int64]?` | 訪問に割り当てられている日付属性（ミリ秒精度の Unix タイムスタンプ）。 |
| `metrics` | `Map<String, Double>?` | `[String: Double]?` | 訪問に割り当てられている数値属性。 |
| `properties` | `Map<String, String>?` | `[String: String]?` | 訪問に割り当てられている文字列属性。 |

## 構成

### リージョン

[Context API エンジンのエンドポイント](https://docs.tealium.com/context-api-endpoint/)と一致するリージョンを構成します。

| Kotlin | Swift | 生の値 |
|:-------|:------|:----------|
| `ContextApiRegion.Germany` | `.germany` | `eu-central-1` |
| `ContextApiRegion.UsEast` | `.usEast` | `us-east-1` |
| `ContextApiRegion.Sydney` | `.sydney` | `ap-southeast-2` |
| `ContextApiRegion.Oregon` | `.oregon` | `us-west-2` |
| `ContextApiRegion.Tokyo` | `.tokyo` | `ap-northeast-1` |
| `ContextApiRegion.HongKong` | `.hongKong` | `ap-east-1` |



```kotlin
Modules.contextApi {
    it.setRegion(ContextApiRegion.UsEast)
}
```


```swift
Modules.contextAPI(forcingSettings: { builder in
    builder.setRegion(.usEast)
})
```



### リファラー

セキュリティをエンリッチメントするには、リファラー URL を構成します。リファラー URL は[ドメイン許可リスト](https://docs.tealium.com/about-context-api/#domain-allow-list)と一致している必要があります。一致しない場合、Moments API はデータを返しません。

デフォルトのリファラー URL は次のとおりです。
```
https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html
```



```kotlin
Modules.contextApi {
    it.setReferrer("https://yourcustomreferrer.example.com")
}
```


```swift
Modules.contextAPI(forcingSettings: { builder in
    builder.setReferrer("https://yourcustomreferrer.example.com")
})
```



## 構成ビルダーのリファレンス



詳細については、[`ContextApiSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/contextapi/com.tealium.prism.contextapi/-context-api-settings-builder/index.html)を参照してください。

| メソッド | 説明 |
|:-------|:------------|
| `setRegion(region: ContextApiRegion)` | Moments API エンジンのリージョンを構成します。必須です。 |
| `setReferrer(referrer: String)` | Moments API リクエストのリファラー URL を構成します。 |
| `setEnabled(enabled: Boolean)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールを初期化する順序を構成します。 |


詳細については、[`ContextAPISettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismContextAPI/Classes/ContextAPISettingsBuilder.html)を参照してください。

| メソッド | 説明 |
|:-------|:------------|
| `setRegion(_:)` | Moments API エンジンのリージョンを構成します。必須です。 |
| `setReferrer(_:)` | Moments API リクエストのリファラー URL を構成します。 |
| `setEnabled(_:)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(_:)` | モジュールを初期化する順序を構成します。 |

