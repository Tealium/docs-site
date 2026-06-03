---
title: インストール
description: Tealium SDKをiOS（Objective-C）にインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/install/
---
このセクションでは、以前のiOSライブラリ、Objective-Cについて説明します。[Swift](/ja/platforms/ios-swift/)はmacOS、iOS、watchOS、tvOSなどで推奨されるプログラミング言語です。Swiftのコードは既存のObjective-Cファイルと同じプロジェクト内で共存し、Objective-C APIに完全にアクセスできるため、採用が容易です。

## 要件

* Xcode 7.0&#43;
* iOS 8.1&#43;
* [Tealium iQ Mobile Profile]()
* [Tealium Customer Data Hub account]()

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、iOS用Tealiumの[sample apps](https://github.com/Tealium/tealium-ios/tree/master/Samples)を探索してみてください。

アプリの残りの部分からTealiumの実装を抽象化するために、`TealiumHelper`クラスの使用をお勧めします。これにより、初期化およびトラッキング呼び出しを行う単一のエントリポイントが提供されます。また、ヘルパーファイルのコードを更新し、すべての`ViewController`またはヘッダー/メソッドファイルで更新する必要がなくなります。

- [Objective-C用TealiumHelper](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_ObjC/UIKitCatalog/TealiumHelper.m)
- [Swift用TealiumHelper](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift)

iOS用のTealiumクラスとメソッドの完全なリストについては、[TealiumIOS API](https://tealium.github.io/tealium-ios/)を参照してください。

## インストール

CocoaPods、Carthage、または手動でiOS（Objective-C）用のTealium SDKをインストールします。

### CocoaPods

アプリにiOS（Objective-C）用のTealiumをCocoaPods（推奨）でインストールするには：

1. Podfileに以下の依存関係を追加します：
      ```perl
      pod &#34;TealiumIOS&#34;
      ```

2. ファイルを保存し、プロジェクトディレクトリで以下を実行します：

      ```perl
      pod install --repo-update
      ```

3. 作成された`.xcworkspace`ファイルを使用してアプリのビルドを続けます。`.xcworkspace`ファイルを使用しないと、アプリを正しくビルドできません。

### Carthage

アプリにiOS（Objective-C）用のTealiumをCarthageでインストールするには：

1.  Cartfileに以下を追加します：  
      ```perl
      github &#34;tealium/tealium-ios&#34;
      ```

2. フレームワークをダウンロードして抽出するには、以下のコマンドを実行します：  
      ```perl
      carthage update --platform ios --use-xcframeworks
      ```
      ビルドが失敗しないように、`--use-xcframeworks`フラグを使用してください。これには[Carthage 0.38.0](https://github.com/Carthage/Carthage/releases/tag/0.38.0)が必要です。

3. ビルド時に必要なフレームワークが自動的にコピーされるように、CarthageがXcodeプロジェクトに[適切に統合](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)されていることを確認します。

### 手動

アプリにiOS（Objective-C）用のTealiumを手動でインストールするには：

1.  `TealiumIOS.xcframework`をプロジェクトに追加します。

2.  結果のダイアログボックスでフレームワークをプロジェクトにコピーします。

3.  ターゲットで**General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、&#34;Embed &amp; Sign&#34;オプションを選択して`TealiumIOS.xcframework`を追加します。
Swiftプロジェクトの場合は、**Build Settings &gt; Swift Compiler &gt; Objective-C Bridging Header**オプションに移動し、`TealiumIOSBridgingHeader.h`ファイルを含めます。


## 初期化

Application Delegateまたはヘルパークラスのセットアップメソッド内で、以下の初期化コードを使用します：  



```swift
// アカウント、プロファイル、環境を構成します
let tealConfig = TEALConfiguration.init(account: &#34;ACCOUNT&#34;,
                                        profile: &#34;PROFILE&#34;,
                                    environment: &#34;ENVIRONMENT&#34;,
                                     datasource: &#34;DATASOURCE&#34;)

// このインスタンスの一意のキーで初期化します
guard let tealium = Tealium.newInstanceForKey(&#34;INSTANCE&#34;, configuration: tealConfig) else {
     // ここで追加の失敗応答           
     return
}
```



```obj-c
// インポートエリア
@import TealiumIOS;

// アカウント、プロファイル、環境を構成します
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34;
                          profile:@&#34;PROFILE&#34;
                          environment:@&#34;ENVIRONMENT&#34;
                          datasource:@&#34;DATASOURCE&#34;];

// このインスタンスの一意のキーで初期化します
Tealium *tealium = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:tealConfig]; 
```



ログレベルはデフォルトでiQアカウントからの公開構成から構成されます。この構成を上書きするには、TEALConfigurationインスタンスの`logLevel`プロパティを構成します：



```swift
// ログの詳細度をエラーのみに構成します
tealConfig.logLevel = .prod
```



```obj-c
// ログの詳細度を最大に構成します
[tealConfig setLogLevel: TEALLogLevelDev];
```



Tealiumインスタンスは、トラッキングを開始する前に以下のパラメータで構成する必要があります：

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumアカウント名 | `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealiumプロファイル名  | `&#34;main&#34;`  |
| `environment` | `String` |Tealium環境名  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` | `String` |(オプション) データソースキー | `&#34;abc123&#34;` |
| `instance` | `String` |インスタンスの一意の名前（複数のインスタンスがサポートされています）  | `&#34;tealium_main&#34;` |


