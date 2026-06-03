---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/track/
---
## ビューの追跡

[`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) メソッドを使用して画面のビューを追跡します。これは、任意のビューコントローラーの [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) メソッドで行われます。このメソッドは2つのパラメータを受け取ります：画面の名前と（オプションで）コンテキストビューデータ。

画面名の値はイベント属性 `screen_title` に構成されます。



```swift
// インスタンスを取得
let tealium = Tealium.instance(forKey: &#34;INSTANCE&#34;)

// 基本
tealium?.trackViewWithTitle(&#34;SCREEN_NAME&#34;, dataSources: nil)

// オプションのデータ付き
let optionalData = [&#34;KEY1&#34;: &#34;VALUE1&#34;]
tealium?.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: optionalData)

// オプションの配列データ付き
let optionalData = [&#34;KEY1&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;]]
tealium?.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: optionalData)
```



```obj-c
// インスタンスを取得
Tealium *tealium = [Tealium instanceForKey:@&#34;INSTANCE&#34;];

// 基本
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources:nil];

// オプションのデータ付き
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @&#34;VALUE1&#34;};
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources: optionalData];

// オプションの配列データ付き
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @[@&#34;STRING1&#34;, @&#34;STRING2&#34;]};
[tealium trackViewWithTitle:@&#34;SCREEN_NAME&#34; dataSources: optionalData];
```



| パラメータ | タイプ | 説明 | Swiftの例 | iOSの例 |
| --- | --- | --- | --- | --- |
| `title` | `String` |ビューのタイトル |  `&#34;screenName&#34;` | `&#34;screenName&#34;` |
| `customDataSources` | `[String]` |（オプション）イベントディスパッチに含めるカスタムデータソース（キーと値のペア） | `@{@&#34;someKey&#34;: @&#34;someValue&#34;}` | `[&#34;someKey&#34;: &#34;someValue&#34;]` |

## イベントの追跡

[`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) メソッドを使用して、ビュー以外の活動を追跡します。このメソッドは2つのパラメータを受け取ります：イベント名と（オプションで）コンテキストイベントデータ。

イベント名の値は、イベント属性 `tealium_event` に構成されます。



```swift
// インスタンスを取得
let tealium = Tealium.instance(forKey: &#34;INSTANCE&#34;)

// 基本
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: nil)

// オプションのデータ付き
let optionalData = [&#34;KEY1&#34;: &#34;VALUE1&#34;]
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: optionalData)

// オプションの配列データ付き
let optionalData = [&#34;KEY1&#34;: [&#34;STRING1&#34;, &#34;STRING2&#34;]]
tealium?.trackEvent(withTitle: &#34;EVENT_NAME&#34;, dataSources: optionalData)
```



```obj-c
// インスタンスを取得
Tealium *tealium = [Tealium instanceForKey:@&#34;INSTANCE&#34;];

// 基本
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:nil];

// オプションのデータ付き
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @&#34;VALUE1&#34;};
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:optionalData];

// オプションの配列データ付き
NSDictionary *optionalData = @{@&#34;KEY1&#34; : @[@&#34;STRING1&#34;, @&#34;STRING2&#34;]};
[tealium trackEventWithTitle:@&#34;EVENT_NAME&#34; dataSources:optionalData];
```



| パラメータ | タイプ |説明 | Swiftの例 | iOSの例 |
| --- | --- | --- | --- | --- |
| `title` | `String` | イベントのタイトル |`&#34;someEvent&#34;` | `&#34;someEvent&#34;` |
| `customDataSources` | `[String]` | （オプション）イベントディスパッチに含めるカスタムデータソース（キーと値のペア） | `@{@&#34;someKey&#34;: @&#34;someValue&#34;}` | `[&#34;someKey&#34;: &#34;someValue&#34;]` |
