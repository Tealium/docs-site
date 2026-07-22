---
title: Tealium
description: Tealiumクラスは、すべてのモジュールのための主要なAPIエントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/
---
## クラス: `Tealium`

以下は、iOS (Swift) の `Tealium` クラスでよく使用されるメソッドをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| `joinTrace()`  | 指定されたIDでトレースに参加する |
| `leaveTrace()`  | 以前に参加したトレースを離れ、訪問セッションを終了する |
| `Tealium()`  | 新しい `Tealium` オブジェクトのコンストラクタ |
| `track()`  | 関連データを持つイベントを追跡し、オプションでコールバック関数をトリガーする |
| `trackView()`  | 関連データを持つ画面ビューを追跡し、オプションでコールバック関数をトリガーする |
| `visitorId` | ランダムに生成された一意の永続的訪問IDを返す |

### `joinTrace()`

指定されたIDでトレースに参加します。トレースはアプリセッションの間アクティブのままで、`leaveTrace()`が呼ばれるまで続きます。Tealium Customer Data Hubのトレース機能について[詳しくはこちら](https://docs.tealium.com/manage-traces/)。

```swift
joinTrace(traceId: String)
```

| パラメータ | タイプ | 説明 | 例 |
|------------|----------------------|-----------------| ---- |
| `traceId`  | `String` | トレースツールから取得したトレースID | `"12345"` |


### `leaveTrace()`

以前に参加したトレースを離れ、訪問セッションを終了します。トレースを離れる際に訪問セッションを保持するオプションがあります。

```swift
tealium?.leaveTrace(killVisitorSession: false)
```

| パラメータ | タイプ | 説明 | 例 |
|------------|----------------------|-----------------| ---- |
| `killVisitorSession`     | `Bool` | (オプション) パラメータが渡されない場合はデフォルトで `true`、訪問セッションを終了したくない場合は `false` を渡す | [`true`, `false`] |

### `Tealium()`
新しい `Tealium` オブジェクトのコンストラクタ。

```swift
Tealium(config: TealiumConfig, completion: Closure)
```

| パラメータ | タイプ | 説明 |
|------------|----------------------|--------------------------------------------------------------------------------------------|
| `config`| `TealiumConfig` | アカウントの詳細を含む `TealiumConfig` オブジェクトで Tealium オブジェクトを初期化します。 |
| `completion`  | `Closure` | (オプション) 初期化完了時に呼び出される完了クロージャ `()-> Void )?` |


### `track()`

関連データを持つイベントを追跡し、オプションでコールバック関数をトリガーします。

```swift
track(title:String, data:[String:Any], completion:ClosureType)
```

| パラメータ | タイプ | 説明 | 例 |
|---------------|---------------|------------------| --- |
| `title`| `String` | 追跡するイベントの名前 | `title: "Buy Now"` |
| `data`| `Dictionary` | イベント追跡に関連するキーと値のペアのオブジェクト | `data: ["product_id" : ["widget123"]]` |
| `completion`| `ClosureType` | 追跡コールの完了時に実行する関数 (なしの場合は `nil` を使用) | `nil` |


### `trackView()`
関連データを持つ画面ビューを追跡し、オプションでコールバック関数をトリガーします。

```swift
trackView(title:String, data:[String:Any], completion:ClosureType)
```

| パラメータ | タイプ | 説明 | 例 |
|---------------|---------------|------------------| --- |
| `title`| `String` | 追跡する画面ビューの名前 | `title: "Homescreen"` |
| `data`| `Dictionary` | イベント追跡に関連するキーと値のペアのオブジェクト | `data: ["customer_id": "1234567890-a"]` |
| `completion`| `ClosureType` | 追跡コールの完了時に実行する関数 (なしの場合は `nil` を使用) | `nil` |


### `visitorId`

ランダムに生成された一意の永続的訪問IDを返します。

```swift
let visitorId: String = tealium.visitorId
```