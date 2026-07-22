---
title: コレクトモジュール
description: イベントをTealium Customer Data Hubに送信します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collect/
---
## 使用法

コレクトモジュールは、トラッキングコールをTealium Customer Data Hubにディスパッチします。このモジュールは、サーバーサイドの製品を使用している場合に強く推奨されます。

また、Tealium iQをお持ちの場合は、[Tag Management Dispatcher](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/)とパートナーシップを組んでTealium Collectタグを使用してください。

## インストール

Collect Dispatcherモジュールは、Maven（推奨）または手動でインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとCollect DispatcherのMaven依存関係を追加します
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-collect-dispatcher:1.1.1'
      }
      ```

### 手動

Collect Dispatcherを手動でインストールするには：

1. Tealiumの[Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.collect-1.1.1.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. Tealiumライブラリの依存関係をプロジェクトモジュールの `build.gradle` ファイルに追加します：
    ```groovy
    dependencies {
        implementation(name:'tealium-kotlin.collect-1.1.1', ext:'aar')
    }
    ```

<blockquote>
Collect Dispatcherは主要なTealium Kotlin SDKに依存しているため、[インストール手順](https://docs.tealium.com/ja/platforms/android-kotlin/install/)に従ってこれも利用可能にすることを確認してください。
</blockquote>


## 構成オプション

TealiumConfigオブジェクトを作成する際に、次の構成を使用して、Collect Dispatcherがデータを送信するURLを構成します：

```kotlin
val config = TealiumConfig(...)
config.overrideCollectUrl = "https://your.endpoint.com/event"
config.overrideCollectBatchUrl = "https://your.endpoint.com/bulk-event"
```

個々のイベントまたは[バッチ処理されたイベント](https://docs.tealium.com/ja/platforms/getting-started-mobile/event-batching/)が送信されるエンドポイントを構成します。

CNAMEまたはデータセンター固有の要件を使用するデプロイメントの場合は、ドメインを上書きし、Tealiumが定義したエンドポイントを保持します。次の例では、個々のイベントは `https://cname.tealiumiq.com/event` に、バッチ処理されたイベントは `https://cname.tealiumiq.com/bulk-event` に行きます：

```kotlin
val config = TealiumConfig(...)
config.overrideCollectDomain = "cname.tealiumiq.com"
```

`TealiumConfig` オブジェクトで使用されるTealiumプロファイルとは異なるTealiumプロファイルにイベントを送信する必要がある場合は、次のようにこれを上書きすることができます - これはイベントペイロードの `tealium_profile` キーの値を変更する効果があります：
```kotlin
val config = TealiumConfig(..., profile="android", ...)
config.overrideCollectProfile = "main"
```

