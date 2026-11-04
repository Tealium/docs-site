---
title: Visitor Serviceモジュール
description: 現在の訪問の最新プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/visitor-service/
---
## 使用方法

Visitor Serviceモジュールは、ネイティブモバイルアプリに[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を提供します。

このモジュールを使用するには、Customer Data Platform（CDP）のライセンスが必要です。取得した訪問プロファイルを使用して、アプリケーション全体のカスタマーエクスペリエンスやデータレイヤーをエンリッチメントできます。

## インストール

Maven（推奨）を使用するか、手動でVisitor Serviceモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには、次の手順に従います。

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenリポジトリを追加します。
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに、TealiumライブラリとVisitor ServiceモジュールのMaven依存関係を追加します。
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-visitor-service:1.2.0'
      }
      ```

### 手動

Visitor Serviceモジュールを手動でインストールするには、次の手順に従います。

1. Tealiumの[Visitor Service](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice)モジュールをダウンロードします。

2. `tealium-kotlin.visitorservice-1.2.0.aar`ファイルを、プロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

3. Tealiumライブラリの依存関係を、プロジェクトモジュールの`build.gradle`ファイルに追加します。
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.visitorservice-1.2.0', ext:'aar')
      }
      ```


<blockquote>
Collect DispatcherはメインのTealium Kotlin SDKに依存しているため、[インストール手順](https://docs.tealium.com/ja/platforms/android-kotlin/install)に従って、このSDKも利用可能にしてください。
</blockquote>


## 訪問プロファイルデータ

現在の訪問データを使用するには、Visitor Profileが更新されるたびに最新のプロファイルを受信するデリゲートオブジェクトを登録する必要があります。

```java
instance = Tealium.create("main", config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

VisitorProfileオブジェクトからは、訪問に関連する多くのフィールドにアクセスできます。使用可能なプロパティは次のとおりです。

| パラメータ | プロパティ | 値 |
| --- | --- | --- |
| `arraysOfBooleans` | キー：String、値：List\<Boolean\> | `key: "5129", value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | キー：String、値：List\<Double\>| `key: "57", value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | キー：String、値：List\<String\> | `key: "5213", value: listOf("green shirts", "green shirts", "blue shirts")` |
| `audiences` | キー：String、名前：String | `key: "tealiummobile_demo_103", name: "Kotlin Users"` |
| `badges` | キー：String、値：Boolean | `key: "2815", value: true` |
| `booleans` | キー：String、値：Boolean | `key: "4868", value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルには、AudiencesまたはBadgesは含まれません。 | `CurrentVisit` |
| `dates` | キー：String、値：Long | `key: "22", value: 1567120112000` |
| `numbers` | キー：String、値：Double | `key: "5728", value: 4.82125` |
| `setsOfStrings` | キー：String、値：Set\<String\> | `key: "5211", value: setOf("green shirts", "red shirts", "blue shirts")` |
| `strings` | キー：String、値：String | `key: "5380", value: "green shirts"` |
| `tallies` | キー：String、値：Map<String, Double> | `key: "57", mapOf("category 1" to 2.0, "category 2" to 1.0)` |

次は、Visitor Profileの取得後に操作する方法を示す基本的な例です。キー名はアカウントまたはプロファイルごとに異なります。

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

TealiumConfigオブジェクトの作成時に次の構成を使用して、Visitor Profileの取得に使用するURLを構成します。

### Visitor Service URLのオーバーライド

訪問プロファイルの更新を取得するときに使用するURLを構成します。

参照：[`TealiumConfig.overrideVisitorServiceUrl`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl)

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = "https://your.preferred.visitor-service.com"
```

デフォルト：`https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### Visitor Serviceプロファイルのオーバーライド

訪問プロファイルの更新を取得するときに使用するTealiumプロファイルを構成します。参照：[`TealiumConfig.overrideVisitorServiceProfile`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile)

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = "someOtherTealiumProfile"
```

### 訪問プロファイルの更新間隔

最新のVisitorProfileデータを取得する呼び出しの時間間隔を秒単位で構成します。参照：[`TealiumConfig.visitorServiceRefreshInterval`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval)

デフォルト：300（5分）

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## APIリファレンス

Visitor Serviceモジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android APIの[`VisitorService`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/)クラスを参照してください。