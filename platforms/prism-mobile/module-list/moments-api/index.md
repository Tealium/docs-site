---
title: Context API module
description: Retrieve real-time visitor profile data using the Context API module (formerly Moments API) in the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/
---
The Context API module (formerly Moments API) provides integration with the [Tealium Context API service](https://docs.tealium.com/about-context-api/). Use it to retrieve real-time visitor profile data for personalization and insights. The module returns audiences, badges, and attributes from configured Context API engines.

## Install



Add the `prism-moments-api` dependency to your `build.gradle` file:

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-moments-api")
```


Add `TealiumPrismMomentsAPI` as a Swift Package Manager dependency using the repository URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism'
```



## Initialize

Add the module to the `modules` list in `TealiumConfig`.


<blockquote>
A region must be set for the Moments API module to initialize.
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
        // other modules...
    ]
)
```



## Get visitor data

Call `fetchEngineResponse()` with your engine ID to retrieve visitor profile data. The method returns a reactive `Single` that you subscribe to for the result.



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



### Visitor attributes

The `EngineResponse` object contains the visitor attributes returned by the Context API engine.

| Property | Kotlin type | Swift type | Description |
|:---------|:------------|:-----------|:------------|
| `audiences` | `List<String>?` | `[String]?` | The audiences the visitor is assigned to. |
| `badges` | `List<String>?` | `[String]?` | The badges assigned to the visitor. |
| `flags` | `Map<String, Boolean>?` | `[String: Bool]?` | Boolean attributes assigned to the visitor. |
| `dates` | `Map<String, Long>?` | `[String: Int64]?` | Date attributes assigned to the visitor (millisecond-precise Unix timestamps). |
| `metrics` | `Map<String, Double>?` | `[String: Double]?` | Number attributes assigned to the visitor. |
| `properties` | `Map<String, String>?` | `[String: String]?` | String attributes assigned to the visitor. |

## Configuration

### Region

Configure the region that matches the [endpoint of your Context API engine](https://docs.tealium.com/context-api-endpoint/).

| Kotlin | Swift | Raw value |
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



### Referrer

For added security, set a referrer URL. The referrer URL must match the [domain allow list](https://docs.tealium.com/about-context-api/#domain-allow-list), or the Moments API does not return data.

The default referrer URL is:
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



## Settings builder reference



For more information, see [`MomentsApiSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/momentsapi/com.tealium.prism.momentsapi/-moments-api-settings-builder/).

| Method | Description |
|:-------|:------------|
| `setRegion(region: MomentsApiRegion)` | Sets the region for the Moments API engine. Required. |
| `setReferrer(referrer: String)` | Sets the referrer URL for Moments API requests. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |


For more information, see [`MomentsAPISettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismMomentsAPI/Classes/MomentsAPISettingsBuilder.html).

| Method | Description |
|:-------|:------------|
| `setRegion(_:)` | Sets the region for the Moments API engine. Required. |
| `setReferrer(_:)` | Sets the referrer URL for Moments API requests. |
| `setEnabled(_:)` | Permanently enables or disables the module. |
| `setOrder(_:)` | Sets the order in which the module is initialized. |


