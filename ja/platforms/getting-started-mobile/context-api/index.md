---
title: Context API（現在はContext API）
description: iOS向けのSwiftとAndroid向けのKotlinを使用してContext APIを実装する方法について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/context-api/
---

<blockquote>
Moments APIはContext APIに名称変更されました。製品ドキュメント全体については、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。
</blockquote>


Context APIは、パーソナライズされたユーザーエクスペリエンスを実現するためにモバイルアプリケーションへ統合できる、一意のエンドポイントを提供します。このガイドでは、iOS向けのSwiftとAndroid向けのKotlinを使用してContext APIを実装する手順について説明します。

## サポート対象プラットフォーム

- [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/context-api/)
- [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/module-list/context-api/)

## 前提条件

開始する前に、以下が用意されていることを確認してください。

- Context APIにアクセスできるTealiumアカウント。

## 仕組み

Context APIは、Customer Data Platform（CDP）から訪問データを取得します。このデータは、アプリ内のパーソナライゼーションに使用できます。

## ユースケース

### アプリ内パーソナライゼーション

必要に応じて最新の訪問情報を取得し、アプリ内でパーソナライズされたコンテンツを提供します。

### 同意を得た訪問データを他のSDKに渡す

訪問プロファイルの特定の属性を、アプリ内に存在する他のSDKに渡します。この属性を使用して、パーソナライズされたメッセージを有効にしたり、特定のユーザーセグメントを対象にA/Bテストを実行したりできます。

## 初期化

### ステップ1：Context APIモジュールを使用してTealiumを初期化する




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




### ステップ2：Context APIのリージョンを構成する

`momentsAPIRegion`プロパティを、CDPプロファイルが配置されているリージョンに構成します。この値は完全に一致している必要があります。不明な場合は、アカウントマネージャーに確認してください。




```swift
config.momentsAPIRegion = .us_east // Example region
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // Example region
```





<blockquote>
`Custom`オプションは将来使用するためのものであり、Tealiumアカウントマネージャーから明示的な指示がない限り使用しないでください。
</blockquote>





```swift
config.momentsAPIRegion = .custom("custom_region_placeholder")
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```




利用可能なリージョンを次の表に示します。

| Swift | Kotlin | 基になる値 |
|-----------------|---------------------|-----------------|
| germany         | MomentsApiRegion.Germany             | eu-central-1    |
| us_east         | MomentsApiRegion.UsEast              | us-east-1       |
| sydney          | MomentsApiRegion.Sydney              | ap-southeast-2  |
| oregon          | MomentsApiRegion.Oregon              | us-west-2       |
| tokyo           | MomentsApiRegion.Tokyo               | ap-northeast-1  |
| hong_kong       | MomentsApiRegion.HongKong            | ap-east-1       |
| custom          | MomentsApiRegion.Custom              | カスタム文字列  |

### ステップ3：セキュリティをエンリッチメントするためにリファラーを構成する

リファラーオプションを使用すると、セキュリティをエンリッチメントできます。この値は、Tealium UIの「Domain Allow List」と一致している必要があります。




```swift
config.momentsAPIReferrer = "https://your.custom.referrer.url"
```




```kotlin
config.momentsApiReferrer = "https://your.custom.referrer.url"
```




### ステップ4：エンジンレスポンスを取得する

Context APIのエンジンレスポンスを取得する関数を実装します。アプリユーザーに関する最新情報を取得する必要があるときは、いつでもこのメソッドを呼び出してください。


<blockquote>
現在のアプリユーザーのTealium Visitor IDは、Context APIリクエストの一部として自動的に送信されます。
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


