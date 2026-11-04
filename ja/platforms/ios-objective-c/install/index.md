---
title: インストール
description: iOS（Objective-C）向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/install/
---

<blockquote>
このセクションでは、以前のiOSライブラリであるObjective-C版について説明します。macOS、iOS、watchOS、tvOSなどでは、[Swift](https://docs.tealium.com/ja/platforms/ios-swift/)が推奨されるプログラミング言語です。Swiftコードは、同じプロジェクト内の既存のObjective-Cファイルと共存でき、Objective-C APIにも完全にアクセスできるため、簡単に導入できます。
</blockquote>


## 要件

* Xcode 7.0以降
* iOS 8.1以降
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Tealiumライブラリ、トラッキングメソッド、および実装のベストプラクティスを理解するために、Tealium for iOSの[サンプルアプリ](https://github.com/Tealium/tealium-ios/tree/master/Samples)を参照してください。

Tealiumの実装をアプリの他の部分から分離するため、`TealiumHelper`クラスの使用をお勧めします。これにより、初期化やトラッキング呼び出しを行うための単一のエントリポイントを作成できます。また、個々の`ViewController`やヘッダー／メソッドファイルを変更することなく、ヘルパーファイル内のコードだけを更新できます。

- [Objective-C向けTealiumHelper](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_ObjC/UIKitCatalog/TealiumHelper.m)
- [Swift向けTealiumHelper](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift)


<blockquote>
iOS向けのTealiumクラスとメソッドの完全な一覧については、[TealiumIOS API](https://tealium.github.io/tealium-ios/)を参照してください。
</blockquote>


## インストール

CocoaPods、Carthage、または手動でiOS（Objective-C）向けTealium SDKをインストールします。

### CocoaPods

CocoaPodsを使用して、アプリにiOS（Objective-C）向けTealiumをインストールするには（推奨）：

1. Podfileに次の依存関係を追加します。
      ```perl
      pod "TealiumIOS"
      ```

2. ファイルを保存し、プロジェクトディレクトリで次のコマンドを実行します。

      ```perl
      pod install --repo-update
      ```

3. 作成された`.xcworkspace`ファイルを使用して、アプリのビルドを続行します。`.xcworkspace`ファイルを使用しない場合、アプリを正しくビルドできません。

### Carthage

Carthageを使用して、アプリにiOS（Objective-C）向けTealiumをインストールするには：

1. Cartfileに次の内容を追加します。  
      ```perl
      github "tealium/tealium-ios"
      ```

2. フレームワークをダウンロードして展開するには、次のコマンドを実行します。  
      ```perl
      carthage update --platform ios --use-xcframeworks
      ```
      
<blockquote>
必ず`--use-xcframeworks`フラグを使用してください。使用しない場合、ビルドが失敗します。これには[Carthage 0.38.0](https://github.com/Carthage/Carthage/releases/tag/0.38.0)が必要です。
</blockquote>


3. ビルド時に必要なフレームワークが自動的にコピーされるように、CarthageがXcodeプロジェクトに[正しく統合されている](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)ことを確認します。

### 手動

アプリにiOS（Objective-C）向けTealiumを手動でインストールするには：

1. `TealiumIOS.xcframework`をプロジェクトに追加します。

2. 表示されたダイアログボックスで、フレームワークをプロジェクトにコピーします。

3. ターゲットで、**General > Frameworks, Libraries & Embedded Content**に移動し、「Embed & Sign」オプションを選択して`TealiumIOS.xcframework`を追加します。

<blockquote>
Swiftプロジェクトの場合は、**Build Settings > Swift Compiler > Objective-C Bridging Header**オプションに移動し、`TealiumIOSBridgingHeader.h`ファイルを指定します。
</blockquote>



## 初期化

Application Delegate、またはヘルパークラスのセットアップメソッド内で、次の初期化コードを使用します。  



```swift
// set your account, profile, and environment
let tealConfig = TEALConfiguration.init(account: "ACCOUNT",
                                        profile: "PROFILE",
                                    environment: "ENVIRONMENT",
                                     datasource: "DATASOURCE")

// Initialize with a unique key for this instance
guard let tealium = Tealium.newInstanceForKey("INSTANCE", configuration: tealConfig) else {
     // Any additional failure response here           
     return
}
```



```obj-c
// import area
@import TealiumIOS;

// Set your account, profile, and environment
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@"ACCOUNT"
                          profile:@"PROFILE"
                          environment:@"ENVIRONMENT"
                          datasource:@"DATASOURCE"];

// Initialize with a unique key for this instance
Tealium *tealium = [Tealium newInstanceForKey:@"INSTANCE" configuration:tealConfig]; 
```



ログレベルは、デフォルトではiQアカウントのパブリッシュ構成に基づいて構成されます。この構成を上書きするには、TEALConfigurationインスタンスの`logLevel`プロパティを構成します。



```swift
// Set the log verbosity to errors only
tealConfig.logLevel = .prod
```



```obj-c
// Set the log verbosity to maximum
[tealConfig setLogLevel: TEALLogLevelDev];
```



トラッキングを開始する前に、Tealiumインスタンスを次のパラメータで構成する必要があります。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ"` |
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` | `String` | （任意）データソースキー | `"abc123"` |
| `instance` | `String` | インスタンスの一意の名前（複数のインスタンスをサポート） | `"tealium_main"` |