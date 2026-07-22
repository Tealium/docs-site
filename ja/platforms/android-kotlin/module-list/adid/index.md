---
title: 広告識別子モジュール
description: デバイスの "広告識別子" (ADID) を使用して、ディスプレイ広告ネットワークとのインタラクションを識別する能力を提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/adid/
---
## 要件

* [Google Play Services SDK](https://developers.google.com/android/guides/setup)

## インストール

Maven（推奨）または手動で広告識別子モジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、次のMaven依存関係を追加します：
      ```groovy
      dependencies{
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-ad-identifier:1.1.1'
      }
      ```

### 手動

広告識別子モジュールを手動でインストールするには：

1. Tealiumの [AdIdentifier](https://github.com/Tealium/tealium-kotlin/tree/master/adidentifier) モジュールをダウンロードします。

2. トップレベルの `build.gradle` ファイルで、次のことを確認します：  
      ```groovy
      allprojects {
            repositories {
            mavenCentral()
            flatDir {
                  dirs 'libs'
            }
            }
      }
      ```

3. ファイル `tealium.adidentifier-1.1.1.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

4. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation (name:'tealium-kotlin.adidentifier-1.1.1', ext:'aar')
      }
      ```

## 初期化

次の例に示すように、広告識別子モジュールを初期化します：

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              modules = mutableSetOf(Modules.AdIdentifier), // Ad Identifier module
              dispatchers = mutableSetOf(Dispatchers.Collect,
              Dispatchers.TagManagement,
              Dispatchers.RemoteCommands)
)
```

## データレイヤー

広告識別子モジュールは、次の変数をデータレイヤーに追加します：

| 変数 | タイプ | 説明 | 例 |
| --- | --- | --- | --- |     
| `google_adid` | `String` | Google広告識別子 | `ca-app-pub-0123456789012345~0123456789` |
| `google_limit_ad_tracking` | `Boolean` | デバイスで広告トラッキングの制限が有効になっている場合は `true`、それ以外の場合は `false`  | `true` |

## APIリファレンス

### `removeAdInfo()`

データレイヤーから保存された広告識別子文字列を削除します。

```kotlin
tealium?.adIdentifier?.removeAdInfo()
```

### `removeAppSetIdInfo()`

データレイヤーから保存されたApp Setデータを削除します。

```kotlin
tealium?.adIdentifier?.removeAppSetIdInfo()
```
