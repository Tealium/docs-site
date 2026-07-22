---
title: Moments API
description: Learn how to implement the Moments API using Swift for iOS and Kotlin for Android.
url: https://docs.tealium.com/platforms/getting-started-mobile/moments-api/
---
The Moments API provides a unique endpoint that can be integrated into your mobile applications for personalized user experiences. This guide covers the steps to implement the Moments API using Swift for iOS and Kotlin for Android.

## Supported Platforms

- [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/module-list/moments-api/)
- [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/module-list/moments-api/)

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

let config = TealiumConfig(account: "your_account",
                           profile: "your_profile",
                           environment: "dev",
                           modules: [Collectors.MomentsAPI])

let tealium = Tealium(config: config)
```




```kotlin
import com.tealium.core.Tealium
import com.tealium.core.TealiumConfig
import com.tealium.core.Environment
import com.tealium.core.modules

val config = TealiumConfig(application, 
                           "your_account",
                           "your_profile",
                           Environment.DEV, 
                           modules = mutableSetOf(Modules.MomentsApi))

val tealium = Tealium.create("your_instance_name", config)
```




### Step 2: Set the Moments API Region

Set the `momentsAPIRegion` property to the region where your AudienceStream profile resides. This must match exactly. If unsure, check with your account manager.




```swift
config.momentsAPIRegion = .us_east // Example region
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // Example region
```





<blockquote>
The `Custom` option is for future use and should not be used without explicit instructions from your Tealium Account Manager.
</blockquote>





```swift
config.momentsAPIRegion = .custom("custom_region_placeholder")
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
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

The referrer option can be used for added security. It must match the "Domain Allow List" in the Tealium UI.




```swift
config.momentsAPIReferrer = "https://your.custom.referrer.url"
```




```kotlin
config.momentsApiReferrer = "https://your.custom.referrer.url"
```




### Step 4: Fetch Engine Response

Implement a function to fetch the Moments API engine response. Call this method any time you need to retrieve the latest information about the app user.


<blockquote>
The Tealium Visitor ID of the current app user is automatically sent as part of the Moments API request.
</blockquote>





```swift
import TealiumMomentsAPI

func fetchMoments(engineId: String, completion: @escaping (Result<EngineResponse, Error>) -> Void) {
    tealium?.momentsAPI?.fetchEngineResponse(
        engineID: engineId,
        completion: { engineResponse in
            switch engineResponse {
            case .success(let response):
                print("String attributes: \(response.strings ?? [])")
                print("Boolean attributes: \(response.booleans ?? [])")
                print("Audiences: \(response.audiences ?? [])")
                print("Date attributes: \(response.dates ?? [:])")
                print("Badges: \(response.badges ?? [])")
                print("Numbers: \(response.numbers ?? [:])")
            case .failure(let error):
                print("Error fetching moments: \(error.localizedDescription)")
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

fun fetchMoments(engineId: String, responseListener: ResponseListener<EngineResponse>) {
    val tealiumInstance = Tealium["your_instance_name"]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, object : ResponseListener<EngineResponse> {
        override fun success(data: EngineResponse) {
            Log.d("MomentsAPI", "String attributes: ${data.strings}")
            Log.d("MomentsAPI", "Boolean attributes: ${data.booleans}")
            Log.d("MomentsAPI", "Audiences: ${data.audiences}")
            Log.d("MomentsAPI", "Date attributes: ${data.dates}")
            Log.d("MomentsAPI", "Badges: ${data.badges}")
            Log.d("MomentsAPI", "Numbers: ${data.numbers}")

            responseListener.success(data)
        }

        override fun failure(errorCode: ErrorCode, message: String) {
            Log.e("MomentsAPI", "Error fetching moments: $errorCode - $message")
            responseListener.failure(errorCode, message)
        }
    })
}
```


