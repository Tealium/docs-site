---
title: Moments API
description: Learn how to implement the Moments API using Swift for iOS and Kotlin for Android.
url: https://docs.tealium.com/platforms/getting-started-mobile/moments-api/
---
The Moments API provides a unique endpoint that can be integrated into your mobile applications for personalized user experiences. This guide covers the steps to implement the Moments API using Swift for iOS and Kotlin for Android.

## Supported Platforms

- [Tealium for Android](/platforms/android-kotlin/module-list/moments-api/)
- [Tealium for iOS](/platforms/ios-swift/module-list/moments-api/)

## Prerequisites

Before you begin, ensure that you have the following:

- A Tealium account with access to the Moments API.

## How it Works

The Moments API retrieves visitor data from AudienceStream, which can be used for in-app personalization.

## Use Cases

### In-App Personalization

Fetch updated visitor information whenever required to power personalized content within your app.

### Pass Consented Visitor Data To Other SDKs

Pass specific attributes from the visitor profile to other SDKs present in your app, which can be used to enable personalized messaging, or to run A/B tests for particular user segments.

## Initialization

### Step 1: Initialize Tealium with Moments API Module




```swift
import TealiumCore
import TealiumMomentsAPI

let config = TealiumConfig(account: &#34;your_account&#34;,
                           profile: &#34;your_profile&#34;,
                           environment: &#34;dev&#34;,
                           modules: [Collectors.MomentsAPI])

let tealium = Tealium(config: config)
```




```kotlin
import com.tealium.core.Tealium
import com.tealium.core.TealiumConfig
import com.tealium.core.Environment
import com.tealium.core.modules

val config = TealiumConfig(application, 
                           &#34;your_account&#34;,
                           &#34;your_profile&#34;,
                           Environment.DEV, 
                           modules = mutableSetOf(Modules.MomentsApi))

val tealium = Tealium.create(&#34;your_instance_name&#34;, config)
```




### Step 2: Set the Moments API Region

Set the `momentsAPIRegion` property to the region where your AudienceStream profile resides. This must match exactly. If unsure, check with your account manager.




```swift
config.momentsAPIRegion = .us_east // Example region
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // Example region
```




 The `Custom` option is for future use and should not be used without explicit instructions from your Tealium Account Manager. 




```swift
config.momentsAPIRegion = .custom(&#34;custom_region_placeholder&#34;)
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom(&#34;custom_region_placeholder&#34;)
```




The following table shows the available regions:

| Swift | Kotlin | Underlying value       |
|-----------------|---------------------|-----------------|
| germany         | MomentsApiRegion.Germany             | eu-central-1    |
| us_east         | MomentsApiRegion.UsEast              | us-east-1       |
| sydney          | MomentsApiRegion.Sydney              | ap-southeast-2  |
| oregon          | MomentsApiRegion.Oregon              | us-west-2       |
| tokyo           | MomentsApiRegion.Tokyo               | ap-northeast-1  |
| hong_kong       | MomentsApiRegion.HongKong            | ap-east-1       |
| custom          | MomentsApiRegion.Custom              | Custom String   |



### Step 3: Set the Referrer for Added Security

The referrer option can be used for added security. It must match the &#34;Domain Allow List&#34; in the Tealium UI.




```swift
config.momentsAPIReferrer = &#34;https://your.custom.referrer.url&#34;
```




```kotlin
config.momentsApiReferrer = &#34;https://your.custom.referrer.url&#34;
```




### Step 4: Fetch Engine Response

Implement a function to fetch the Moments API engine response. Call this method any time you need to retrieve the latest information about the app user.

The Tealium Visitor ID of the current app user is automatically sent as part of the Moments API request.




```swift
import TealiumMomentsAPI

func fetchMoments(engineId: String, completion: @escaping (Result&lt;EngineResponse, Error&gt;) -&gt; Void) {
    tealium?.momentsAPI?.fetchEngineResponse(
        engineID: engineId,
        completion: { engineResponse in
            switch engineResponse {
            case .success(let response):
                print(&#34;String attributes: \(response.strings ?? [])&#34;)
                print(&#34;Boolean attributes: \(response.booleans ?? [])&#34;)
                print(&#34;Audiences: \(response.audiences ?? [])&#34;)
                print(&#34;Date attributes: \(response.dates ?? [:])&#34;)
                print(&#34;Badges: \(response.badges ?? [])&#34;)
                print(&#34;Numbers: \(response.numbers ?? [:])&#34;)
            case .failure(let error):
                print(&#34;Error fetching moments: \(error.localizedDescription)&#34;)
            }
            completion(engineResponse)
        }
    )
}
```




```kotlin
import android.util.Log
import com.tealium.momentsapi.EngineResponse
import com.tealium.momentsapi.ErrorCode
import com.tealium.momentsapi.ResponseListener
import com.tealium.core.Tealium

fun fetchMoments(engineId: String, responseListener: ResponseListener&lt;EngineResponse&gt;) {
    val tealiumInstance = Tealium[&#34;your_instance_name&#34;]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, object : ResponseListener&lt;EngineResponse&gt; {
        override fun success(data: EngineResponse) {
            Log.d(&#34;MomentsAPI&#34;, &#34;String attributes: ${data.strings}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Boolean attributes: ${data.booleans}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Audiences: ${data.audiences}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Date attributes: ${data.dates}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Badges: ${data.badges}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Numbers: ${data.numbers}&#34;)

            responseListener.success(data)
        }

        override fun failure(errorCode: ErrorCode, message: String) {
            Log.e(&#34;MomentsAPI&#34;, &#34;Error fetching moments: $errorCode - $message&#34;)
            responseListener.failure(errorCode, message)
        }
    })
}
```


