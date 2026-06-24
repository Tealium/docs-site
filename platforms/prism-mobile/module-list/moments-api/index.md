---
title: Moments API module
description: Use the Moments API module to retrieve real-time visitor profile data.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/
---
The Moments API module provides integration with the [Tealium Moments API service](). Use it to retrieve real-time visitor profile data for personalization and insights. The module enables high-performance, customizable data retrieval for real-time visitor personalization use cases, including audiences, badges, and attributes from configured Moments API engines.

## Install



Add the `prism-moments-api` dependency to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-moments-api&#34;)
```


Add `TealiumPrismMomentsAPI` as a Swift Package Manager dependency using the repository URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism&#39;
```



## Initialize

Add the module to the `modules` list in `TealiumConfig`.

A region must be set for the Moments API module to initialize.



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;ACCOUNT&#34;,
    profileName = &#34;PROFILE&#34;,
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
    account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;prod&#34;,
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
tealium.momentsAPI().fetchEngineResponse(&#34;your-engine-id&#34;)
    .subscribe { result -&gt;
        result.onSuccess { response -&gt;
            println(&#34;Audiences: ${response.audiences}&#34;)
            println(&#34;Badges: ${response.badges}&#34;)
            println(&#34;Properties: ${response.properties}&#34;)
            println(&#34;Flags: ${response.flags}&#34;)
            println(&#34;Dates: ${response.dates}&#34;)
            println(&#34;Metrics: ${response.metrics}&#34;)
        }
        result.onFailure { error -&gt;
            println(&#34;Failed to fetch engine response: $error&#34;)
        }
    }
```


```swift
tealium.momentsAPI().fetchEngineResponse(engineID: &#34;your-engine-id&#34;).subscribe { result in
    switch result {
    case .success(let response):
        print(&#34;Audiences: \(response.audiences ?? [])&#34;)
        print(&#34;Badges: \(response.badges ?? [])&#34;)
        print(&#34;Properties: \(response.properties ?? [:])&#34;)
        print(&#34;Flags: \(response.flags ?? [:])&#34;)
        print(&#34;Dates: \(response.dates ?? [:])&#34;)
        print(&#34;Metrics: \(response.metrics ?? [:])&#34;)
    case .failure(let error):
        print(&#34;Failed to fetch engine response: \(error)&#34;)
    }
}
```



### Visitor attributes

The `EngineResponse` object contains the visitor attributes returned by the Moments API engine.

| Property | Kotlin type | Swift type | Description |
|:---------|:------------|:-----------|:------------|
| `audiences` | `List&lt;String&gt;?` | `[String]?` | The audiences the visitor is assigned to. |
| `badges` | `List&lt;String&gt;?` | `[String]?` | The badges assigned to the visitor. |
| `flags` | `Map&lt;String, Boolean&gt;?` | `[String: Bool]?` | Boolean attributes assigned to the visitor. |
| `dates` | `Map&lt;String, Long&gt;?` | `[String: Int64]?` | Date attributes assigned to the visitor (millisecond-precise Unix timestamps). |
| `metrics` | `Map&lt;String, Double&gt;?` | `[String: Double]?` | Number attributes assigned to the visitor. |
| `properties` | `Map&lt;String, String&gt;?` | `[String: String]?` | String attributes assigned to the visitor. |

## Configuration

### Region

Configure the region that matches the [endpoint of your Moments API engine]().

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

For added security, set a referrer URL. The referrer URL must match the [domain allow list](), or the Moments API does not return data.

The default referrer URL is:
```
https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html
```



```kotlin
Modules.momentsAPI {
    setReferrer(&#34;https://yourcustomreferrer.example.com&#34;)
}
```


```swift
Modules.momentsAPI(forcingSettings: { builder in
    builder.setReferrer(&#34;https://yourcustomreferrer.example.com&#34;)
})
```



## Settings builder reference



For more information, see [`MomentsApiSettingsBuilder`](/tealium-prism-kotlin/momentsapi/com.tealium.prism.momentsapi/-moments-api-settings-builder/).

| Method | Description |
|:-------|:------------|
| `setRegion(region: MomentsApiRegion)` | Sets the region for the Moments API engine. Required. |
| `setReferrer(referrer: String)` | Sets the referrer URL for Moments API requests. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |


For more information, see [`MomentsAPISettingsBuilder`](/tealium-prism-swift/TealiumPrismMomentsAPI/Classes/MomentsAPISettingsBuilder.html).

| Method | Description |
|:-------|:------------|
| `setRegion(_:)` | Sets the region for the Moments API engine. Required. |
| `setReferrer(_:)` | Sets the referrer URL for Moments API requests. |
| `setEnabled(_:)` | Permanently enables or disables the module. |
| `setOrder(_:)` | Sets the order in which the module is initialized. |


