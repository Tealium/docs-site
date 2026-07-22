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
[optimizelyTracker addInstanceWithName:@"INSTANCE_KEY"];
```

追加の構成は必要ありません。モジュールはOptimizely SDKからの通知を監視し、必要に応じてTealium Collectにデータを渡します。

## トラッキング

Tealium Collectに渡されるOptimizelyイベントは、実験とカスタムイベントの2種類です。 

これらのイベントは、以下のイベント名でTealiumによりキャプチャされます。

* `tealium_event="Optimizely Experiment Started"`  
Optimizely SDKが実験を有効化したとき。
* `tealium_event="Optimizely Event Tracked"`  
Optimizely SDKがカスタムイベントを受け取ったとき（Optimizelyの`track`メソッドを手動で呼び出すことで生成）。

## データレイヤー

トラッキングされるイベントには、以下のイベント属性が含まれます。

| 変数 | スコープ| 説明| 例|
| --- | ---| --- | --- |
| `optimizely_experiment_key` | 揮発性（セッション）| Optimizely実験名| `"Homescreen MVT"` |
| `optimizely_variation_key` | 揮発性（セッション）| Optimizely変数名| `"Variation A"` |
| `optimizely_user_id` | 揮発性（セッション）| OptimizelyユーザーID| `"ralph@tealium.com"` |
| `optimizely_event_key` | ヒット（単一イベント）| Optimizelyイベント名| `"purchase"` |
| `optimizely_event_value` | ヒット（単一イベント）| Optimizelyイベント値| `"123"` - 整数値のみ|
| `optimizely_XXX` | ヒット（単一イベント）| Optimizelyカスタム属性接頭辞。すべてのカスタム属性の先頭に"optimizely_"がエンリッチメントされ、Tealiumに直接渡されます| |

### デフォルト名の上書き

異なる名前付け規則を使用したい場合は、デフォルトの変数名をオーバーライドします。変数名を上書きするには、`TealiumOptimizelyTracker`クラスのパブリックプロパティを変更します。

```objc
TealiumOptimizelyTracker * optimizelyTracker = [TealiumOptimizelyTracker sharedInstance];

[optimizelyTracker addInstanceWithName:@"INSTANCE_NAME"];
optimizelyTracker.TEOptimizelyUserIdKeyName = @"USER_ID_KEY_NAME";
optimizelyTracker.TEOptimizelyExperimentKeyName = @"EXPERIMENT_KEY_NAME";
optimizelyTracker.TEOptimizelyVariationKeyName = @"VARIATION_KEY_NAME";
optimizelyTracker.TEOptimizelyEventKeyKeyName = @"EVENT_NAME_KEY_NAME";
optimizelyTracker.TEOptimizelyEventValueKeyName = @"EVENT_VALUE_KEY_NAME";
```
