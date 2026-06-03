---
title: モーメンツAPI
description: Swiftを使用したiOSとKotlinを使用したAndroidでモーメンツAPIを実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/moments-api/
---
モーメンツAPIは、パーソナライズされたユーザーエクスペリエンスのためにモバイルアプリケーションに統合できるユニークなエンドポイントを提供します。このガイドでは、Swiftを使用したiOSとKotlinを使用したAndroidでモーメンツAPIを実装する手順を説明します。

## サポートされているプラットフォーム

- [Tealium for Android](/ja/platforms/android-kotlin/module-list/moments-api/)
- [Tealium for iOS](/ja/platforms/ios-swift/module-list/moments-api/)

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




### ステップ2：モーメンツAPIリージョンを構成する

`momentsAPIRegion`プロパティを、AudienceStreamプロファイルが存在するリージョンに構成します。これは正確に一致する必要があります。不確かな場合は、アカウントマネージャーに確認してください。




```swift
config.momentsAPIRegion = .us_east // 例のリージョン
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast // 例のリージョン
```




 `Custom`オプションは将来の使用のためのものであり、Tealiumアカウントマネージャーから明示的な指示がない限り使用しないでください。 




```swift
config.momentsAPIRegion = .custom(&#34;custom_region_placeholder&#34;)
```




```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom(&#34;custom_region_placeholder&#34;)
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
config.momentsAPIReferrer = &#34;https://your.custom.referrer.url&#34;
```




```kotlin
config.momentsApiReferrer = &#34;https://your.custom.referrer.url&#34;
```




### ステップ4：エンジンレスポンスを取得する

モーメンツAPIエンジンレスポンスを取得する関数を実装します。このメソッドは、アプリユーザーに関する最新情報を取得する必要があるたびに呼び出します。

現在のアプリユーザーのTealium訪問IDは、モーメンツAPIリクエストの一部として自動的に送信されます。




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


