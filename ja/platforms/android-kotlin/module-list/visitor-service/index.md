---
title: 訪問サービスモジュール
description: 現在の訪問の最新プロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/visitor-service/
---
## 使用方法

訪問サービスモジュールは、ネイティブモバイルアプリにデータレイヤー機能エンリッチメントを提供します。

このモジュールの使用には、Tealium AudienceStreamのライセンスが必要です。取得した訪問プロファイルを使用して、アプリケーション全体の顧客体験またはデータレイヤーを向上させます。

## インストール

Maven（推奨）または手動で訪問サービスモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに以下のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリと訪問サービスモジュールのMaven依存関係を追加します：
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-visitor-service:1.2.0'
      }
      ```

### 手動

訪問サービスモジュールを手動でインストールするには：

1. Tealiumの[訪問サービス](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.visitorservice-1.2.0.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.visitorservice-1.2.0', ext:'aar')
      }
      ```


<blockquote>
Collect DispatcherはTealium Kotlin SDKのメインに依存しているため、[インストール手順](https://docs.tealium.com/ja/platforms/android-kotlin/install)に従ってこれを利用可能にすることを確認してください。
</blockquote>


## 訪問プロファイルデータ

現在の訪問データを使用するには、更新されるたびに最新の訪問プロファイルを受け取るためのデリゲートオブジェクトを登録する必要があります：

```java
instance = Tealium.create("main", config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

訪問プロファイルオブジェクトは、訪問に関連する多くのフィールドにアクセスできます。以下は利用可能なプロパティを概説しています：

| パラメータ | プロパティ |  値 |
| --- | --- | --- |
| `arraysOfBooleans` | key: String, value: List\<Boolean\> | `key: "5129", value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | key: String, value: List\<Double\>| `key: "57", value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | key: String, value: List\<String\> | `key: "5213", value: listOf("green shirts", "green shirts", "blue shirts")` |
| `audiences` | key: String, name: String | `key: "tealiummobile_demo_103", name: "Kotlin Users"` |
| `badges` | key: String, value: Boolean | `key: "2815", value: true` |
| `booleans` | key: String, value: Boolean | `key: "4868", value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesが含まれていません。 | `CurrentVisit` |
| `dates` | key: String, value: Long | `key: "22", value: 1567120112000` |
| `numbers` | key: String, value: Double | `key: "5728", value: 4.82125` |
| `setsOfStrings` | key: String, value: Set\<String\> | `key: "5211", value: setOf("green shirts", "red shirts", "blue shirts")` |
| `strings` | key: String, value: String | `key: "5380", value: "green shirts"` |
| `tallies` | key: String, value: Map<String, Double> |  `key: "57", mapOf("category 1" to 2.0, "category 2" to 1.0)` |

以下は、取得した訪問プロファイルを操作する基本的な例です。アカウント/プロファイルごとにキー名が異なります。
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

訪問プロファイルを取得するために使用するURLを次の構成で指定します：

### 訪問サービスURLの上書き

訪問プロファイルの更新を取得する際に使用するURLを構成します。

参照：[`TealiumConfig.overrideVisitorServiceUrl`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = "https://your.preferred.visitor-service.com"
```

デフォルト：`https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### 訪問サービスプロファイルの上書き

訪問プロファイルの更新を取得する際に使用するTealiumプロファイルを構成します。参照：[`TealiumConfig.overrideVisitorServiceProfile`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = "someOtherTealiumProfile"
```

### 訪問プロファイル更新間隔

訪問プロファイルデータを取得するための呼び出し間の時間間隔を秒単位で構成します。参照：[`TealiumConfig.visitorServiceRefreshInterval`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval). 

デフォルト：300（5分）

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30分
```

## APIリファレンス

訪問サービスモジュールで使用されるメソッドのリファレンスについては、Android APIのTealium SDKにある[`VisitorService`](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/)クラスを参照してください。