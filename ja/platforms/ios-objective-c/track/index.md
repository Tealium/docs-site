---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/track/
---
## ビューの追跡

[`trackViewWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackViewWithTitle:dataSources:) メソッドを使用して画面のビューを追跡します。これは、任意のビューコントローラーの [`viewDidAppear()`](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621423-viewdidappear) メソッドで行われます。このメソッドは2つのパラメータを受け取ります：画面の名前と（オプションで）コンテキストビューデータ。


<blockquote>
画面名の値はイベント属性 `screen_title` に構成されます。
</blockquote>




```swift
// インスタンスを取得
let tealium = Tealium.instance(forKey: "INSTANCE")

// 基本
tealium?.trackViewWithTitle("SCREEN_NAME", dataSources: nil)

// オプションのデータ付き
let optionalData = ["KEY1": "VALUE1"]
tealium?.trackView(withTitle: "SCREEN_NAME", dataSources: optionalData)

// オプションの配列データ付き
let optionalData = ["KEY1": ["STRING1", "STRING2"]]
tealium?.trackView(withTitle: "SCREEN_NAME", dataSources: optionalData)
```



```obj-c
// インスタンスを取得
Tealium *tealium = [Tealium instanceForKey:@"INSTANCE"];

// 基本
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources:nil];

// オプションのデータ付き
NSDictionary *optionalData = @{@"KEY1" : @"VALUE1"};
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources: optionalData];

// オプションの配列データ付き
NSDictionary *optionalData = @{@"KEY1" : @[@"STRING1", @"STRING2"]};
[tealium trackViewWithTitle:@"SCREEN_NAME" dataSources: optionalData];
```



| パラメータ | タイプ | 説明 | Swiftの例 | iOSの例 |
| --- | --- | --- | --- | --- |
| `title` | `String` |ビューのタイトル |  `"screenName"` | `"screenName"` |
| `customDataSources` | `[String]` |（オプション）イベントディスパッチに含めるカスタムデータソース（キーと値のペア） | `@{@"someKey": @"someValue"}` | `["someKey": "someValue"]` |

## イベントの追跡

[`trackEventWithTitle()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/trackEventWithTitle:dataSources:) メソッドを使用して、ビュー以外の活動を追跡します。このメソッドは2つのパラメータを受け取ります：イベント名と（オプションで）コンテキストイベントデータ。


<blockquote>
イベント名の値は、イベント属性 `tealium_event` に構成されます。
</blockquote>




```swift
// インスタンスを取得
let tealium = Tealium.instance(forKey: "INSTANCE")

// 基本
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: nil)

// オプションのデータ付き
let optionalData = ["KEY1": "VALUE1"]
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: optionalData)

// オプションの配列データ付き
let optionalData = ["KEY1": ["STRING1", "STRING2"]]
tealium?.trackEvent(withTitle: "EVENT_NAME", dataSources: optionalData)
```



```obj-c
// インスタンスを取得
Tealium *tealium = [Tealium instanceForKey:@"INSTANCE"];

// 基本
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:nil];

// オプションのデータ付き
NSDictionary *optionalData = @{@"KEY1" : @"VALUE1"};
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:optionalData];

// オプションの配列データ付き
NSDictionary *optionalData = @{@"KEY1" : @[@"STRING1", @"STRING2"]};
[tealium trackEventWithTitle:@"EVENT_NAME" dataSources:optionalData];
```



| パラメータ | タイプ |説明 | Swiftの例 | iOSの例 |
| --- | --- | --- | --- | --- |
| `title` | `String` | イベントのタイトル |`"someEvent"` | `"someEvent"` |
| `customDataSources` | `[String]` | （オプション）イベントディスパッチに含めるカスタムデータソース（キーと値のペア） | `@{@"someKey": @"someValue"}` | `["someKey": "someValue"]` |
