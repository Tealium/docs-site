---
title: Optimizely X Trackingモジュール
description: Optimizely XとTealium Collectの統合をもたらします。このモジュールは、Optimizely Xライブラリによってトリガーされるイベントを監視し、イベントデータをTealium Collectに渡します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/module-list/optimizely-x-tracking/
---

## 要件

* [Optimizely X iOS SDK](https://developers.optimizely.com/classic/ios/getting-started/index.html)がアプリに追加されていること

## インストール

Optimizely X Trackingモジュールを手動でインストールするには、以下の手順に従います。

1. [Optimizely X Trackingモジュール](https://github.com/Tealium/tealium-ios/tree/master/TealiumIOSOptimizely.framework)をダウンロードします。

2. Xcodeプロジェクトに`TealiumIOSOptimizely.framework`ファイルを追加します（プロジェクト構成の**[Embedded Binaries]**セクション）。

Optimizely Xライブラリの詳細については、[こちら](https://docs.developers.optimizely.com/full-stack/docs)を参照してください。

## 初期化

Optimizely X Trackingモジュールは、標準のTealiumインスタンスを作成した後に初期化する必要があります。

`TealiumOptimizelyTracker`インスタンスを初期化するには、Tealiumインスタンスを渡し、インスタンス名を指定します。

```objc
// Initialize the Tealium Optimizely instance
TealiumOptimizelyTracker * optimizelyTracker = [TealiumOptimizelyTracker tealium];
[optimizelyTracker addInstanceWithName:@&#34;INSTANCE_KEY&#34;];
```

追加の構成は必要ありません。モジュールはOptimizely SDKからの通知を監視し、必要に応じてTealium Collectにデータを渡します。

## トラッキング

Tealium Collectに渡されるOptimizelyイベントは、実験とカスタムイベントの2種類です。 

これらのイベントは、以下のイベント名でTealiumによりキャプチャされます。

* `tealium_event=&#34;Optimizely Experiment Started&#34;`  
Optimizely SDKが実験を有効化したとき。
* `tealium_event=&#34;Optimizely Event Tracked&#34;`  
Optimizely SDKがカスタムイベントを受け取ったとき（Optimizelyの`track`メソッドを手動で呼び出すことで生成）。

## データレイヤー

トラッキングされるイベントには、以下のイベント属性が含まれます。

| 変数 | スコープ| 説明| 例|
| --- | ---| --- | --- |
| `optimizely_experiment_key` | 揮発性（セッション）| Optimizely実験名| `&#34;Homescreen MVT&#34;` |
| `optimizely_variation_key` | 揮発性（セッション）| Optimizely変数名| `&#34;Variation A&#34;` |
| `optimizely_user_id` | 揮発性（セッション）| OptimizelyユーザーID| `&#34;ralph@tealium.com&#34;` |
| `optimizely_event_key` | ヒット（単一イベント）| Optimizelyイベント名| `&#34;purchase&#34;` |
| `optimizely_event_value` | ヒット（単一イベント）| Optimizelyイベント値| `&#34;123&#34;` - 整数値のみ|
| `optimizely_XXX` | ヒット（単一イベント）| Optimizelyカスタム属性接頭辞。すべてのカスタム属性の先頭に&#34;optimizely_&#34;がエンリッチメントされ、Tealiumに直接渡されます| |

### デフォルト名の上書き

異なる名前付け規則を使用したい場合は、デフォルトの変数名をオーバーライドします。変数名を上書きするには、`TealiumOptimizelyTracker`クラスのパブリックプロパティを変更します。

```objc
TealiumOptimizelyTracker * optimizelyTracker = [TealiumOptimizelyTracker sharedInstance];

[optimizelyTracker addInstanceWithName:@&#34;INSTANCE_NAME&#34;];
optimizelyTracker.TEOptimizelyUserIdKeyName = @&#34;USER_ID_KEY_NAME&#34;;
optimizelyTracker.TEOptimizelyExperimentKeyName = @&#34;EXPERIMENT_KEY_NAME&#34;;
optimizelyTracker.TEOptimizelyVariationKeyName = @&#34;VARIATION_KEY_NAME&#34;;
optimizelyTracker.TEOptimizelyEventKeyKeyName = @&#34;EVENT_NAME_KEY_NAME&#34;;
optimizelyTracker.TEOptimizelyEventValueKeyName = @&#34;EVENT_VALUE_KEY_NAME&#34;;
```
