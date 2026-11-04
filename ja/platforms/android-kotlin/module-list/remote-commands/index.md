---
title: RemoteCommandsモジュール
description: 拡張機能と読み込みルールによって制御される、タグ管理のイベントからネイティブコードブロックをトリガーできるようにします。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/remote-commands/
---
[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)の詳細をご覧ください。

## 要件

* `webview`リモートコマンドを使用する場合は、[タグ管理Dispatcherモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/tag-management/)が必要です。
* RemoteCommandDispatcher `1.4.0`以降では、最低でも`com.tealium:kotlin-core:1.6.0`が必要です。

## インストール

Maven（推奨）または手動でRemoteCommands Dispatcherモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenリポジトリを追加します。
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの`build.gradle`ファイルに、RemoteCommands DispatcherのMaven依存関係を追加します。これにより、Tealium Kotlinライブラリが取り込まれます。
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-remotecommand-dispatcher:1.4.0'
            implementation 'com.tealium:remotecommands:1.0.1'
      }
      ```

### 手動

RemoteCommands Dispatcherを手動でインストールするには、次の手順を実行します。

1. Tealiumの[Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher)モジュールをダウンロードします。

2. `tealium-kotlin.remotecommand-1.4.0.aar`ファイルを、プロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

3. プロジェクトモジュールの`build.gradle`ファイルに、Tealiumライブラリの依存関係を追加します。
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.remotecommand-1.4.0', ext:'aar')
      }
      ```

## リモートコマンドのオプション

リモートコマンドには、次の2つの構成オプションがあります。

* **JSONファイル**  
ベンダー構成、データマッピング、イベントトリガーを含むJSONファイルを、ローカルまたはリモートホストから読み込みます。
* **リモートコマンドタグ**  
ベンダーAPIの構成オプションを提供するタグ管理内のタグです（タグ管理モジュールで使用）。

[リモートコマンドのベンダー統合一覧](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

### 例

リモートコマンドタグは、タグ管理、アプリ内のJSONファイル、またはリモートサーバー上のJSONファイルを使用して構成できます。リモートコマンドを構成してモジュールをインストールしたら、初期化処理に次の行を追加します。





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





JSONファイルを構成し、アプリに追加するかサーバー上でホストした後、各種の[JSON読み込みオプション](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#load-options)について確認してください。

## データレイヤー

このモジュールによって追加される変数はありません。

## APIリファレンス

### `RemoteCommand()`
`add`コマンドに渡す準備が整った、新しいリモートコマンドオブジェクトを作成します。

```kotlin
val remoteCommand = object : RemoteCommand("commandName", "description") {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, "ResponsePayload for webView RemoteCommand ${response.requestPayload}")
    }
}
```

| パラメータ | 説明 | 例 |
|-------------- |-------------------------------------------------- |---------------- |
| `commandName` | 必須の文字列型コマンド名 | `"sample"` |
| `description` | リモートコマンドの任意の文字列型説明 | `"testing RCs"` |

### `add()`

指定したリモートコマンドをTealiumに登録し、後でトリガーできるようにします。新しいリモートコマンドを追加する前に、Tealiumを初期化しておく必要があります。

```kotlin
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(remoteCommand)
}
```

使用例を次に示します。

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
以前に登録したリモートコマンドを削除し、再度トリガーされないようにします。

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