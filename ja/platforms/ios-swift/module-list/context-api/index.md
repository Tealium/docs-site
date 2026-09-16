---
title: Moments APIモジュール（現在はContext API）
description: Context APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/context-api/
---

<blockquote>
Moments APIはContext APIに名称が変更されました。製品の完全なドキュメントについては、[Context APIについて](https://docs.tealium.com/about-context-api/)をご覧ください。
</blockquote>


Context APIモジュールを使用すると、Tealium AudienceStreamから訪問プロファイルに関する詳細情報を取得できます。この情報を使用して、オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスすることにより、アプリの顧客体験を向上させることができます。

## 対応プラットフォーム

以下のプラットフォームがContext APIモジュールをサポートしています：

- iOS
- macOS
- tvOS
- watchOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してContext APIモジュールをインストールします。

### Swift Package Manager（推奨）

1. Xcodeプロジェクトで、**File > Swift Packages > Add Package Dependency** を選択します
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は「"Up to next major"」が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールして追加するモジュールのリストから`TealiumMomentsAPI`、`TealiumCore`、および`TealiumCollect`または`TealiumTagManagement`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットの**Frameworks and Libraries**の下に追加します。

### CocoaPods

Podfileに以下のポッドを追加します：

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' // or 'tealium-swift/TagManagement'
pod 'tealium-swift/MomentsAPI'
```

### Carthage

1. XcodeのアプリターゲットのGeneral構成ページに移動します。
2. 次のフレームワークを**Embedded Binaries**セクションに追加します：

   ```
   TealiumMomentsAPI.xcframework
   ```

3. プロジェクトに必要なインポート文を追加します：

   ```swift
   import TealiumCore
   import TealiumCollect // or import TealiumTagManagement
   import TealiumMomentsAPI
   ```

## 使用方法

### 初期化

モジュールを初期化するには、`TealiumConfig`の`collectors`プロパティに指定する必要があります。

```swift
config.collectors = [Collectors.MomentsAPI]
config.momentsAPIRegion = .us_east // 下記の可能なリージョンオプションを参照
```


<blockquote>
リージョンの構成は必須です。リージョンがない場合、Context APIモジュールは初期化されません。
</blockquote>


### 訪問データの取得

`fetchEngineResponse`メソッドを呼び出してパーソナライズされた訪問データを取得します。これは、アプリ内パーソナライゼーションのユースケースをサポートするために、更新された訪問情報が必要な場合に呼び出す必要があります。

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

`EngineResponse`オブジェクトには、Context APIによって返されるさまざまなタイプの属性が含まれています。以下の表は、利用可能なプロパティとそのデータタイプを示しています：

| プロパティ   | データタイプ             | 説明                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| `[String]`          | 訪問が現在割り当てられているオーディエンスのリストです。     |
| `badges`   | `[String]`          | 訪問に割り当てられているバッジのリストです。                     |
| `booleans` | `[String: Bool]`  | 訪問に現在割り当てられているブール属性です。       |
| `dates`    | `[String: Int64]`     | 訪問に現在割り当てられている日付属性（ミリ秒単位）。  |
| `numbers`  | `[String: Double]`   | 訪問に現在割り当てられている数値属性です。        |
| `strings`  | `[String: String]`  | 訪問に現在割り当てられている文字列属性です。        |

## 構成オプション

### リージョン

AudienceStreamプロファイルが存在するリージョンに応じてContext APIリージョンを構成します。不明な場合は、アカウントマネージャーに相談してください。

| Enum Case    | Raw Value         |
|--------------|-------------------|
| `.germany`   | `eu-central-1`    |
| `.us_east`   | `us-east-1`       |
| `.sydney`    | `ap-southeast-2`  |
| `.oregon`    | `us-west-2`       |
| `.tokyo`     | `ap-northeast-1`  |
| `.hong_kong` | `ap-east-1`       |
| `.custom`    | `<custom string>` |

```swift
config.momentsAPIRegion = .us_east
```


<blockquote>
カスタムオプションは将来の拡張のためにありますが、指示がない限り使用しないでください。
</blockquote>


### リファラー

セキュリティをエンリッチメントするために、リファラーURLを指定することができます。このURLはTealium UIの「ドメイン許可リスト」と一致する必要があります。そうでない場合、Context APIはデータを返しません。デフォルトのリファラーURLは以下の通りです：

```
https://tags.tiqcdn.com/utag/{account}/{profile}/{environment}/mobile.html
```

以下に示すようにカスタムリファラーURLを指定します：

```swift
let config = TealiumConfig(
    account: "tealiummobile",
    profile: "demo",
    environment: "prod"
)
config.momentsAPIReferrer = "https://example.com/"
tealium = Tealium(config: config) { _ in
    // 初期化完了
}
```

## トラブルシューティング

### 一般的なエラー

Context APIからデータをリクエストする際にエラーが発生することがあります。以下の表は、発生可能なエラーを示しています：

| エラー                        | 説明                                                                                       | 解決策                                                                    |
|----------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `.badRequest`                    | リクエストが適切にフォーマットされていないか、無効なパラメータを含んでいます。                           | Context APIモジュールを使用している場合、発生する可能性は低いです。                         |
| `.forbidden`                     | Context APIエンジンがアカウントで有効になっていないか、リクエストが認証されていません。          | Context APIエンジンが適切に構成され、有効になっていることを確認してください。             |
| `.notFound`                      | Tealium訪問IDにデータベースにデータが保存されていません。                                 | この訪問にはまだデータが存在しません。                                          |
| `.unsuccessful(statusCode: Int)` | サーバーが予期しないステータスコードで応答しました。                                              | ドキュメントを参照するか、さらなる支援のためにサポートに連絡してください。          |
| `.missingVisitorID`              | リクエストに訪問IDが提供されていません。                                                   | Context APIモジュールを使用している場合、発生する可能性は低いです。                         |
| `URLError`                       | Context APIと通信しようとする際にネットワークエラーが発生しました。                        | ネットワーク接続を確認して再試行してください。                                      |
| `URLError(.cannotDecodeRawData)` | Context APIから返されたデータをデコードできませんでした。                                        | サポートに連絡してください。応答に予期しないデータタイプが含まれていました。              |
