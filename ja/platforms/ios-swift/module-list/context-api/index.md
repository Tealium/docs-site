---
title: Context APIモジュール（現Context API）
description: Context APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/context-api/
---

<blockquote>
Moments APIはContext APIに名称変更されました。製品の完全なドキュメントについては、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。
</blockquote>


Context APIモジュールを使用すると、Customer Data Platform（CDP）から訪問プロファイルの詳細情報を取得できます。オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスすることで、アプリ内の顧客体験を向上させるためにこの情報を利用できます。

## サポート対象プラットフォーム

Context APIモジュールは、以下のプラットフォームをサポートしています。

- iOS
- macOS
- tvOS
- watchOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してContext APIモジュールをインストールします。

### Swift Package Manager（推奨）

1. Xcodeプロジェクトで、**File > Swift Packages > Add Package Dependency**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
1. バージョンルールを構成します。通常は`"Up to next major"`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールのリストから`TealiumMomentsAPI`、`TealiumCore`、および`TealiumCollect`または`TealiumTagManagement`のいずれかを選択し、Xcodeプロジェクトの**Frameworks and Libraries**で各アプリターゲットに追加します。

### CocoaPods

Podfileに以下のPodを追加します。

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' // or 'tealium-swift/TagManagement'
pod 'tealium-swift/MomentsAPI'
```

### Carthage

1. XcodeでアプリターゲットのGeneral構成ページに移動します。
2. **Embedded Binaries**セクションに以下のフレームワークを追加します。

   ```
   TealiumMomentsAPI.xcframework
   ```

3. 必要なimport文をプロジェクトに追加します。

   ```swift
   import TealiumCore
   import TealiumCollect // or import TealiumTagManagement
   import TealiumMomentsAPI
   ```

## 使用方法

### 初期化

モジュールを初期化するには、`TealiumConfig`の`collectors`プロパティにモジュールが指定されていることを確認します。

```swift
config.collectors = [Collectors.MomentsAPI]
config.momentsAPIRegion = .us_east // See possible region options below
```


<blockquote>
リージョンの構成は必須です。構成されていない場合、Context APIモジュールは初期化されません。
</blockquote>


### 訪問データの取得

パーソナライズされた訪問データを取得するには、`fetchEngineResponse`メソッドを呼び出します。アプリ内パーソナライゼーションのユースケースを実現する場合など、更新された訪問情報が必要になるたびに、このメソッドを呼び出してください。

```swift
func fetchMoments(engineId: String, completion: @escaping (Result<EngineResponse, Error>) -> Void) {
    tealium?.momentsAPI?.fetchEngineResponse(engineID: engineId) { engineResponse in
        switch engineResponse {
        case .success(let response):
            print("String attributes:", response.strings ?? [])
            print("Boolean attributes:", response.booleans ?? [])
            print("Audiences:", response.audiences ?? [])
            print("Date attributes:", response.dates ?? [:])
            print("Badges:", response.badges ?? [])
            print("Numbers:", response.numbers ?? [:])
        case .failure(let error):
            print("Error fetching moments:", error.localizedDescription)
            if let suggestion = (error as? LocalizedError)?.recoverySuggestion {
                print("Recovery suggestion:", suggestion)
            }
        }
        completion(engineResponse)
    }
}
```

## 訪問プロファイルデータ

`EngineResponse`オブジェクトには、Context APIから返されるさまざまな種類の属性が含まれています。次の表に、使用可能なプロパティとそのデータ型を示します。

| プロパティ | データ型 | 説明 |
|------------|----------|------|
| `audiences` | `[String]` | 訪問が現在割り当てられているオーディエンスのリスト。 |
| `badges` | `[String]` | 訪問に割り当てられているバッジのリスト。 |
| `booleans` | `[String: Bool]` | 訪問に現在割り当てられているブール属性。 |
| `dates` | `[String: Int64]` | 訪問に現在割り当てられている日付属性（ミリ秒単位）。 |
| `numbers` | `[String: Double]` | 訪問に現在割り当てられている数値属性。 |
| `strings` | `[String: String]` | 訪問に現在割り当てられている文字列属性。 |

## 構成オプション

### リージョン

Customer Data Platform（CDP）のプロファイルが保存されている場所に応じて、Context APIのリージョンを構成します。不明な場合は、アカウントマネージャーにお問い合わせください。

| 列挙型ケース | Raw値 |
|--------------|-------|
| `.germany` | `eu-central-1` |
| `.us_east` | `us-east-1` |
| `.sydney` | `ap-southeast-2` |
| `.oregon` | `us-west-2` |
| `.tokyo` | `ap-northeast-1` |
| `.hong_kong` | `ap-east-1` |
| `.custom` | `<custom string>` |

```swift
config.momentsAPIRegion = .us_east
```


<blockquote>
カスタムオプションは将来の拡張用です。指示がない限り使用しないでください。
</blockquote>


### リファラー

セキュリティをエンリッチメントするために、リファラーURLを指定できます。このURLはTealium UIの「Domain Allow List」と一致している必要があります。一致していない場合、Context APIはデータを返しません。デフォルトのリファラーURLは次のとおりです。

```
https://tags.tiqcdn.com/utag/{account}/{profile}/{environment}/mobile.html
```

次のようにカスタムリファラーURLを指定します。

```swift
let config = TealiumConfig(
    account: "tealiummobile",
    profile: "demo",
    environment: "prod"
)
config.momentsAPIReferrer = "https://example.com/"
tealium = Tealium(config: config) { _ in
    // Initialization complete
}
```

## トラブルシューティング

### 一般的なエラー

Context APIからデータをリクエストする際に、エラーが発生することがあります。次の表に、発生する可能性のあるエラーを示します。

| エラー | 説明 | 解決方法 |
|--------|------|----------|
| `.badRequest` | リクエストの形式が正しくないか、無効なパラメータが含まれています。 | Context APIモジュールを使用している場合、このエラーが発生する可能性は低いです。 |
| `.forbidden` | アカウントでContext APIエンジンが有効になっていないか、リクエストが認証されていません。 | Context APIエンジンが正しく構成され、有効になっていることを確認してください。 |
| `.notFound` | Tealium訪問IDのデータがデータベースに保存されていません。 | この訪問のデータはまだ存在しません。 |
| `.unsuccessful(statusCode: Int)` | サーバーが予期しないステータスコードを返しました。 | 詳細についてはドキュメントを参照するか、サポートにお問い合わせください。 |
| `.missingVisitorID` | リクエストに訪問IDが指定されていません。 | Context APIモジュールを使用している場合、このエラーが発生する可能性は低いです。 |
| `URLError` | Context APIとの通信中にネットワークエラーが発生しました。 | ネットワーク接続を確認して、再試行してください。 |
| `URLError(.cannotDecodeRawData)` | Context APIから返されたデータをデコードできませんでした。 | サポートにお問い合わせください。レスポンスに予期しないデータ型が含まれています。 |