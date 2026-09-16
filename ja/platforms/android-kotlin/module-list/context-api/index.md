---
title: Moments APIモジュール（現在はContext API）
description: Context APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/context-api/
---

<blockquote>
Moments APIはContext APIに名称が変更されました。製品の完全なドキュメントについては、[Context APIについて](https://docs.tealium.com/about-context-api/)をご覧ください。
</blockquote>


Context APIモジュールを使用すると、Tealium AudienceStreamから訪問プロファイルに関する詳細情報を取得できます。この情報を使用して、オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスすることで、アプリの顧客体験を向上させることができます。

## 対応プラットフォーム

以下のプラットフォームがContext APIモジュールをサポートしています：

- Android (Kotlin)

## インストール

Mavenを使用してContext APIモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルに次のMavenリポジトリを追加します：
   ```groovy
   maven {
       url "https://maven.tealiumiq.com/android/releases/"
   }
   ```

2. プロジェクトモジュールの`build.gradle`ファイルにTealiumライブラリとContext APIモジュールのMaven依存関係を追加します：
   ```groovy
   dependencies {
       implementation 'com.tealium:kotlin-core:1.6.0'
       implementation 'com.tealium:kotlin-momentsapi:1.0.0'
   }
   ```

## 使用方法

### 初期化

次のように構成を含めてTealiumインスタンスを初期化します：

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
    momentsApiRegion = MomentsApiRegion.UsEast // 下記の可能なリージョンオプションを参照
    // momentsApiRegion = MomentsApiRegion.Custom("myRegion")
}

Tealium.create("your_instance_name", config)
```


<blockquote>
リージョンの構成は必須です。リージョンがない場合、Context APIモジュールは初期化されません。
</blockquote>


### 訪問データの取得

`fetchEngineResponse`メソッドを使用して訪問プロファイル情報を取得します。このメソッドはエンジンIDとAPIレスポンスを処理するレスポンスリスナーを受け入れます。

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

`EngineResponse`オブジェクトには、Context APIによって返されるさまざまなタイプの属性が含まれています。以下の表は、利用可能なプロパティとそのデータタイプを示しています：

| プロパティ   | データタイプ             | 説明                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| List<String>          | 訪問が現在割り当てられているオーディエンスのリスト。     |
| `badges`   | List<String>          | 訪問に割り当てられたバッジのリスト。                     |
| `booleans` | Map<String, Boolean>  | 訪問に現在割り当てられているブール属性。       |
| `dates`    | Map<String, Long>     | 訪問に現在割り当てられている日付属性（ミリ秒単位）。  |
| `numbers`  | Map<String, Double>   | 訪問に現在割り当てられている数値属性。        |
| `strings`  | Map<String, String>   | 訪問に現在割り当てられている文字列属性。        |

## 構成オプション

### リージョン

AudienceStreamプロファイルが存在するリージョンに応じてContext APIリージョンを構成します。不明な場合は、アカウントマネージャーに相談してください。

| Enum Case    | Raw Value         |
|--------------|-------------------|
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
カスタムオプションは将来の拡張のためにありますが、指示がない限り使用しないでください。
</blockquote>


```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```

### リファラー

セキュリティをエンリッチメントするために、リファラーURLを指定することができます。このURLはTealium UIの「ドメイン許可リスト」と一致する必要があります。そうでない場合、Context APIはデータを返しません。デフォルトのリファラーURLは以下の通りです：

```
https://tags.tiqcdn.com/utag/<account>/<profile>/<environment>/mobile.html
```

提供されたリファラーが許可リストにない場合、Context APIはデータを返しません。

```kotlin
config.momentsApiReferrer = "https://yourcustomreferrer.com"
```

## トラブルシューティング

### 一般的なエラー

Context APIからデータをリクエストする際にエラーが発生することがあります。以下の表は、発生可能なエラーを示しています：

| エラー               | 説明                                                                                       | 解決策                                                                    |
|--------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `BAD_REQUEST`            | リクエストが適切にフォーマットされていないか、無効なパラメータを含んでいます。                           | Context APIモジュールを使用する場合、発生する可能性は低いです。                         |
| `ENGINE_NOT_ENABLED`     | Context APIエンジンがアカウントで有効になっていないか、リクエストが承認されていません。          | Context APIエンジンが適切に構成され、有効になっていることを確認してください。             |
| `VISITOR_NOT_FOUND`      | Tealium訪問IDにデータがデータベースに保存されていません。                                 | この訪問にはまだデータが存在しません。                                          |
| `UNKNOWN_ERROR`          | サーバーが予期しないステータスコードで応答しました。                                              | ドキュメントを参照するか、さらなる支援のためにサポートに連絡してください。          |
| `NOT_CONNECTED`          | Context APIと通信しようとする際にネットワークエラーが発生しました。                        | ネットワーク接続を確認して再試行してください。                                      |
| `INVALID_JSON`           | Context APIから返されたデータをデコードできませんでした。                                        | サポートに連絡してください。応答に予期しないデータタイプが含まれていました。              |
