---
title: AppDataモジュール
description: アプリバンドルに関する情報をデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/
---
## AppDataモジュールについて

AppDataモジュールは、アプリケーションのメタデータに必要な情報を自動的に追加するコレクターです。アプリバンドルからアプリケーション固有の情報を収集し、すべてのトラッキングイベントで利用可能にします。

## インストール



`build.gradle`ファイルに`prism-appdata`依存関係を追加してください：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-appdata")
```


AppDataモジュールは`TealiumPrismCore`に含まれています。Swift Package Manager依存関係としてリポジトリURL`https://github.com/Tealium/tealium-prism-swift`を使用して追加するか、CocoaPodsのためにPodfileに追加してください：

```ruby
pod 'tealium-prism/Core'
```

完全なPrismライブラリをインストールする場合：

```ruby
pod 'tealium-prism'
```



## 初期化

AppDataモジュールは構成時に自動的に初期化されます。ほとんどの統合ではコード変更は必要ありません。TealiumプラットフォームUIでモジュールを構成するか、アプリにローカルJSON構成ファイルをバンドルしてください。

### 上級者向け：プログラムによる初期化

プラットフォームまたはローカルJSON構成が存在しない場合でも、デフォルト値でモジュールを初期化するには、`TealiumConfig`の`modules`リストに追加します。`TealiumConfig`にモジュールを追加することは、テスト時やランタイムで動的に値を構成する必要がある場合に便利です。



```kotlin
val config = TealiumConfig.Builder(
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.appData(),
        // 他のモジュール...
    )
).build()
```


```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                               Modules.appData(),
                               // 他のモジュール...
                           ])
```



## データレイヤー

モジュールが有効な間、以下の変数が各トラッキングコールに追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `app_build` | アプリのビルド番号 | `"42"` |
| `app_memory_usage` | 現在のアプリメモリ使用量 | `"775 MB"` |
| `app_name` | アプリケーションの表示名（iOS: `CFBundleName`; Android: `android:label`） | `"Digital Velocity"` |
| `app_rdns` | 逆DNSアプリケーションID（iOS: `CFBundleIdentifier`; Android: マニフェスト `package`） | `"com.tealium.digitalvelocity"` |
| `app_uuid` | アプリインストールの寿命にわたって持続するランダム識別子。アプリがアンインストールされるとリセットされます。 | `"4AB81234-C2A8-46DE-9AED-7ACE555521E0"` |
| `app_version` | ユーザーに向けたアプリのバージョン | `"1.0.0"` |