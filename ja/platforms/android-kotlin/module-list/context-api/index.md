---
title: Context APIモジュール（現在のContext API）
description: Context APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/context-api/
---

<blockquote>
Moments APIはContext APIに名称変更されました。製品ドキュメント全体については、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。
</blockquote>


Context APIモジュールを使用すると、Customer Data Platform（CDP）から訪問プロファイルの詳細情報を取得できます。オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスし、この情報をアプリのカスタマーエクスペリエンス向上に活用できます。

## サポート対象プラットフォーム

Context APIモジュールは、次のプラットフォームをサポートしています。

- Android（Kotlin）

## インストール

Mavenを使用してContext APIモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenリポジトリを追加します。
   ```groovy
   maven {
       url "https://maven.tealiumiq.com/android/releases/"
   }
   ```

2. プロジェクトモジュールの`build.gradle`ファイルに、TealiumライブラリとContext APIモジュールのMaven依存関係を追加します。
   ```groovy
   dependencies {
       implementation 'com.tealium:kotlin-core:1.6.0'
       implementation 'com.tealium:kotlin-momentsapi:1.0.0'
   }
   ```

## 使用方法

### 初期化

次のように、構成にContext APIモジュールを含めてTealiumインスタンスを初期化します。

```kotlin
val config = TealiumConfig(
    application,
    "tealiummobile",
    "demo",
    Environment.DEV,
    modules = mutableSetOf(
        Modules.Lifecycle,
        Modules.VisitorService,
        Modules.MomentsApi
    ),
    dispatchers = mutableSetOf(
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    )
).apply {
    momentsApiRegion = MomentsApiRegion.UsEast // See possible region options below
    // momentsApiRegion = MomentsApiRegion.Custom("myRegion")
}

Tealium.create("your_instance_name", config)
```


<blockquote>
リージョンの構成は必須です。リージョンが構成されていない場合、Context APIモジュールは初期化されません。
</blockquote>


### 訪問データの取得

訪問プロファイル情報を取得するには、`fetchEngineResponse`メソッドを使用します。このメソッドは、エンジンIDと、APIレスポンスを処理するためのレスポンスリスナーを受け取ります。

```kotlin
fun fetchMoments(engineId: String, responseListener: ResponseListener<EngineResponse>) {
    val tealiumInstance = Tealium["your_instance_name"]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, responseListener)
}
```

### 例：Context APIデータの取得と処理

```kotlin
fun fetchMoments(engineId: String) {
    val tealiumInstance = Tealium["your_instance_name"]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, object : ResponseListener<EngineResponse> {
        override fun success(data: EngineResponse) {
            Log.d("MomentsAPI", "String attributes: ${data.strings}")
            Log.d("MomentsAPI", "Boolean attributes: ${data.booleans}")
            Log.d("MomentsAPI", "Audiences: ${data.audiences}")
            Log.d("MomentsAPI", "Date attributes: ${data.dates}")
            Log.d("MomentsAPI", "Badges: ${data.badges}")
            Log.d("MomentsAPI", "Numbers: ${data.numbers}")
        }

        override fun failure(errorCode: ErrorCode, message: String) {
            Log.e("MomentsAPI", "Error fetching moments: $errorCode - $message")
        }
    })
}
```

## 訪問プロファイルデータ

`EngineResponse`オブジェクトには、Context APIから返されるさまざまな種類の属性が含まれています。次の表に、使用可能なプロパティとそのデータ型を示します。

| プロパティ | データ型 | 説明 |
|------------|----------|------|
| `audiences`| List<String>          | 訪問が現在割り当てられているオーディエンスのリスト。 |
| `badges`   | List<String>          | 訪問に割り当てられているバッジのリスト。 |
| `booleans` | Map<String, Boolean>  | 訪問に現在割り当てられているブール属性。 |
| `dates`    | Map<String, Long>     | 訪問に現在割り当てられている日付属性（ミリ秒単位）。 |
| `numbers`  | Map<String, Double>   | 訪問に現在割り当てられている数値属性。 |
| `strings`  | Map<String, String>   | 訪問に現在割り当てられている文字列属性。 |

## 構成オプション

### リージョン

Customer Data Platform（CDP）プロファイルが配置されている場所に応じて、Context APIのリージョンを構成します。不明な場合は、アカウントマネージャーにお問い合わせください。

| 列挙型のケース | Raw値 |
|----------------|-------|
| `MomentsApiRegion.Germany`   | `eu-central-1`    |
| `MomentsApiRegion.UsEast`   | `us-east-1`       |
| `MomentsApiRegion.Sydney`    | `ap-southeast-2`  |
| `MomentsApiRegion.Oregon`    | `us-west-2`       |
| `MomentsApiRegion.Tokyo`     | `ap-northeast-1`  |
| `MomentsApiRegion.HongKong` | `ap-east-1`       |
| `MomentsApiRegion.Custom`    | `<custom string>` |

```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast
```


<blockquote>
カスタムオプションは将来の拡張用です。指示がない限り使用しないでください。
</blockquote>


```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```

### リファラー

セキュリティをエンリッチメントするために、リファラーURLを指定できます。このURLはTealium UIの「Domain Allow List」と一致している必要があります。一致しない場合、Context APIはデータを返しません。デフォルトのリファラーURLは次のとおりです。

```
https://tags.tiqcdn.com/utag/<account>/<profile>/<environment>/mobile.html
```

指定したリファラーが許可リストに含まれていない場合、Context APIはデータを返しません。

```kotlin
config.momentsApiReferrer = "https://yourcustomreferrer.com"
```

## トラブルシューティング

### 一般的なエラー

Context APIにデータをリクエストするときに、エラーが発生する場合があります。次の表に、発生する可能性のあるエラーを示します。

| エラー | 説明 | 解決方法 |
|--------|------|----------|
| `BAD_REQUEST`            | リクエストの形式が正しくないか、無効なパラメータが含まれています。 | Context APIモジュールを使用している場合、発生する可能性は低いです。 |
| `ENGINE_NOT_ENABLED`     | アカウントでContext APIエンジンが有効になっていないか、リクエストが承認されていません。 | Context APIエンジンが適切に構成され、有効になっていることを確認してください。 |
| `VISITOR_NOT_FOUND`      | Tealium訪問IDに対応するデータがデータベースに保存されていません。 | この訪問のデータはまだ存在しません。 |
| `UNKNOWN_ERROR`          | サーバーから予期しないステータスコードが返されました。 | 詳細については、ドキュメントを参照するか、サポートにお問い合わせください。 |
| `NOT_CONNECTED`          | Context APIとの通信中にネットワークエラーが発生しました。 | ネットワーク接続を確認して、再試行してください。 |
| `INVALID_JSON`           | Context APIから返されたデータをデコードできませんでした。 | サポートにお問い合わせください。レスポンスに予期しないデータ型が含まれています。 |