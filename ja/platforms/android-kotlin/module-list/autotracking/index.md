---
title: AutoTrackingモジュール
description: 画面のビューを自動的に追跡します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/
---
AutoTrackingモジュールは、アプリ内で追加のコードを書くことなく、一般的なイベントの自動追跡をアプリに追加します。

## 仕組み

ビルドと初期化にAutoTrackingモジュールを含めることで、アプリに自動追跡を追加します。このモジュールには、追跡する画面とその命名方法を制御するためのいくつかのオプションがあります。

Autotrackingモジュールには2つの追跡モードがあります：

* **フルトラッキング**  
すべての画面ビューを自動的に追跡し、画面を省略したり画面名を上書きするオプションがあります。
* **部分的な追跡**  
注釈が付けられたアクティビティのみを追跡し、画面名を上書きするオプションがあります。

### 注釈

以下の注釈を使用して、モジュールの動作を調整します：

* **イベント名の上書き**  
この注釈を使用して、デフォルトの画面名を上書きします。

      ```kotlin
      @Autotracked(name = &#34;MyCustomName&#34;)
      private class AnnotatedActivityWithOverride : Activity()
      ```
* **追跡に含める**  
部分的な追跡モードでは、この注釈を使用して特定のアクティビティを追跡します。

      ```kotlin
      @Autotracked()
      private class AnnotatedActivity : Activity()
      ```
* **追跡から省略**  
フルトラッキングモードでは、この注釈を使用してアクティビティを自動的に追跡しないようにします。

      ```kotlin
      @Autotracked(track = false)
      private class AnnotatedActivityWithoutTracking : Activity()
      ```

### フルトラッキング

フルトラッキングモードは、`Application.ActivityLifecycleCallbacks`を使用して新しいアクティビティがフォーカスに入ったときを判断し、`TealiumView`イベントをトリガーします。イベントでは、`tealium_event`はクラス名に構成されますが、名前から&#34;Activity&#34;が削除されます。

画面名を上書きするための注釈を使用するか、アクティビティの追跡を防ぐために注釈を使用します。

[Android Developers: The Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)から詳細を学びましょう。

### 部分的な追跡

部分的な追跡モードは、注釈に依存して追跡するアクティビティを決定します。注釈を使用して追跡するアクティビティを指定するか、画面名を上書きします。

### ブロックリスト

ブロックリストは、文字列の単一配列を含むJSONファイルです。文字列は、自動追跡から省略するアクティビティを表します。ブロックリストにある文字列がアクティビティ名のどこかに現れると、それは追跡されません。文字列の比較は大文字と小文字を区別しません。

例えば、&#34;Settings&#34;や&#34;Profile&#34;という文字列を含むアクティビティを追跡したくない場合、ブロックリストには以下のように含めることができます：

```json
[
  &#34;settings&#34;, &#34;profile&#34;
]
```

ブロックリストファイルは、アプリの`assets`ディレクトリにローカルに保存するか、URLとしてリモートにホストすることができます。

ブロックリストを使用するためには、以下の`TealiumConfig`プロパティのいずれかを使用します：

* [`autoTrackingBlocklistFilename`](/ja/platforms/android-kotlin/api/tealium-config/#autotrackingblocklistfilename)
* [`autoTrackingBlocklistUrl`](/ja/platforms/android-kotlin/api/tealium-config/#autotrackingblocklisturl)

## インストール

Maven（推奨）または手動でモジュールをインストールします。

### Maven

Mavenを使用してAutoTracking Trackingモジュールをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルに、以下のMavenリポジトリを追加します：
      ```groovy
      allprojects {
          repositories {
            mavenCentral()
            maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
            }
          }
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに、以下のMaven依存関係を追加します：
      ```groovy
      dependencies {
          implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
          implementation &#39;com.tealium:kotlin-autotracking:1.0.1&#39;
      }
      ```

### 手動

AutoTrackingモジュールを手動でインストールするには、以下の手順を実行します：

1. Tealiumの[AutoTracking Module](https://github.com/Tealium/tealium-kotlin/tree/master/autotracking/)モジュールをダウンロードします。

2. ファイル`tealium-kotlin.autotracking-1.0.1.aar`をプロジェクトの`&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`ディレクトリにコピーします。

3. プロジェクトモジュールの`build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.autotracking-1.0.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## 初期化

AutoTrackingモジュールを初期化するには、`TealiumConfig`のモジュールリストに追加し、追跡モードを構成します。

AutoTrackingモジュールを初期化する例：

```kotlin
val config = TealiumConfig(application,
              &#34;ACCOUNT&#34;,
              &#34;PROFILE&#34;,
              ENVIRONMENT,
              modules = mutableSetOf(Modules.AutoTracking)
              ).apply {
                autoTrackingMode = AutoTrackingMode.ANNOTATED
              }
```

より多くのオプションについては、[`TealiumConfig.autoTrackingMode`](/ja/platforms/android-kotlin/api/tealium-config/#autotrackingmode)を参照してください。

## データレイヤー

以下の変数は、このモジュールによってトリガーされる各追跡呼び出しに含まれます：

| 変数名 | タイプ     | 説明                                            | 例 |
|:--------------|:---------|:-------------------------------------------------------|:--------|
| `autotracked` | `String` | Autotrackingモジュールによって追跡されたすべてのイベントに構成されます。 | `true`  |

### カスタムデータ

デフォルトでは、自動的に追跡されるイベントにはコンテキスト変数は含まれません。AutoTrackingモジュールからのイベントにコンテキストデータを追加するには、`TealiumConfig`で構成されたグローバルデリゲートを使用して、各追跡アクティビティのカスタムデータオブジェクトのマップを返します。これはモジュールによって追跡されるすべてのイベントで実行されます。

デリゲートを構成するには：

```kotlin
config.autoTrackingCollectorDelegate = object: ActivityDataCollector {
    override fun onCollectActivityData(activityName: String): Map&lt;String, Any&gt;? {
        when (activityName) {
            &#34;some_activity&#34; -&gt; return mapOf(&#34;some_key&#34; to &#34;some_value&#34;)
            else -&gt; return null
        }
    }
}
```

または、特定のアクティビティにコンテキストデータを追加するには、`Activity`が同じ`ActivityDataCollector`インターフェースを実装するようにします。

```kotlin
class ActivityWithDataCollector : Activity(), ActivityDataCollector {
    override fun onCollectActivityData(activityName: String): Map&lt;String, Any&gt;? {
        return mapOf(&#34;some_key&#34; to &#34;some_value&#34;)
    }
}
```

各追跡アクティビティで両方のデリゲートが実行されるため、グローバルレベルで共通データを追加し、`onCollectActivityData`メソッドを使用して特定のデータを追加します。

## APIリファレンス

* [`TealiumConfig`](/ja/platforms/android-kotlin/api/tealium-config/)

