---
title: tvOS
description: Tealium for tvOSのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/tvos/
---

<blockquote>
tvOSはもうサポートされていません。Tealium [iOS (Swift)](https://docs.tealium.com/ja/platforms/ios-swift/) ライブラリを推奨します。
</blockquote>



## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Xcode 7+
* tvOS 9.0+
* `.ipa`ファイルサイズに100KBの利用可能なスペース
* [Bitcode準拠](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) フレームワーク 

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、[tvOSサンプルアプリ](https://github.com/Tealium/tealium-tvos/tree/master/Samples)のダウンロードを推奨します。

Tealiumの実装をアプリの他の部分から抽象化するために、[サンプルヘルパークラス](https://github.com/Tealium/tealium-tvos/blob/master/Samples/tvOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift)の使用を推奨します。これにより、初期化とトラッキング呼び出しを行う単一のエントリーポイントが提供されます。また、ヘルパーファイル内のコードを更新し、すべてのヘッダー/メソッドファイル内のコードを更新する必要がなくなります。


## インストール

CocoaPodsを使用してtvOSのTealium依存関係をインストールおよび管理します。

1. Podfileに以下の依存関係を追加します：
    ```perl
    pod 'TealiumTVOS'
    ```

2. [Tealium for tvOS](https://github.com/Tealium/tealium-tvos)をダウンロードしてインストールします。
    
<blockquote>
ライブラリをクローンすること（ダウンロードする代わりに）を推奨します。これにより、将来のリリースに簡単に更新できます。
</blockquote>
  

3. `TealiumTVOS.framework`をプロジェクトのtvOS Extensionターゲットに追加し、結果のダイアログボックスでフレームワークをプロジェクトにコピーします。

4. ターゲットの**General: Embedded Binaries**セクションにフレームワークを追加します：    
    ```perl
    TealiumTVOS.framework
    ```

## 初期化

Application Delegate、またはヘルパークラスのセットアップメソッド内で、以下のコードを使用してTealiumインスタンスを呼び出します：



```swift
let config = TEALConfiguration.init(account: "ACCOUNT",
                      profile: "PROFILE",
                      environment: "ENV",
                      datasource: "DATASOURCE")

guard let tealium = Tealium.newInstanceForKey("uniqueInstanceKey", configuration: config) else {
    // Any additional failure response here
    return
}
```


```objc
TEALConfiguration *configuration = [TEALConfiguration
                      configurationWithAccount:@"ACCOUNT"
                      profile:@"PROFILE"
                      environment:@"ENV",
                      datasource:@"DATASOURCE"];

Tealium *tealiumInstance1 = [Tealium newInstanceForKey:@"INSTANCE" configuration:configuration]; 
```



| パラメータ | 説明 | 例 |
|-----------|-------------|  ---- |
| `account`   | Tealiumアカウント名 |`"companyXYZ"` |
| `profile`   | Tealiumプロファイル名 | `"main"` |
| `environment` | Tealium環境名  | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` | (オプション) データソースキー  | `"abc123"`|
| `instance` | ユニークなTealiumインスタンス識別子（複数のインスタンスがサポートされています） | `"tealium_main"` |

## ビューのトラッキング

画面のビューをトラッキングするには、[`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:)を2つのパラメーターで呼び出します：画面の名前と（オプションで）コンテキストビューデータ。

任意のUIViewControllerの[`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear)メソッド内で： 



```swift
Tealium.instanceForKey("uniqueInstanceKey")?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [:])
```


```objc
[[Tealium instanceForKey:@"INSTANCE"] trackViewWithTitle:NSStringFromClass([self class]) dataSources:nil];
```




<blockquote>
画面名はイベントデータに`screen_title`として記入されます。
</blockquote>


## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、[`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:)を2つのパラメーターで呼び出します：イベント名と（オプションで）コンテキストイベントデータ。 



```swift
Tealium.instanceForKey("INSTANCE")?.trackEventWithTitle("EVENT_NAME", dataSources: [:])
```


```objc
[[Tealium instanceForKey:@"INSTANCE"] trackEventWithTitle:@"EVENT_NAME" dataSources:nil];
```




<blockquote>
イベント名はイベントデータに`tealium_event`として記入されます。
</blockquote>



## APIリファレンス

クラスとメソッドの完全なリストについては、[TealiumTVOS Reference API](http://tealium.github.io/tealium-tvos/)を参照してください。

