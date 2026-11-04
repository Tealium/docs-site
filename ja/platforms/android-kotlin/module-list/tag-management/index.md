---
title: タグ管理ディスパッチャーモジュール
description: JavaScript の実行に非表示の WebView インスタンスを使用する Universal Tag（`utag.js`）のクライアントサイド実装。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/
---
## 使用方法

タグ管理ディスパッチャーモジュールは、JavaScript の実行に非表示の `WebView` インスタンスを使用する Universal Tag（`utag.js`）のクライアントサイド実装です。タグ管理を使用するアプリでは、このディスパッチャーが必要です。

## インストール

Maven（推奨）を使用するか、手動でタグ管理ディスパッチャーモジュールをインストールします。

### Maven

Maven を使用してモジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の `build.gradle` ファイルに、次の Maven リポジトリを追加します。  
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリとタグ管理ディスパッチャーの Maven 依存関係を追加します。
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-tagmanagement-dispatcher:1.2.2'
      }
      ```

### 手動

タグ管理ディスパッチャーを手動でインストールするには、次の手順を実行します。

1. Tealium の[タグ管理ディスパッチャー](https://github.com/Tealium/tealium-kotlin/tree/master/tagmanagementdispatcher)モジュールをダウンロードします。

2. `tealium-kotlin.tagmanagement-1.2.1.aar` ファイルを、プロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリの依存関係を追加します。
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.tagmanagement-1.2.1', ext:'aar')
      }
      ```

## 構成オプション

次の `TealiumConfig` オプションを使用して、タグ管理ディスパッチャーが Universal Tag（`utag.js`）をダウンロードして実行する際に使用する URL を上書きします。

```kotlin
val config = TealiumConfig(...)

config.overrideTagManagementUrl = "https://yourcustomdomain.com"
```

タグ管理 WebView に送信される `remote_api` イベントを有効または無効にします。これにより、WebView によってトリガーされるリモートコマンドを実質的に無効にできます。デフォルトでは有効になっています。

```kotlin
val config = TealiumConfig(...)

config.remoteApiEnabled = false
```