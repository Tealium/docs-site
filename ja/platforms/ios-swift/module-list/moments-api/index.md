---
title: Moments APIモジュール
description: Moments APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/moments-api/
---
Moments APIモジュールを使用すると、Tealium AudienceStreamから訪問プロファイルの詳細情報を取得できます。この情報は、オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスして、アプリ内の顧客体験を向上させるために使用できます。

## サポートされているプラットフォーム

以下のプラットフォームがMoments APIモジュールをサポートしています：

- iOS
- macOS
- tvOS
- watchOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してMoments APIモジュールをインストールします。

### Swift Package Manager（推奨）

1. Xcodeプロジェクトで、**File &gt; Swift Packages &gt; Add Package Dependency**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`&#34;Up to next major&#34;`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`TealiumMomentsAPI`、`TealiumCore`、および`TealiumCollect`または`TealiumTagManagement`モジュールを選択し、それらをXcodeプロジェクトの各アプリターゲットに追加します。これは**Frameworks and Libraries**の下にあります。

### CocoaPods

Podfileに以下のpodsを追加します：  

```perl
pod &#39;tealium-swift/Core&#39;
pod &#39;tealium-swift/Collect&#39; // or &#39;tealium-swift/TagManagement&#39;
pod &#39;tealium-swift/MomentsAPI&#39;
```

### Carthage

1. Xcodeでアプリターゲットの一般構成ページに移動します。
2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  

   ```
   TealiumMomentsAPI.xcframework
   ```

3. 必要なインポート文をプロジェクトに追加します：  

   ```swift
   import TealiumCore
   import TealiumCollect // or import TealiumTagManagement
   import TealiumMomentsAPI
   ```

## 使用法

### 初期化

モジュールを初期化するには、`TealiumConfig`の`collectors`プロパティで指定されていることを確認します。

```swift
config.collectors = [Collectors.MomentsAPI]
config.momentsAPIRegion = .us_east // 下記の可能なリージョンオプションを参照
```

 リージョンの構成は必須です。これが欠けていると、Moments APIモジュールは初期化されません。 

### 訪問データの取得

`fetchEngineResponse`メソッドを呼び出して、パーソナライズされた訪問データを取得します。これは、アプリ内のパーソナライゼーションのユースケースを実現するために、更新された訪問情報が必要なときに呼び出すべきです。

```swift
func fetchMoments(engineId: String, completion: @escaping (Result&lt;EngineResponse, Error&gt;) -&gt; Void) {
    tealium?.momentsAPI?.fetchEngineResponse(engineID: engineId) { engineResponse in
        switch engineResponse {
        case .success(let response):
            print(&#34;String attributes:&#34;, response.strings ?? [])
            print(&#34;Boolean attributes:&#34;, response.booleans ?? [])
            print(&#34;Audiences:&#34;, response.audiences ?? [])
            print(&#34;Date attributes:&#34;, response.dates ?? [:])
            print(&#34;Badges:&#34;, response.badges ?? [])
            print(&#34;Numbers:&#34;, response.numbers ?? [:])
        case .failure(let error):
            print(&#34;Error fetching moments:&#34;, error.localizedDescription)
            if let suggestion = (error as? LocalizedError)?.recoverySuggestion {
                print(&#34;Recovery suggestion:&#34;, suggestion)
            }
        }
        completion(engineResponse)
    }
}
```

## 訪問プロファイルデータ

`EngineResponse`オブジェクトには、Moments APIが返すさまざまなタイプの属性が含まれています。以下の表は、利用可能なプロパティとそのデータタイプを示しています：

| プロパティ   | データタイプ             | 説明                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| `[String]`          | 訪問が現在割り当てられているオーディエンスのリスト。     |
| `badges`   | `[String]`          | 訪問に割り当てられたバッジのリスト。                     |
| `booleans` | `[String: Bool]`  | 訪問に現在割り当てられているブール属性。       |
| `dates`    | `[String: Int64]`     | 訪問に現在割り当てられている日付属性（ミリ秒単位）。  |
| `numbers`  | `[String: Double]`   | 訪問に現在割り当てられている数値属性。        |
| `strings`  | `[String: String]`  | 訪問に現在割り当てられている文字列属性。        |

## 構成オプション

### リージョン

AudienceStreamプロファイルが存在する場所に応じて、Moments APIのリージョンを構成します。不確かな場合は、アカウントマネージャーに相談してください。

| Enum Case    | Raw Value         |
|--------------|-------------------|
| `.germany`   | `eu-central-1`    |
| `.us_east`   | `us-east-1`       |
| `.sydney`    | `ap-southeast-2`  |
| `.oregon`    | `us-west-2`       |
| `.tokyo`     | `ap-northeast-1`  |
| `.hong_kong` | `ap-east-1`       |
| `.custom`    | `&lt;custom string&gt;` |

```swift
config.momentsAPIRegion = .us_east
```

 カスタムオプションは将来の拡張のためのものであり、指示がない限り使用しないでください。 

### リファラー

追加のセキュリティのために、リファラーURLを指定できます。このURLはTealium UIの&#34;Domain Allow List&#34;と一致する必要があります。そうでない場合、Moments APIはデータを返しません。デフォルトのリファラーURLは次のとおりです：

```
https://tags.tiqcdn.com/utag/{account}/{profile}/{environment}/mobile.html
```

以下のようにカスタムリファラーURLを指定します：

```swift
let config = TealiumConfig(
    account: &#34;tealiummobile&#34;,
    profile: &#34;demo&#34;,
    environment: &#34;prod&#34;
)
config.momentsAPIReferrer = &#34;https://example.com/&#34;
tealium = Tealium(config: config) { _ in
    // Initialization complete
}
```

## トラブルシューティング

### 一般的なエラー

Moments APIからデータをリクエストするときにエラーが発生することがあります。以下の表は、発生可能なエラーを示しています：

| エラー                        | 説明                                                                                       | 解決策                                                                    |
|----------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `.badRequest`                    | リクエストが適切にフォーマットされていないか、無効なパラメータを含んでいます。                           | Moments APIモジュールを使用している場合、発生する可能性は低いです。                         |
| `.forbidden`                     | Moments APIエンジンがアカウントで有効化されていないか、リクエストが認証されていません。          | Moments APIエンジンが適切に構成され、有効化されていることを確認します。             |
| `.notFound`                      | Tealium訪問IDがデータベースに保存されているモーメントを持っていません。                              | この訪問のデータはまだ存在しません。                                          |
| `.unsuccessful(statusCode: Int)` | サーバーが予期しないステータスコードで応答しました。                                              | ドキュメンテーションを参照するか、サポートに連絡してさらなる支援を求めます。          |
| `.missingVisitorID`              | リクエストに訪問IDが提供されていません。                                                   | Moments APIモジュールを使用している場合、発生する可能性は低いです。                         |
| `URLError`                       | Moments APIと通信しようとしたときにネットワークエラーが発生しました。                        | ネットワーク接続を確認し、再試行します。                                      |
| `URLError(.cannotDecodeRawData)` | Moments APIが返したデータをデコードできませんでした。                                        | サポートに連絡します。レスポンスには予期しないデータタイプが含まれていました。              |