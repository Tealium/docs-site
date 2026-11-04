---
title: Adobe Visitor Service モジュール
description: Adobe Visitor Service モジュールについて説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/adobe-visitor-service/
---
Adobe Visitor Service モジュールは、Adobe の REST API と直接連携し、訪問の Experience Cloud ID（ECID）を取得および維持します。ECID は、Adobe Target や Adobe Analytics など、Adobe エコシステムのさまざまな領域で同一の訪問を識別し、ユニーク訪問を特定します。

Adobe トラッキング SDK から Tealium SDK に移行する場合は、Adobe Visitor Service モジュールを使用して、トラッキングペイロードで ECID を渡します。データレイヤー内の新しい ECID は、Event Streaming または Customer Data Platform（CDP）のサーバーサイド Adobe コネクタでマッピングできます。Adobe Visitor Service モジュールは、既存の ECID がある場合はそれを再利用し、ない場合は新しい ECID を生成することで、Tealium SDK へのシームレスな移行を実現し、アプリ内の訪問数を正確に集計できるようにします。

## サポート対象プラットフォーム

Adobe Visitor Service モジュールは、次のプラットフォームでサポートされています。

- [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/adobe-visitor-service/)
- [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/module-list/adobe-visitor-service/)
- [Tealium for React Native](https://docs.tealium.com/ja/platforms/react-native/adobe-visitor-service/)
- [Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/adobe-visitor-service/)

## ユースケース

### サーバーサイド Analytics への移行

Adobe 統合をサーバーサイドに移行し、Event Streaming を介して Adobe Analytics をサーバーサイドで使用するコネクタ内の `marketingCloudVisitorID` パラメータに ECID をマッピングします。これにより、複数の Adobe 製品を連携させるために必要な有効な ECID を利用できます。Tealium SDK は、Event Streaming に呼び出しを送信する前に Adobe から ECID をリクエストし、その ECID は Adobe Analytics コネクタの `marketingCloudVisitorID` プロパティにマッピングされます。

### タグ管理

Adobe Analytics タグを使用する場合は、タグ管理を使用して ECID を生成することをお勧めします。これにより、ECID がすぐに利用可能となり、保存に永続化され、非表示の WebView 内の Cookie ストアに依存しないことが保証されます。

### Adobe SDK から Tealium SDK への移行

Adobe SDK から Tealium モジュールへの移行はシームレスです。現在、アプリで Adobe SDK を使用して ECID を管理している場合は、Adobe SDK と Tealium SDK の両方をアプリに含める移行期間を設けることをお勧めします。訪問に既存の Adobe ECID がある場合は、`config.adobeVisitorExistingEcid` プロパティを使用して Tealium モジュールに渡します。初期化時にこのプロパティが構成されている場合は、既存の ECID が使用されます。構成されていない場合、Tealium モジュールは Adobe API から新しい ECID を取得します。

### 同じデバイス上で異なる訪問をトラッキングする

アプリ内で異なる訪問アカウントを検出した場合は、`tealium.adobeVisitor?.resetVisitor()` を呼び出して ECID をリセットし、各訪問が個別にトラッキングされるようにします。これにより現在の ECID がリセットされ、新しい ECID が Adobe API に自動的にリクエストされます。

### 既知の訪問 ID と認証状態を構成する

`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、および `adobeVisitorAuthState` の構成プロパティは、アプリセッションの開始時に 3 つすべての値が判明している場合にのみ使用してください。`adobeVisitorAuthState` は、`adobeVisitorCustomVisitorId` も構成する場合にのみ構成してください。

初期化時に訪問の ID が不明な場合（たとえば、ユーザーがログインする前）は、これらのプロパティを省略し、ID が利用可能になった時点で `linkEcidToKnownIdentifier` を呼び出します。

初期化時にすべての値が判明している場合は、モジュールの起動時に `TealiumConfig` オブジェクトで構成します。




```kotlin
config.adobeVisitorDataProviderId = "01" // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```swift
config.adobeVisitorDataProviderId = "01" // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = .authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```javascript
config.adobeVisitorDataProviderId = "01" // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




```dart
config.adobeVisitorDataProviderId = "01" // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = "customeremail@emailprovider.com"
```




モジュールは必要に応じて新しい ID を自動的にリクエストし、その後、追加の API 呼び出しを送信して、ECID を `TealiumConfig` プロパティで指定された既知の ID にリンクします。

訪問のログイン時に ID と認証状態を渡す必要がある場合は、次のメソッドを呼び出して、訪問の既知の ID を匿名 ECID にリンクします。




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

API 障害時の動作は次のとおりです。

* **Adobe 組織 ID がない**  
モジュールが有効になっていても、Adobe 組織 ID が `TealiumConfig` オブジェクトに渡されていない場合、モジュールは無効になり、Adobe ECID なしでトラッキング呼び出しが続行されます。

* **Adobe 組織 ID が無効**  
モジュールは、再試行上限（デフォルト：5 回）まで再試行します。再試行上限を超えると、ECID なしで通常どおりトラッキング呼び出しが続行され、キューに入っているすべてのリクエストが直ちに送信されます。

* **Adobe API がエラーまたは空のレスポンスを返す**  
接続障害などにより、リクエストの送信中にエラーが返された場合、モジュールは再試行上限（デフォルト：5 回）まで再試行します。再試行上限を超えると、ECID なしで通常どおりトラッキング呼び出しが続行され、キューに入っているすべてのリクエストが直ちに送信されます。

* モジュールで上記の（2）または（3）が発生したものの、訪問の以前の ECID が `TealiumConfig` オブジェクトで指定されている場合、最大再試行回数に達した後、モジュールは指定された訪問 ID の値を使用し、リクエストをブロックしません。


<blockquote>
Tealium にデータを送信することを最優先する場合は、再試行回数を 0 に構成し、障害発生時の ECID の取得をスキップしてください。再試行回数は `config.adobeVisitorRetries` プロパティで制御します。
</blockquote>

## データレイヤー

次の変数がデータレイヤーに追加されます。

| 変数           | 型       | 説明                                                                                                                                 |
|:---------------|:---------|:-------------------------------------------------------------------------------------------------------------------------------------|
| `adobe_ecid`   | `String` | Adobe ECID。モジュールが Adobe Visitor API から ECID を正常に取得すると、すべてのトラッキング呼び出しに含まれます。                   |
| `adobe_error`  | `String` | 発生したエラーの種類の説明（例：`Org ID Not Set. ECID is not included from track requests`）                                        |
| `queue_reason` | `String` | 訪問 ID が利用可能になる前に、モジュールによってイベントがキューに追加された理由。                                                |

## URL の修飾

Adobe Analytics JavaScript タグなど、Web コンテキストで読み込まれる Adobe 製品では、Experience Cloud ID が自動的に使用されます。この ID は、Web ページのクエリ文字列に `adobe_mc` パラメータとして渡されます。`adobe_mc` パラメータには、パイプ文字（`|`）で区切られた複数の値が含まれます。

| コンポーネント | 説明                                                  | 値の例         |
|----------------|-------------------------------------------------------|----------------|
| MCMID          | Adobe Visitor Service から取得した Experience Cloud ID | 1234           |
| MCORGID        | Adobe 組織 ID                                         | 12345@AdobeOrg |
| TS             | 秒単位のタイムスタンプ                                | 1655826247     |

生成される URL は次のとおりです。

`https://tealium.com/?adobe_mc=MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247`


<blockquote>
`adobe_mc` パラメータは URL エンコードされます。
</blockquote>


Adobe Visitor Service モジュールでは、この機能をサポートするために、以下で説明する 2 つのメソッドを提供しています。

### タグ管理モジュール

`adobe_mc` パラメータは、タグ管理モジュールの Tealium WebView で使用される URL に自動的に追加されます。

### カスタム WebView

アプリで WebView を使用してコンテンツを表示する場合は、WebView 内で Adobe ECID を利用できるようにする必要があります。これにより、WebView に読み込まれたすべての Adobe 製品がユーザーの ECID を認識できます。また、ネイティブアプリと WebView で、同じユーザーが別々のユーザーとして認識されることを防げます。

Adobe Visitor Service モジュールには、クエリ文字列パラメータを使用して WebView の URL を修飾するメソッドが用意されています。これにより、Adobe Analytics は Experience Cloud ID Service の JavaScript タグではなく、モジュールによって生成された ECID を使用します。例に示すように、URL を `decorateURL` メソッドに渡し、アプリで WebView を読み込む際に、返された URL を読み込む必要があります。


<blockquote>
このメソッドでは、URL にすでに含まれているクエリパラメータが維持されます。
</blockquote>





```kotlin
adobeVisitorModule?.decorateUrl(
            URL(url),
            object : UrlDecoratorHandler {
                override fun onDecorateUrl(url: URL) {
                  // Resulting URL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
                  // Only for demonstration purposes; launch your app's webview with the resulting URL
                    myApp.launchWebview(url)
                }
            }
        )
```




```swift
let url = URL(string: "https://tealium.com/?myparam=abc&myparam2=bcd")!
tealium.adobeVisitorApi?.decorateURL(url) { url in
    // Resulting URL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // Only for demonstration purposes; launch your app's webview with the resulting URL
    myApp.launchWebview(url)
}
```




```javascript
TealiumAdobeVisitor.decorateUrl("https://tealium.com", value => {
    // Resulting URL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // Only for demonstration purposes; launch your app's webview with the resulting URL
    launchUrl(value);
});
```




```
// Resulting URL = https://tealium.com/?myparam=abc&myparam2=bcd&adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
// Only for demonstration purposes; launch your app's webview with the resulting URL
TealiumAdobeVisitor.decorateUrl("https://tealium.com").then(
                    (value) =>
                        launchUrl(value));
```




Angular など、標準以外の URL スキームを使用する WebView をアプリで読み込む場合は、Adobe Visitor API のクエリパラメータを取得し、URL に手動で追加できます。これらのメソッドは URL エンコードされていないパラメータ名と値を返すため、URL に追加する前に値をエンコードする必要があります。




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
            // Result: params.name = adobe_mc
            //         params.value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
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
            // Result: key = adobe_mc
            //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
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
                                // Result: key = adobe_mc
                                //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
                                // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
                                print("Retrieved URL Parameters: $key = $value");
                            })
                    )
```


