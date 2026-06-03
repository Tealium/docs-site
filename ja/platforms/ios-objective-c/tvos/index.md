---
title: tvOS
description: Tealium for tvOSのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/tvos/
---
tvOSはもうサポートされていません。Tealium [iOS (Swift)](/ja/platforms/ios-swift/) ライブラリを推奨します。


## 要件

* [Tealium Customer Data Hubアカウント]()
* Xcode 7&#43;
* tvOS 9.0&#43;
* `.ipa`ファイルサイズに100KBの利用可能なスペース
* [Bitcode準拠](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) フレームワーク 

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、[tvOSサンプルアプリ](https://github.com/Tealium/tealium-tvos/tree/master/Samples)のダウンロードを推奨します。

Tealiumの実装をアプリの他の部分から抽象化するために、[サンプルヘルパークラス](https://github.com/Tealium/tealium-tvos/blob/master/Samples/tvOS_UIKitCatalog%2BTealium_Swift/UIKitCatalog/TealiumHelper.swift)の使用を推奨します。これにより、初期化とトラッキング呼び出しを行う単一のエントリーポイントが提供されます。また、ヘルパーファイル内のコードを更新し、すべてのヘッダー/メソッドファイル内のコードを更新する必要がなくなります。


## インストール

CocoaPodsを使用してtvOSのTealium依存関係をインストールおよび管理します。

1. Podfileに以下の依存関係を追加します：
    ```perl
    pod &#39;TealiumTVOS&#39;
    ```

2. [Tealium for tvOS](https://github.com/Tealium/tealium-tvos)をダウンロードしてインストールします。
    ライブラリをクローンすること（ダウンロードする代わりに）を推奨します。これにより、将来のリリースに簡単に更新できます。  

3. `TealiumTVOS.framework`をプロジェクトのtvOS Extensionターゲットに追加し、結果のダイアログボックスでフレームワークをプロジェクトにコピーします。

4. ターゲットの**General: Embedded Binaries**セクションにフレームワークを追加します：    
    ```perl
    TealiumTVOS.framework
    ```

## 初期化

Application Delegate、またはヘルパークラスのセットアップメソッド内で、以下のコードを使用してTealiumインスタンスを呼び出します：



```swift
let config = TEALConfiguration.init(account: &#34;ACCOUNT&#34;,
                      profile: &#34;PROFILE&#34;,
                      environment: &#34;ENV&#34;,
                      datasource: &#34;DATASOURCE&#34;)

guard let tealium = Tealium.newInstanceForKey(&#34;uniqueInstanceKey&#34;, configuration: config) else {
    // Any additional failure response here
    return
}
```


```objc
TEALConfiguration *configuration = [TEALConfiguration
                      configurationWithAccount:@&#34;ACCOUNT&#34;
                      profile:@&#34;PROFILE&#34;
                      environment:@&#34;ENV&#34;,
                      datasource:@&#34;DATASOURCE&#34;];

Tealium *tealiumInstance1 = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:configuration]; 
```



| パラメータ | 説明 | 例 |
|-----------|-------------|  ---- |
| `account`   | Tealiumアカウント名 |`&#34;companyXYZ&#34;` |
| `profile`   | Tealiumプロファイル名 | `&#34;main&#34;` |
| `environment` | Tealium環境名  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` | (オプション) データソースキー  | `&#34;abc123&#34;`|
| `instance` | ユニークなTealiumインスタンス識別子（複数のインスタンスがサポートされています） | `&#34;tealium_main&#34;` |

## ビューのトラッキング

画面のビューをトラッキングするには、[`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:)を2つのパラメーターで呼び出します：画面の名前と（オプションで）コンテキストビューデータ。

任意のUIViewControllerの[`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear)メソッド内で： 



```swift
Tealium.instanceForKey(&#34;uniqueInstanceKey&#34;)?.trackViewWithTitle(NSStringFromClass(self.classForCoder), dataSources: [:])
```


```objc
[[Tealium instanceForKey:@&#34;INSTANCE&#34;] trackViewWithTitle:NSStringFromClass([self class]) dataSources:nil];
```



画面名はイベントデータに`screen_title`として記入されます。

## イベントのトラッキング

ビュー以外のイベントをトラッキングするには、[`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:)を2つのパラメーターで呼び出します：イベント名と（オプションで）コンテキストイベントデータ。 



```swift
Tealium.instanceForKey(&#34;INSTANCE&#34;)?.trackEventWithTitle(&#34;EVENT_NAME&#34;, dataSources: [:])
```


```objc
[[Tealium instanceForKey:@&#34;INSTANCE&#34;] trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:nil];
```



イベント名はイベントデータに`tealium_event`として記入されます。


## APIリファレンス

クラスとメソッドの完全なリストについては、[TealiumTVOS Reference API](http://tealium.github.io/tealium-tvos/)を参照してください。

