---
title: Moments API（現在はContext API）
description: Swift（iOS用）とKotlin（Android用）を使用してContext APIを実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/context-api/
---

<blockquote>
Moments APIはContext APIに名称が変更されました。製品の完全なドキュメントについては、[Context APIについて](https://docs.tealium.com/about-context-api/)をご覧ください。
</blockquote>


Context APIは、モバイルアプリケーションに統合できるユニークなエンドポイントを提供し、パーソナライズされたユーザーエクスペリエンスを実現します。このガイドでは、Swift（iOS用）とKotlin（Android用）を使用してContext APIを実装する手順を説明します。

## 対応プラットフォーム

- [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/context-api/)
- [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/module-list/context-api/)

## 前提条件

開始する前に、以下のものを用意してください：

- Context APIにアクセスできるTealiumアカウント。

## 動作原理

Context APIはAudienceStreamから訪問データを取得し、アプリ内パーソナライゼーションに使用できます。

## ユースケース

### アプリ内パーソナライゼーション

必要に応じて訪問情報を更新して取得し、アプリ内のパーソナライズされたコンテンツを提供します。

### 同意された訪問データを他のSDKに渡す

訪問プロファイルから特定の属性をアプリ内の他のSDKに渡し、パーソナライズされたメッセージングを有効にするか、特定のユーザーセグメントのA/Bテストを実行するのに使用できます。

## 初期化

### ステップ1: Context APIモジュールでTealiumを初期化




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




### ステップ2: Context APIリージョンを構成

`momentsAPIRegion`プロパティを構成して、AudienceStreamプロファイルが存在するリージョンを指定します。確実に一致させる必要があります。不明な場合はアカウントマネージャーに確認してください。




```swift
config.momentsAPIRegion = .us_east // 例：リージョン
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // 例：リージョン
```





<blockquote>
`Custom`オプションは将来の使用のためのものであり、Tealiumアカウントマネージャーから明確な指示がない限り使用しないでください。
</blockquote>





```swift
config.momentsAPIRegion = .custom("custom_region_placeholder")
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```




利用可能なリージョンの表は以下の通りです：

| Swift | Kotlin | Underlying value       |
|-----------------|---------------------|-----------------|
| germany         | MomentsApiRegion.Germany             | eu-central-1    |
| us_east         | MomentsApiRegion.UsEast              | us-east-1       |
| sydney          | MomentsApiRegion.Sydney              | ap-southeast-2  |
| oregon          | MomentsApiRegion.Oregon              | us-west-2       |
| tokyo           | MomentsApiRegion.Tokyo               | ap-northeast-1  |
| hong_kong       | MomentsApiRegion.HongKong            | ap-east-1       |
| custom          | MomentsApiRegion.Custom              | Custom String   |


### ステップ3: 追加のセキュリティのためにリファラーを構成

リファラーオプションは追加のセキュリティのために使用できます。Tealium UIの「ドメイン許可リスト」と一致する必要があります。




```swift
config.momentsAPIReferrer = "https://your.custom.referrer.url"
```




```kotlin
config.momentsApiReferrer = "https://your.custom.referrer.url"
```




### ステップ4: エンジンレスポンスを取得

アプリユーザーに関する最新情報を取得するために、Context APIエンジンレスポンスを取得する関数を実装します。このメソッドを必要な時に呼び出します。


<blockquote>
現在のアプリユーザーのTealium訪問IDは、Context APIリクエストの一部として自動的に送信されます。
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


