---
title: RemoteCommands モジュール
description: Tealium iQタグ管理のイベントからネイティブコードブロックをトリガーすることを可能にし、拡張機能とロードルールによって制御されます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/remote-commands/
---
[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)について詳しく学びましょう。

## 要件

* `webview`リモートコマンドを使用する場合、[Tag Management Dispatcherモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/)が必要です。


## インストール

Maven（推奨）または手動でRemoteCommands Dispatcherモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの`build.gradle`ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに、RemoteCommands DispatcherのMaven依存関係を追加します。これにより、Tealium Kotlinライブラリが取り込まれます。
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-remotecommand-dispatcher:1.4.0'
            implementation 'com.tealium:remotecommands:1.0.1'

      }
      ```

### 手動

RemoteCommands Dispatcherを手動でインストールするには：

1. Tealiumの[Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher)モジュールをダウンロードします。

2. ファイル`tealium-kotlin.remotecommand-1.4.0.aar`をプロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

3. プロジェクトモジュールの`build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.remotecommand-1.4.0', ext:'aar')
      }
      ```

## リモートコマンドのオプション

リモートコマンドには2つの構成オプションがあります：

* **JSONファイル**  
ベンダーの構成、データマッピング、イベントトリガーを含むJSONファイル。ローカルにロードするか、リモートでホストすることができます。
* **リモートコマンドタグ**  
ベンダーのAPIの構成オプションを提供するiQタグ管理のタグ（Tag Managementモジュールと共に使用）。

[リモートコマンドベンダー統合のリスト](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

### 例

リモートコマンドタグは、Tealium iQタグ管理、アプリ内のJSONファイル、またはリモートサーバー上のJSONファイルを介して構成可能です。リモートコマンドが構成され、モジュールがインストールされたら、初期化に次の行を追加します：





```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  // register the command
  remoteCommands?.add(remoteCommands);
}
```




```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  remoteCommands?.add(remoteCommands, filename = "FILENAME.json");
}
```





```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  remoteCommands?.add(remoteCommands, remoteUrl = "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json");
}
```





JSONファイルが構成され、アプリに追加されたかサーバーにホストされた後、さまざまな[JSONロードオプション](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#load-options)について学びましょう。


## データレイヤー

このモジュールによって追加の変数は導入されません。

## APIリファレンス

### `RemoteCommand()`
新しいリモートコマンドオブジェクトを作成し、`add`コマンドに渡す準備をします。

```kotlin
val remoteCommand = object : RemoteCommand("commandName", "description") {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, "ResponsePayload for webView RemoteCommand ${response.requestPayload}")
    }
}
```

| パラメータ     | 説明                                       | 例         |
|-------------- |-------------------------------------------------- |---------------- |
| `commandName`  | 必須のStringコマンド名                      | `"sample"`     |
| `description` | リモートコマンドのオプションのString説明 | `"testing RCs"` |


### `add()`

指定したリモートコマンドをTealiumに登録し、後でトリガーできるようにします。新しいリモートコマンドを追加する前にTealiumを初期化する必要があります。

```kotlin
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(remoteCommand)
}
```

以下は使用例です：

```kotlin
val remoteCommand = object : RemoteCommand("sample", "testing RCs") {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, "ResponsePayload for webView RemoteCommand ${response.requestPayload}")
    }
}

val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(remoteCommand)
}
```

### `remove()`
以前に登録したリモートコマンドを削除し、再度トリガーされるのを防ぎます。

```kotlin
val tealium = Tealium.create(instanceName, config) {
   remoteCommands?.remove("commandName")
}
```

### `removeAll`

以前に登録したすべてのリモートコマンドを削除します。

```kotlin
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.removeAll()
}
```


