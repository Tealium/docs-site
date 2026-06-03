---
title: タグ管理ディスパッチャーモジュール
description: JavaScriptを実行するために非表示のWebViewインスタンスを使用する、Universal Tag (`utag.js`)のクライアントサイド実装です。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/
---
## 使用方法

タグ管理ディスパッチャーモジュールは、JavaScriptを実行するために非表示の`WebView`インスタンスを使用する、Universal Tag (`utag.js`)のクライアントサイド実装です。このディスパッチャーは、Tealium iQタグ管理を使用するアプリで必要とされます。

## インストール

Maven（推奨）または手動でタグ管理ディスパッチャーモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルに、次のMavenリポジトリを追加します：  
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```
2. プロジェクトモジュールの`build.gradle`ファイルに、Tealiumライブラリとタグ管理ディスパッチャーのMaven依存関係を追加します
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-tagmanagement-dispatcher:1.2.2&#39;
      }
      ```

### 手動

タグ管理ディスパッチャーを手動でインストールするには：

1. Tealiumの[タグ管理ディスパッチャー](https://github.com/Tealium/tealium-kotlin/tree/master/tagmanagementdispatcher)モジュールをダウンロードします。

2. ファイル`tealium-kotlin.tagmanagement-1.2.1.aar`をプロジェクトの`&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`ディレクトリにコピーします。

3. プロジェクトモジュールの`build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.tagmanagement-1.2.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## 構成オプション

次の`TealiumConfig`オプションを使用して、タグ管理ディスパッチャーでUniversal Tag (`utag.js`)をダウンロードして実行するために使用されるURLを上書きします：
```kotlin
val config = TealiumConfig(...)

config.overrideTagManagementUrl = &#34;https://yourcustomdomain.com&#34;
```

タグ管理のwebviewに送信される`remote_api`イベントを有効または無効にします。これにより、webviewによってトリガーされるリモートコマンドが無効になります。これらはデフォルトで有効になっています。

```kotlin
val config = TealiumConfig(...)

config.remoteApiEnabled = false
```

