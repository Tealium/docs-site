---
title: Moments APIモジュール
description: Moments APIを使用して訪問データを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/moments-api/
---
Moments APIモジュールを使用すると、Tealium AudienceStreamから訪問プロファイルの詳細情報を取得できます。この情報は、オーディエンス、バッジ、文字列、ブール値、日付、数値などのさまざまな属性にアクセスして、アプリ内の顧客体験を向上させるために使用できます。

## サポートされているプラットフォーム

以下のプラットフォームがMoments APIモジュールをサポートしています：

- Android (Kotlin)

## インストール

Mavenを使用してMoments APIモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
   ```groovy
   maven {
       url &#34;https://maven.tealiumiq.com/android/releases/&#34;
   }
   ```

2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとMoments APIモジュールのMaven依存関係を追加します：
   ```groovy
   dependencies {
       implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
       implementation &#39;com.tealium:kotlin-momentsapi:1.0.0&#39;
   }
   ```

## 使用方法

### 初期化

以下のように、構成にMoments APIモジュールを含めてTealiumインスタンスを初期化します：

```kotlin
val config = TealiumConfig(
    application,
    &#34;tealiummobile&#34;,
    &#34;demo&#34;,
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
    // momentsApiRegion = MomentsApiRegion.Custom(&#34;myRegion&#34;)
}

Tealium.create(&#34;your_instance_name&#34;, config)
```

 リージョンの構成は必須です。これが欠けていると、Moments APIモジュールは初期化されません。 

### 訪問データの取得

`fetchEngineResponse` メソッドを使用して訪問プロファイル情報を取得します。このメソッドはエンジンIDとAPIレスポンスを処理するレスポンスリスナーを受け入れます。

```kotlin
fun fetchMoments(engineId: String, responseListener: ResponseListener&lt;EngineResponse&gt;) {
    val tealiumInstance = Tealium[&#34;your_instance_name&#34;]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, responseListener)
}
```

### 例：Moments APIデータの取得と処理

```kotlin
fun fetchMoments(engineId: String) {
    val tealiumInstance = Tealium[&#34;your_instance_name&#34;]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, object : ResponseListener&lt;EngineResponse&gt; {
        override fun success(data: EngineResponse) {
            Log.d(&#34;MomentsAPI&#34;, &#34;String attributes: ${data.strings}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Boolean attributes: ${data.booleans}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Audiences: ${data.audiences}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Date attributes: ${data.dates}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Badges: ${data.badges}&#34;)
            Log.d(&#34;MomentsAPI&#34;, &#34;Numbers: ${data.numbers}&#34;)
        }

        override fun failure(errorCode: ErrorCode, message: String) {
            Log.e(&#34;MomentsAPI&#34;, &#34;Error fetching moments: $errorCode - $message&#34;)
        }
    })
}
```

## 訪問プロファイルデータ

`EngineResponse` オブジェクトには、Moments APIが返すさまざまなタイプの属性が含まれています。以下の表は、利用可能なプロパティとそのデータタイプを示しています：

| プロパティ   | データタイプ             | 説明                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| List&lt;String&gt;          | 訪問が現在割り当てられているオーディエンスのリスト。     |
| `badges`   | List&lt;String&gt;          | 訪問に割り当てられたバッジのリスト。                     |
| `booleans` | Map&lt;String, Boolean&gt;  | 訪問に現在割り当てられているブール属性。       |
| `dates`    | Map&lt;String, Long&gt;     | 訪問に現在割り当てられている日付属性（ミリ秒単位）。  |
| `numbers`  | Map&lt;String, Double&gt;   | 訪問に現在割り当てられている数値属性。        |
| `strings`  | Map&lt;String, String&gt;   | 訪問に現在割り当てられている文字列属性。        |

## 構成オプション

### リージョン

AudienceStreamプロファイルが存在する場所に応じて、Moments APIのリージョンを構成します。不確かな場合は、アカウントマネージャーに相談してください。

| Enum Case    | Raw Value         |
|--------------|-------------------|
| `MomentsApiRegion.Germany`   | `eu-central-1`    |
| `MomentsApiRegion.UsEast`   | `us-east-1`       |
| `MomentsApiRegion.Sydney`    | `ap-southeast-2`  |
| `MomentsApiRegion.Oregon`    | `us-west-2`       |
| `MomentsApiRegion.Tokyo`     | `ap-northeast-1`  |
| `MomentsApiRegion.HongKong` | `ap-east-1`       |
| `MomentsApiRegion.Custom`    | `&lt;custom string&gt;` |

```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast
```

 カスタムオプションは将来の拡張のためのものであり、指示がない限り使用しないでください。 

```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom(&#34;custom_region_placeholder&#34;)
```

### リファラー

追加のセキュリティのために、リファラーURLを指定できます。このURLはTealium UIの「ドメイン許可リスト」に一致する必要があります。そうでない場合、Moments APIはデータを返しません。デフォルトのリファラーURLは次のとおりです：

```
https://tags.tiqcdn.com/utag/&lt;account&gt;/&lt;profile&gt;/&lt;environment&gt;/mobile.html
```

提供されたリファラーが許可リストにない場合、Moments APIはデータを返しません。

```kotlin
config.momentsApiReferrer = &#34;https://yourcustomreferrer.com&#34;
```

## トラブルシューティング

### 一般的なエラー

Moments APIからデータをリクエストする際にエラーが発生することがあります。以下の表は、発生可能なエラーを示しています：

| エラー               | 説明                                                                                       | 解決策                                                                    |
|--------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `BAD_REQUEST`            | リクエストが適切にフォーマットされていないか、無効なパラメータを含んでいます。                           | Moments APIモジュールを使用している場合、発生する可能性は低いです。                         |
| `ENGINE_NOT_ENABLED`     | Moments APIエンジンがアカウントで有効になっていないか、リクエストが認証されていません。          | Moments APIエンジンが適切に構成され、有効になっていることを確認してください。             |
| `VISITOR_NOT_FOUND`      | Tealium訪問IDがデータベースに保存されているモーメントを持っていません。                              | この訪問のデータはまだ存在しません。                                          |
| `UNKNOWN_ERROR`          | サーバーが予期しないステータスコードで応答しました。                                              | ドキュメンテーションを参照するか、さらなる支援のためにサポートに連絡してください。          |
| `NOT_CONNECTED`          | Moments APIと通信しようとしたときにネットワークエラーが発生しました。                        | ネットワーク接続を確認し、再試行してください。                                      |
| `INVALID_JSON`           | Moments APIが返したデータをデコードできませんでした。                                        | サポートに連絡してください。レスポンスに予期しないデータタイプが含まれていました。              |