---
title: AppDataモジュール
description: アプリバンドルに関する情報をデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/
---
## AppDataモジュールについて

AppDataモジュールは、トラッキングデータにアプリケーションの重要なメタデータを自動的にエンリッチメントするコレクターです。アプリバンドルからアプリケーション固有の情報を収集し、すべてのトラッキングイベントで利用できるようにします。

## インストール



AppDataモジュールは`prism-core`に含まれています。`build.gradle`ファイルに追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
```


AppDataモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```

代わりにPrismライブラリ全体をインストールするには、次のようにします。

```ruby
pod 'tealium-prism'
```



## 初期化

AppDataモジュールは、構成されると自動的に初期化されます。ほとんどの統合ではコードを変更する必要はありません。TealiumプラットフォームのUIでモジュールを構成するか、ローカルのJSON構成ファイルをアプリにバンドルします。

### 高度な構成：プログラムによる初期化

プラットフォーム構成またはローカルのJSON構成が存在しない場合でも、モジュールをデフォルト値で強制的に初期化するには、`TealiumConfig`の`modules`リストに追加します。モジュールを`TealiumConfig`に追加する方法は、テストを行う場合や、実行時に値を動的に構成する必要がある場合に便利です。



```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.appData(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                               Modules.appData(),
                               // other modules...
                           ])
```



## データレイヤー

モジュールが有効な間、各トラッキング呼び出しに次の変数が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `app_build` | アプリのビルド番号 | `"42"` |
| `app_memory_usage` | 現在のアプリのメモリ使用量（MB） | `775` |
| `app_name` | アプリケーションの表示名（iOS：`CFBundleName`、Android：`android:label`） | `"Digital Velocity"` |
| `app_rdns` | 逆引きDNS形式のアプリケーションID（iOS：`CFBundleIdentifier`、Android：マニフェストの`package`） | `"com.tealium.digitalvelocity"` |
| `app_uuid` | アプリがインストールされている間保持されるランダムな識別子。アプリをアンインストールするとリセットされます。 | `"4AB81234-C2A8-46DE-9AED-7ACE555521E0"` |
| `app_version` | ユーザー向けのアプリバージョン | `"1.0.0"` |