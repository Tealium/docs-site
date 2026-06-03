---
title: ビジターサービスモジュール
description: 現在のビジターの最新のプロファイルを取得します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/visitor-service/
---
## 使用法

ビジターサービスモジュールは、ネイティブモバイルアプリに[データレイヤーのエンリッチメント]()機能を提供します。

このモジュールの使用には、Tealium AudienceStreamのライセンスが必要です。取得したビジタープロファイルを使用して、アプリケーション全体の顧客体験やデータレイヤーをエンリッチメントします。

## インストール

ビジターサービスモジュールは、Maven（推奨）または手動でインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとビジターサービスモジュールのMaven依存関係を追加します
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-visitor-service:1.2.0&#39;
      }
      ```

### 手動

ビジターサービスモジュールを手動でインストールするには：

1. Tealiumの[ビジターサービス](https://github.com/Tealium/tealium-kotlin/tree/master/visitorservice)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.visitorservice-1.2.0.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.visitorservice-1.2.0&#39;, ext:&#39;aar&#39;)
      }
      ```

Collect DispatcherはメインのTealium Kotlin SDKに依存しているので、[インストール手順](/ja/platforms/android-kotlin/install)に従ってこれも利用可能にすることを確認してください。

## ビジタープロファイルデータ

現在のビジターデータを利用するには、最新のビジタープロファイルが更新されるたびに受け取るためのデリゲートオブジェクトを登録する必要があります：

```java
instance = Tealium.create(&#34;main&#34;, config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev(&#34;--&#34;, &#34;VisitorProfile updated: $visitorProfile&#34;)
        }
    })
}
```

VisitorProfileオブジェクトは、ビジターに関連する多くのフィールドにアクセスできます - 以下に利用可能なプロパティを概説します：

| パラメータ | プロパティ |  値 |
| --- | --- | --- |
| `arraysOfBooleans` | key: String, value: List\&lt;Boolean\&gt; | `key: &#34;5129&#34;, value: listOf(true,false,true,true)` |
| `arraysOfNumbers` | key: String, value: List\&lt;Double\&gt;| `key: &#34;57&#34;, value: listOf(4.82125, 16.8, 0.5714285714285714)` |
| `arraysOfStrings` | key: String, value: List\&lt;String\&gt; | `key: &#34;5213&#34;, value: listOf(&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;)` |
| `audiences` | key: String, name: String | `key: &#34;tealiummobile_demo_103&#34;, name: &#34;Kotlin Users&#34;` |
| `badges` | key: String, value: Boolean | `key: &#34;2815&#34;, value: true` |
| `booleans` | key: String, value: Boolean | `key: &#34;4868&#34;, value: true `|
| `currentVisit` | 現在の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesは含まれていません。 | `CurrentVisit` |
| `dates` | key: String, value: Long | `key: &#34;22&#34;, value: 1567120112000` |
| `numbers` | key: String, value: Double | `key: &#34;5728&#34;, value: 4.82125` |
| `setsOfStrings` | key: String, value: Set\&lt;String\&gt; | `key: &#34;5211&#34;, value: setOf(&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;)` |
| `strings` | key: String, value: String | `key: &#34;5380&#34;, value: &#34;green shirts&#34;` |
| `tallies` | key: String, value: Map&lt;String, Double&gt; |  `key: &#34;57&#34;, mapOf(&#34;category 1&#34; to 2.0, &#34;category 2&#34; to 1.0)` |


以下は、ビジタープロファイルが取得された後にそれをどのように操作するかの基本的な例です。キー名はアカウント/プロファイルごとに異なります。
```java
val returningVisitor = visitorProfile.badges?.get(&#34;returning_visitor&#34;)
returningVisitor?.let {
    if (returningVisitor == true) {
        val ltv = visitorProfile.numbers?.get(&#34;lifetime_value&#34;)
        // take action
    }
}
```


## 構成オプション

TealiumConfigオブジェクトを作成する際に、以下の構成を使用してビジタープロファイルを取得するためのURLを構成します：

### ビジターサービスURLの上書き

ビジタープロファイルの更新を取得する際に使用するURLを構成します。

参照：[`TealiumConfig.overrideVisitorServiceUrl`](/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceurl). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = &#34;https://your.preferred.visitor-service.com&#34;
```

デフォルト：`https://visitor-service.tealiumiq.com/{ACCOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}`

### ビジターサービスプロファイルの上書き

ビジタープロファイルの更新を取得する際に使用するTealiumプロファイルを構成します。参照：[`TealiumConfig.overrideVisitorServiceProfile`](/ja/platforms/android-kotlin/api/visitor-service/#overridevisitorserviceprofile). 

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = &#34;someOtherTealiumProfile&#34;
```

### ビジタープロファイルの更新間隔

最新のVisitorProfileデータを取得するための呼び出し間隔（秒）を構成します。参照：[`TealiumConfig.visitorServiceRefreshInterval`](/ja/platforms/android-kotlin/api/visitor-service/#visitorservicerefreshinterval). 

デフォルト：300（5分）

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30 minutes
```

## APIリファレンス

ビジターサービスモジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android APIの[`VisitorService`](/ja/platforms/android-kotlin/api/visitor-service/)クラスを参照してください。

