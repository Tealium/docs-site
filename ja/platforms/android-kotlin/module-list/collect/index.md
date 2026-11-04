---
title: Collect モジュール
description: Tealium Customer Data Hub にイベントを送信します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collect/
---
## 使用方法

Collect モジュールは、トラッキング呼び出しを Tealium Customer Data Hub に送信します。サーバーサイド製品を使用している場合は、このモジュールの使用を強く推奨します。

または、Tag Management を使用している場合は、[Tag Management Dispatcher](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/) と組み合わせて Tealium Collect タグを使用してください。

## インストール

Maven（推奨）または手動で Collect Dispatcher モジュールをインストールします。

### Maven

Maven を使用してモジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の `build.gradle` ファイルに、次の Maven リポジトリを追加します。
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリと Collect Dispatcher の Maven 依存関係を追加します。
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-collect-dispatcher:1.1.1'
      }
      ```

### 手動

Collect Dispatcher を手動でインストールするには、次の手順を実行します。

1. Tealium の [Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher) モジュールをダウンロードします。

2. `tealium-kotlin.collect-1.1.1.aar` ファイルをプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリの依存関係を追加します。
    ```groovy
    dependencies {
        implementation(name:'tealium-kotlin.collect-1.1.1', ext:'aar')
    }
    ```

<blockquote>
Collect Dispatcher はメインの Tealium Kotlin SDK に依存しているため、[インストール手順](https://docs.tealium.com/ja/platforms/android-kotlin/install/)に従って、この SDK も利用できるようにしてください。
</blockquote>


## 構成オプション

TealiumConfig オブジェクトを作成する際に次の構成を使用して、Collect Dispatcher がデータを送信する URL を構成します。

```kotlin
val config = TealiumConfig(...)
config.overrideCollectUrl = "https://your.endpoint.com/event"
config.overrideCollectBatchUrl = "https://your.endpoint.com/bulk-event"
```

個別のイベントまたは[バッチ処理されたイベント](https://docs.tealium.com/ja/platforms/getting-started-mobile/event-batching/)の送信先となるエンドポイントを構成します。

CNAME またはデータセンター固有の要件を使用するデプロイメントでは、ドメインをオーバーライドし、Tealium が定義したエンドポイントを維持します。次の例では、個別のイベントは `https://cname.tealiumiq.com/event` に、バッチ処理されたイベントは `https://cname.tealiumiq.com/bulk-event` に送信されます。

```kotlin
val config = TealiumConfig(...)
config.overrideCollectDomain = "cname.tealiumiq.com"
```

`TealiumConfig` オブジェクトで使用しているものとは異なる Tealium プロファイルにイベントを送信する必要がある場合は、次のようにオーバーライドできます。これにより、イベントペイロード内の `tealium_profile` キーの値が変更されます。

```kotlin
val config = TealiumConfig(..., profile="android", ...)
config.overrideCollectProfile = "main"
```