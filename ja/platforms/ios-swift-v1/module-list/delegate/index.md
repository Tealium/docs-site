---
title: デリゲートモジュール
description: デリゲートがディスパッチイベントの監視や抑制を可能にするマルチキャストデリゲートハンドラ。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/delegate/
---## 使用法

デリゲートモジュールは、デリゲートがディスパッチイベントの監視や抑制を可能にするマルチキャストデリゲートハンドラを提供します。このモジュールの使用は任意です。個々のディスパッチ/イベントに対して細かい制御が必要な場合にのみ使用します。例えば、イベントの送信をブロックしたり、トラッキング呼び出しの成功/失敗を監視するためなどです。

以下のプラットフォームがサポートされています:

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageでDelegateモジュールをインストールします。

### CocoaPods

CocoaPodsでDelegateモジュールをインストールするには、以下のpodをPodfileに追加します:  
```ruby
pod &#39;tealium-swift/TealiumDelegate&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについては[こちら](/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

CarthageでDelegateモジュールをインストールするには、以下の手順を実行します:

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します:  
    ```ruby
    TealiumDelegate.framework
    ```
3. トラッキングデリゲートを構成するには、プロジェクトに以下の必要なインポート文を追加します:  
    ```swift
    import TealiumDelegate
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポート文は必要ありません。iOSのCarthageインストールについては[こちら](/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー

このモジュールによって追加の変数は導入されません。

## APIリファレンス

### `add()`
`TealiumDelegate`プロトコルに準拠するクラスインスタンスへの弱いポインタを追加します。

```swift
add(delegate)
```

| パラメータ  | タイプ    | 説明                                       | 例 |
|-------------|---------|---------------------------------------------------| ---|
| `delegate`  | `TealiumDelegate`  | TealiumDelegateプロトコルに準拠する任意のクラス | `delegate:self` |


### `remove()`
`TealiumDelegate`プロトコルに準拠する指定されたクラスへの弱いポインタ参照を削除します。

```swift
remove(delegate)
```

| パラメータ  | タイプ    | 説明                                       | 例 |
|-------------|---------|---------------------------------------------------| --- |
| `delegate`  | `TealiumDelegate`  | TealiumDelegateプロトコルに準拠する任意のクラス	  | `delegate:self` |


### `removeAll()`

トラッキングからすべての弱いポインタを削除します。

```swift
removeAll()
```

### `tealiumShouldTrack()`

メソッドが`true`を返す場合、トラッキング呼び出しは完了することが許可されます。メソッドがfalseを返す場合、トラッキング呼び出しはキャンセルされます。

```swift
tealiumShouldTrack(data: [String:Any]) -&gt; Bool
```

| パラメータ | 説明   | 例             |
|------------|---------------|---------------------------|
| `data`     | `[String:Any]`| `[&#34;somekey&#34; : &#34;somevalue&#34;]` |


### `tealiumTrackCompleted()`
完了したトラック呼び出しの監視とエラーの処理を可能にします。

```swift
tealiumTrackCompleted(success: Bool, info: [String:Any]?, error: Error?)
```

| パラメータ | タイプ             | 説明                                                  | 例 |
|------------|------------------|--------------------------------------------------------------| ------- |
| `success`    | `Bool`         | ディスパッチが適切に完了したかどうか                                                       |[`&#34;true&#34;`, `&#34;false&#34;`] |
| `info`       | `[String:Any]` | 元のペイロードの辞書とディスパッチに関する他の返されたデータ     |`[&#34;somekey&#34; : &#34;somevalue&#34;]`  |
| `error`      | `Error`        | ディスパッチ処理中に遭遇したエラー（ある場合）|  `TealiumCollectError.xErrorDetected` |
