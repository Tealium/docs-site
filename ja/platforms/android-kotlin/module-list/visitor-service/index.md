---
title: ビジターサービスモジュール
description: 現在のビジターの最新のプロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/visitor-service/
---
## 使用法

ビジターサービスモジュールは、ネイティブモバイルアプリに[データレイヤーのエンリッチメント](https://docs.tealium.com/enable-data-layer-enrichment/)機能を提供します。

このモジュールの使用には、Tealium AudienceStreamのライセンスが必要です。取得したビジタープロファイルを使用して、アプリケーション全体の顧客体験やデータレイヤーをエンリッチメントします。

## インストール

ビジターサービスモジュールは、Maven（推奨）または手動でインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとビジターサービスモジュールのMaven依存関係を追加します
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-visitor-service:1.2.0'
      }
      ```

### 手動

ビジターサービスモジュールを手動でインストールするには：

1. Tealiumの[ビジターサービス](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.visitorservice-1.2.0.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.visitorservice-1.2.0', ext:'aar')
      }
      ```


<blockquote>
Collect DispatcherはメインのTealium Kotlin SDKに依存しているので、[インストール手順](https://docs.tealium.com/ja/platforms/android-kotlin/install)に従ってこれも利用可能にすることを確認してください。
</blockquote>


## ビジタープロファイルデータ

現在のビジターデータを利用するには、最新のビジタープロファイルが更新されるたびに受け取るためのデリゲートオブジェクトを登録する必要があります：

```java
instance = Tealium.create("main", config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

VisitorProfileオブジェクトは、ビジターに関連する多くのフィールドにアクセスできます - 以下に利用可能なプロパティを概説します：

| パラメータ | プロパティ |  値 |
| --- | --- | --- |
| `arraysOfBooleans` | key: String, value: List\<Boolean\> | `key: "5129", value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | key: String, value: List\<Double\>| `key: "57", value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | key: String, value: List\<String\> | `key: "5213", value: listOf("green shirts", "green shirts", "blue shirts")` |
| `audiences` | key: String, name: String | `key: "tealiummobile_demo_103", name: "Kotlin Users"` |
| `badges` | key: String, value: Boolean | `key: "2815", value: true` |
| `booleans` | key: String, value: Boolean | `key: "4868", value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesは含まれていません。 | `CurrentVisit` |
| `dates` | key: String, value: Long | `key: "22", value: 1567120112000` |
| `numbers` | key: String, value: Double | `key: "5728", value: 4.82125` |
| `setsOfStrings` | key: String, value: Set\<String\> | `key: "5211", value: setOf("green shirts", "red shirts", "blue shirts")` |
| `strings` | key: String, value: String | `key: "5380", value: "green shirts"` |
| `tallies` | key: String, value: Map<String, Double> |  `key: "57", mapOf("category 1" to 2.0, "category 2" to 1.0)` |


以下は、ビジタープロファイルが取得された後にそれをどのように操作するかの基本的な例です。キー名はアカウント/プロファイルごとに異なります。
```java
val returningVisitor = visitorProfile.badges?.get("returning_visitor")
returningVisitor?.let {
    if (returningVisitor == true) {
        val ltv = visitorProfile.numbers?.get("lifetime_value")
        // take action
    }
}
```


## 構成オプション

TealiumConfigオブジェクトを作成する際に、以下の構成を使用してビジタープロファイルを取得するためのURLを構成します：

### ビジターサービスURLの上書き

ビジタープロファイルの更新を取得する際に使用するURLを構成します。

参照：[`TealiumConfig.overrideVisitorServiceUrl`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = "https://your.preferred.visitor-service.com"
```

デフォルト：`https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### ビジターサービスプロファイルの上書き

ビジタープロファイルの更新を取得する際に使用するTealiumプロファイルを構成します。参照：[`TealiumConfig.overrideVisitorServiceProfile`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = "someOtherTealiumProfile"
```

### ビジタープロファイルの更新間隔

最新のVisitorProfileデータを取得するための呼び出し間隔（秒）を構成します。参照：[`TealiumConfig.visitorServiceRefreshInterval`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval). 

デフォルト：300（5分）

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## APIリファレンス

ビジターサービスモジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android APIの[`VisitorService`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/)クラスを参照してください。

