---
title: watchOS
description: Tealium for watchOSのインストール方法を学びましょう。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/watchos/
---## 要件

* Xcode 7&#43;
* iOS 8.1&#43;
* watchOS 2.0&#43;
* ホストアプリに[Tealium for iOS](/ja/platforms/ios-swift/)がインストールされていること
* `.ipa `ファイルサイズに400KBの利用可能なスペース（これはホストアプリに必要な`tealium-ios`ライブラリを含む）
* [Bitcode準拠](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html)フレームワーク

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、サンプルアプリをダウンロードすることをお勧めします：

- [Objective-C WatchOSサンプルアプリ](https://github.com/Tealium/tealium-ios/tree/master/Samples/WatchOS_Catalog%2BTealium_ObjC)
- [Swift WatchOSサンプルアプリ](https://github.com/Tealium/tealium-ios/tree/master/Samples/WatchOS_Sample_Swift)

Tealiumの実装をアプリの他の部分から抽象化するために、[サンプルヘルパークラス](https://github.com/Tealium/tealium-ios/blob/master/Samples/WatchOS_Catalog%2BTealium_ObjC/WatchKit%20Catalog/Tealium/TealiumHelper.m)の使用をお勧めします。これにより、初期化およびトラッキング呼び出しを行う単一のエントリポイントが提供されます。また、ヘルパーファイルのコードを更新し、すべてのヘッダー/メソッドファイルで更新することなく、コードを更新できます。


## インストール

Tealium for watchOSを、`TealiumIOS.framework`がホストアプリケーションで実装されている拡張アプリケーションとしてインストールします。


1. `TealiumWATCHOSExtension.framework`をプロジェクトのwatchOS Extensionターゲットに追加し、結果のダイアログボックスでフレームワークをプロジェクトにコピーします。

2. ターゲットの**General: Embedded Binaries**セクションにフレームワークを追加します：  
    ```perl
    TealiumWATCHOSExtension.framework
    ```  
Swiftプロジェクトの場合、ブリッジングヘッダーファイルに`&lt;TealiumWATCHOSExtension/TEALWKExtension.h&gt;`を追加します。  

3. **Projects: Target: Build Settings**の下ですべてのパスが期待通りであることを確認します。


## 初期化

Tealium for watchOSがプロジェクトに追加されたら、コーディングを開始する準備が整います。

Application Delegateまたはヘルパークラスのセットアップメソッド内で、以下のコードを追加してTealiumインスタンスを初期化します：



```swift
// Tealiumインスタンスを取得
let config = TEALWKExtensionConfiguration.configuration()
guard let tealium = TEALWKExtension.newInstanceForKey(&#34;[INSTANCE]&#34;) else {
    // ここで追加の失敗応答
    return
}
```


```objc
// インポートエリア
#import &lt;TealiumWATCHOSExtension/TealiumWATCHOS.h&gt;

// セットアップメソッド内
TEALWKExtensionConfiguration *config = [TEALWKExtensionConfiguration configuration];
config.logLevel = TEALLogLevelDev;
[TEALWKExtension newInstanceForKey:@&#34;[INSTANCE]&#34; configuration:config]; 
```




## ビューのトラッキング

画面のビューをトラッキングするには、[`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:)を2つのパラメーター（画面の名前と（オプションで）コンテキストビューデータ）で呼び出します。

任意のUIViewControllerの[`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear)メソッドで、このコードを使用します：




```swift
TEALWKExtension.instanceForKey(&#34;[hostTealiumInstanceKey]&#34;)?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [String:String]())
```


```objc
[[TEALWKExtension instanceForKey:@&#34;[INSTANCE]&#34;] trackViewWithTitle:NSStringFromClass([self class]) dataSources:@{}];
```



## イベントのトラッキング

非ビューのアクティビティをトラッキングするには、[`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:)を2つのパラメーター（イベント名と（オプションで）コンテキストイベントデータ）で呼び出します。

イベントトリガーをトリガーするか、イベントトリガーに応答する任意のメソッドで、このコードを使用します：



```swift
TEALWKExtension.instanceForKey(&#34;[INSTANCE]&#34;)?.trackEventwWithTitle(&#34;EVENT_NAME&#34;), dataSources: [String:String]())
```


```objc
[[Tealium instanceForKey:@&#34;[INSTANCE]&#34;] trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:@{@&#34;optionalKey&#34;:@&#34;optionalValue&#34;}];
```



