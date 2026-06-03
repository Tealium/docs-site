---
title: Install Referrerモジュールのインストール
description: アプリのインストールリファラー情報（利用可能な場合）を自動的に収集し、それをデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/install-referrer/
---
## インストール

Install ReferrerモジュールをMavenまたは手動でインストールします。

### Maven

MavenでInstall Referrerモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```  
2. プロジェクトモジュールの `build.gradle` ファイルに、次のMaven依存関係を追加します：
      ```groovy
      dependencies{
            // この参照がない場合のみ必要
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-install-referrer:1.1.1&#39;
            // この参照がすでに存在しない場合、またはライフサイクルの追跡が必要な場合のみ必要
            implementation &#39;com.tealium:kotlin-lifecycle:1.2.0&#39;
            // GoogleのInstall Referrer API
            implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
      }
      ```  
このモジュールの依存関係である[Google Install Referrer API](https://developer.android.com/google/play/installreferrer/library)は自動的に追加されません。ビルドにモジュールを追加してください。


### 手動

Install Referrerモジュールを手動でインストールするには：

1. Tealiumの[Install Referrer](https://github.com/Tealium/tealium-kotlin/tree/master/installreferrer)モジュールをダウンロードします。

2. トップレベルの `build.gradle` ファイルで、以下を確認します：  
      ```groovy
      allprojects {
            repositories {
            mavenCentral()
            flatDir {
                  dirs &#39;libs&#39;
            }
            }
      }
      ```  

3. ファイル `tealium-kotlin.installreferrer-1.1.1.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

4. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            // この参照がすでに存在しない場合のみ必要
            implementation(name:&#39;tealium-kotlin-1.6.0&#39;, ext:&#39;aar&#39;)
            implementation(name:&#39;tealium-kotlin.installreferrer-1.1.1&#39;, ext:&#39;aar&#39;)
            // この参照がすでに存在しない場合、またはライフサイクルの追跡が必要な場合のみ必要
            implementation(name:&#39;tealium-kotlin.lifecycle-1.2.0&#39;, ext:&#39;aar&#39;)
            // GoogleのInstall Referrer API
            implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
      }
      ```

## データレイヤー

Google Playから取得した以下のリファラーデータを期待します

```
&#34;install_referrer&#34; - インストールパッケージのリファラーURL
&#34;install_referrer_begin_timestamp&#34; - リファラルクリックが発生したタイムスタンプ（秒）
&#34;install_referrer_click_timestamp&#34; - インストールが開始されたタイムスタンプ（秒）
```

## 追加の考慮事項

**保存されたリファラーの削除**  
保存されたインストールリファラー文字列を削除するには、Tealiumデータレイヤーの `remove()` メソッドを呼び出します。
```kotlin
// データレイヤーから以下のキーの一つまたはすべてを削除します
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER)
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER_BEGIN_TIMESTAMP)
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER_CLICK_TIMESTAMP)
```
