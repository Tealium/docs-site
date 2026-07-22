---
title: モーメンツAPI
description: Swiftを使用したiOSとKotlinを使用したAndroidでモーメンツAPIを実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/moments-api/
---
モーメンツAPIは、パーソナライズされたユーザーエクスペリエンスのためにモバイルアプリケーションに統合できるユニークなエンドポイントを提供します。このガイドでは、Swiftを使用したiOSとKotlinを使用したAndroidでモーメンツAPIを実装する手順を説明します。

## サポートされているプラットフォーム

- [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/moments-api/)
- [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/module-list/moments-api/)

## 前提条件

開始する前に、以下を確認してください：

- モーメンツAPIへのアクセス権を持つTealiumアカウント。

## 仕組み

モーメンツAPIは、AudienceStreamから訪問データを取得し、アプリ内のパーソナライゼーションに使用できます。

## ユースケース

### アプリ内パーソナライゼーション

必要に応じて訪問情報を更新し、アプリ内のパーソナライズされたコンテンツをエンリッチメントします。

### 同意した訪問データを他のSDKに渡す

訪問プロファイルから特定の属性を他のアプリ内のSDKに渡し、パーソナライズされたメッセージングを有効にするか、特定のユーザーセグメントのA/Bテストを実行するために使用できます。

## 初期化

### ステップ1：モーメンツAPIモジュールでTealiumを初期化する




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




### ステップ2：モーメンツAPIリージョンを構成する

`momentsAPIRegion`プロパティを、AudienceStreamプロファイルが存在するリージョンに構成します。これは正確に一致する必要があります。不確かな場合は、アカウントマネージャーに確認してください。




```swift
config.momentsAPIRegion = .us_east // 例のリージョン
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // 例のリージョン
```





<blockquote>
`Custom`オプションは将来の使用のためのものであり、Tealiumアカウントマネージャーから明示的な指示がない限り使用しないでください。
</blockquote>





```swift
config.momentsAPIRegion = .custom("custom_region_placeholder")
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```




以下の表は、利用可能なリージョンを示しています：

| Swift | Kotlin | Underlying value       |
|-----------------|---------------------|-----------------|
| germany         | MomentsApiRegion.Germany             | eu-central-1    |
| us_east         | MomentsApiRegion.UsEast              | us-east-1       |
| sydney          | MomentsApiRegion.Sydney              | ap-southeast-2  |
| oregon          | MomentsApiRegion.Oregon              | us-west-2       |
| tokyo           | MomentsApiRegion.Tokyo               | ap-northeast-1  |
| hong_kong       | MomentsApiRegion.HongKong            | ap-east-1       |
| custom          | MomentsApiRegion.Custom              | Custom String   |



### ステップ3：セキュリティエンリッチメントのためのリファラーを構成する

リファラーオプションは、セキュリティをエンリッチメントするために使用できます。これはTealium UIの「ドメイン許可リスト」に一致する必要があります。




```swift
config.momentsAPIReferrer = "https://your.custom.referrer.url"
```




```kotlin
config.momentsApiReferrer = "https://your.custom.referrer.url"
```




### ステップ4：エンジンレスポンスを取得する

モーメンツAPIエンジンレスポンスを取得する関数を実装します。このメソッドは、アプリユーザーに関する最新情報を取得する必要があるたびに呼び出します。


<blockquote>
現在のアプリユーザーのTealium訪問IDは、モーメンツAPIリクエストの一部として自動的に送信されます。
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


