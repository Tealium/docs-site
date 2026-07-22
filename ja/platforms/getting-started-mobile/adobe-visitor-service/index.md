---
title: Adobe Visitor Service モジュール
description: Adobe Visitor Service モジュールについて学びましょう。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/adobe-visitor-service/
---
Adobe Visitor Service モジュールは、訪問のExperience Cloud ID（ECID）を取得および維持するために、AdobeのREST APIと直接連携します。ECIDは、Adobe TargetやAdobe Analyticsなど、Adobeエコシステムの異なる部分で同じ訪問を識別し、ユニークな訪問を識別します。

AdobeのトラッキングSDKからTealium SDKへの移行を行う場合は、トラッキングペイロードでECIDを渡すためにAdobe Visitor Serviceモジュールを使用します。データレイヤーの新しいECIDは、Tealium EventStreamまたはTealium AudienceStreamのサーバーサイドAdobeコネクタでマッピングされる場合があります。Adobe Visitor Serviceモジュールは、既存のECIDが存在する場合はそれを再利用し、存在しない場合は新しいものを生成することで、アプリ内の訪問数を正確にカウントするためのシームレスな移行を提供します。

## 対応プラットフォーム

以下のプラットフォームがAdobe Visitor Serviceモジュールをサポートしています：

- [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/adobe-visitor-service/)
- [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/module-list/adobe-visitor-service/)
- [Tealium for React Native](https://docs.tealium.com/ja/platforms/react-native/adobe-visitor-service/)
- [Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/adobe-visitor-service/)

## ユースケース

### サーバーサイドアナリティクスへの移行

Adobeの統合をサーバーサイドに移行し、EventStreamを通じてAdobe Analyticsサーバーサイドで`marketingCloudVisitorID`パラメータにECIDをマッピングします。複数のAdobe製品が連携して動作するためには有効なECIDが必要です。Tealium SDKは、EventStreamへの呼び出しを行う前にAdobeからECIDを要求し、Adobe Analyticsコネクタの`marketingCloudVisitorID`プロパティにECIDをマッピングします。

### Tealium iQタグ管理

Adobe Analyticsタグを使用する際には、Tealium iQタグ管理を使用してECIDを生成することをお勧めします。これにより、ECIDがすぐに利用可能であり、保存に保存され、隠れたウェブビューのクッキーストアに依存しないことが保証されます。

### Adobe SDKからTealium SDKへの移行

Adobe SDKからTealiumモジュールへの移行はシームレスです。現在、アプリがAdobe SDKを使用してECIDを管理している場合は、Tealium SDKとともにアプリ内にAdobe SDKが存在する移行期間を設けることをお勧めします。訪問が既存のAdobe ECIDを持っている場合は、`config.adobeVisitorExistingEcid`プロパティを通じてTealiumモジュールに渡します。このプロパティが初期化時に構成されている場合は、既存のECIDが使用されます。構成されていない場合は、TealiumモジュールがAdobe APIから新しいものを取得します。

### 同じデバイス上の異なる訪問の追跡

アプリ内で異なる訪問アカウントを検出した場合は、`tealium.adobeVisitor?.resetVisitor()`を呼び出してECIDをリセットし、各訪問が別々に追跡されるようにします。これにより、現在のECIDがリセットされ、新しいものがAdobe APIから自動的に要求されます。

### 既知の訪問IDと認証状態の構成

`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、および`adobeVisitorAuthState`の構成プロパティは、アプリセッションの開始時にすべての値が既知の場合にのみ使用します。`adobeVisitorAuthState`は、`adobeVisitorCustomVisitorId`も構成する場合にのみ構成します。

訪問のIDが初期化時に未知の場合（例えば、ユーザーがログインする前など）、これらのプロパティを省略し、IDが利用可能になったら`linkEcidToKnownIdentifier`を呼び出します。

すべての値が初期化時に既知の場合は、モジュールの開始時に`TealiumConfig`オブジェクトにそれらを構成します：




```kotlin
config.adobeVisitorDataProviderId = "01" // このタイプの訪問IDのデータプロバイダーID
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```swift
config.adobeVisitorDataProviderId = "01" // このタイプの訪問IDのデータプロバイダーID
config.adobeVisitorAuthState = .authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```javascript
config.adobeVisitorDataProviderId = "01" // このタイプの訪問IDのデータプロバイダーID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```dart
config.adobeVisitorDataProviderId = "01" // このタイプの訪問IDのデータプロバイダーID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




モジュールは必要に応じて新しいIDを自動的に要求し、その後、`TealiumConfig`プロパティで提供された既知のIDにECIDをリンクするために追加のAPI呼び出しを送信します。

訪問がログインする際にIDと認証状態を渡す必要がある場合は、以下の方法を呼び出して、訪問の既知のIDを匿名のECIDにリンクします：




```kotlin
tealium.adobeVisitorApi?.linkEcidToKnownIdentifier("myidentifier", "123456", AdobeAuthState.AUTH_STATE_AUTHENTICATED, null)
```




```swift
tealium?.adobeVisitorApi?.linkECIDToKnownIdentifier("myidentifier", adobeDataProviderId: "123456", .unknown)
```




```javascript
TealiumAdobeVisitor.linkEcidToKnownIdentifier("myidentifier", "123456", AuthState.unknown, value => {
                console.log("AdobeVisitor Data: " + JSON.stringify(value))
});
```




```dart
TealiumAdobeVisitor.linkEcidToKnownIdentifier("myidentifier", "123456", AuthState.unknown)
```




## トラブルシューティング

以下は、異なるAPI障害の挙動をリストアップしています：

* **Adobe組織IDが不足している場合**  
モジュールが有効になっているが、`TealiumConfig`オブジェクトにAdobe組織IDが渡されていない場合、モジュールは無効になり、Adobe ECIDなしでトラッキング呼び出しが続行されます。

* **無効なAdobe組織ID**  
モジュールはリトライ制限（デフォルト：5）までリトライを試みます。リトライ制限を超えた後、トラッキング呼び出しは通常通り続行され、キューに入れられたリクエストはすぐに送信されます。

* **Adobe APIがエラーまたは空の応答を返す場合**  
リクエスト送信中にエラーが返された場合（例：接続障害など）、モジュールはリトライ制限（デフォルト：5）までリトライを試みます。リトライ制限を超えた後、トラッキング呼び出しは通常通り続行され、キューに入れられたリクエストはすぐに送信されます。

* 上記の（2）または（3）が発生したが、`TealiumConfig`オブジェクトに訪問の以前のECIDが提供されている場合、最大リトライ後にモジュールは提供された訪問ID値を使用し、リクエストのブロックは行いません。


<blockquote>
Tealiumへのデータ送信が最優先事項である場合は、障害時にECIDの取得をスキップするためにリトライ回数を0に構成します。リトライ回数は`config.adobeVisitorRetries`プロパティによって制御されます。
</blockquote>

## データレイヤー

以下の変数がデータレイヤーに追加されます：

| 変数            | タイプ    | 説明                                                                                                      |
|:----------------|:---------|:----------------------------------------------------------------------------------------------------------|
| `adobe_ecid`    | `String` | Adobe ECID。モジュールがAdobe Visitor APIからECIDを正常に取得した場合、すべてのトラッキングコールで存在します。 |
| `adobe_error`   | `String` | 遭遇したエラーの種類の説明、例えば `Org ID Not Set. ECID is not included from track requests`              |
| `queue_reason`  | `String` | モジュールによって訪問IDが利用可能になる前にイベントがキューに入れられます。                              |

## URLデコレーション

WebコンテキストでロードされたAdobe製品（例えばAdobe AnalyticsのJavaScriptタグ）は、自動的にExperience Cloud IDを使用します。このIDは、`adobe_mc`パラメーターでWebページのクエリ文字列に渡されます。`adobe_mc`パラメーターには、パイプ文字（`|`）で区切られた複数の値が含まれます。

| コンポーネント | 説明                                              | 例の値              |
|---------------|--------------------------------------------------|--------------------|
| MCMID         | Adobe Visitor Serviceから取得したExperience Cloud ID | 1234               |
| MCORGID       | Adobe Org ID                                     | 12345@AdobeOrg     |
| TS            | 秒単位のタイムスタンプ                           | 1655826247         |

結果のURLは以下の通りです：

`https://tealium.com/?adobe_mc=MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247`


<blockquote>
`adobe_mc`パラメーターはURLエンコードされています。
</blockquote>


Adobe Visitor Serviceモジュールは、この機能をサポートするための2つの方法を提供します。以下で説明します。

### タグ管理モジュール

`adobe_mc`パラメーターは、TealiumのWebビューで使用されるURLに自動的に追加されます。

### カスタムWebビュー

アプリがWebビューを使用してコンテンツを表示する場合、そのWebビューでAdobe製品がロードされるときにユーザーのECIDを知る必要があります。これにより、ネイティブアプリとWebビューでユーザーが異なるユーザーとして表示されるのを防ぎます。

Adobe Visitor Serviceモジュールは、クエリ文字列パラメーターでWebビューURLをデコレートする方法を提供します。これにより、モジュールによって生成されたECIDを使用してAdobe AnalyticsがExperience Cloud ID Service JavaScriptタグの代わりに使用します。例に示されているように、`decorateURL`メソッドにURLを渡し、アプリでWebビューをロードしたいときに返されたURLをロードする必要があります。


<blockquote>
この方法は、URLに既に存在するクエリパラメーターを保持します
</blockquote>





```kotlin
adobeVisitorModule?.decorateUrl(
            URL(url),
            object : UrlDecoratorHandler {
                override fun onDecorateUrl(url: URL) {
                  // 結果のURL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
                  // デモンストレーション目的のみ; アプリのWebビューで結果のURLを起動
                    myApp.launchWebview(url)
                }
            }
        )
```




```swift
let url = URL(string: "https://tealium.com/?myparam=abc&myparam2=bcd")!
tealium.adobeVisitorApi?.decorateURL(url) { url in
    // 結果のURL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // デモンストレーション目的のみ; アプリのWebビューで結果のURLを起動
    myApp.launchWebview(url)
}
```




```javascript
TealiumAdobeVisitor.decorateUrl("https://tealium.com", value => {
    // 結果のURL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // デモンストレーション目的のみ; アプリのWebビューで結果のURLを起動
    launchUrl(value);
});
```




```
// 結果のURL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
// デモンストレーション目的のみ; アプリのWebビューで結果のURLを起動
TealiumAdobeVisitor.decorateUrl("https://tealium.com").then(
                    (value) =>
                        launchUrl(value));
```




非標準のURLスキームを使用してWebビューをロードするアプリの場合、Adobe Visitor APIのクエリパラメーターを取得し、手動でURLに追加することができます。これらの方法はURLエンコードされていないパラメータ名と値を返すため、URLに追加する前に値をエンコードする必要があります。




```kotlin
adobeVisitorApi?.getUrlParameters(
    object : GetUrlParametersHandler {
        override fun onRetrieveParameters(params: Map<String, String>?) {
            params?.let {
                params.forEach {
                    Log.d("ADB Visitor","Retrieved URL Parameters:${it.key} = ${it.value}")
                }
            }
        }
    }
)
```




```swift
tealium.adobeVisitorApi.adobeVisitorApi?.getURLParameters { params in
            guard let params = params else {
                completion(nil)
                return
            }
            // 結果: params.name = adobe_mc
            //       params.value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // デモンストレーション目的のみ; アプリでURLをデコレートするメソッドを呼び出し、その後Webビューを起動
            print("Retrieved URL Parameters:\(params.name) = \(params.value)")
}
```




```javascript
TealiumAdobeVisitor.getUrlParameters(value => {
    if (value === null || value === undefined) {
        console.log("Adobe Visitor was null");
        return;
    } else {
        for (var key of Object.keys(value)) {
            // 結果: key = adobe_mc
            //       value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // デモンストレーション目的のみ; アプリでURLをデコレートするメソッドを呼び出し、その後Webビューを起動
            console.log("Retrieved URL Parameters: ", key + "=" + value[key]);
            break;
        }
    }
});
```




```
TealiumAdobeVisitor.getUrlParameters().then(
                            (value) =>
                            value?.forEach((key, value) {
                                // 結果: key = adobe_mc
                                //       value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
                                // デモンストレーション目的のみ; アプリでURLをデコレートするメソッドを呼び出し、その後Webビューを起動
                                print("Retrieved URL Parameters: $key = $value");
                            })
                    )
```


