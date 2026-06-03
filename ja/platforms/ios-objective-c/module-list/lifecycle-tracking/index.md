---
title: ライフサイクル追跡モジュール
description: TealiumのiOS向け5.x実装にアプリライフサイクル追跡イベントを提供します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/module-list/lifecycle-tracking/
---
## インストール

ライフサイクル追跡モジュールはアプリに追加する必要があります。CocoaPodsまたは手動でTealium for iOSライブラリと同様にモジュールをインストールしてください。

任意の抽象クラス（`TealiumHelper.h`など）で、`@import TealiumIOS`を`@import TealiumIOSLifecycle`に置き換えてください。

### CocoaPods

CocoaPodsでライフサイクル追跡モジュールをインストールするには、Podfileに以下を追加してください：

```perl
pod &#39;TealiumIOSLifecycle&#39;
```

### 手動

ライフサイクル追跡モジュールを手動でインストールするには、以下の手順に従ってください：

1. [ライフサイクル追跡モジュール](https://github.com/Tealium/tealium-ios/tree/master/TealiumIOSLifecycle.framework)をダウンロードします。

2. `TealiumIOSLifecycle.framework`ファイルをプロジェクトに追加します（Embedded Binariesセクションに）。

## トラック

このモジュールは以下のライフサイクルイベントを追跡します：

| ライフサイクルイベント | 説明 |
| --- | --- |
| `launch` | アプリが起動されました |
| `sleep` | アプリがバックグラウンドに送られました |
| `wake` | アプリがフォアグラウンドに送られました |
| `none` | ライフサイクルイベントに関連付けられていないイベントに追加されたデータ |

これらの値は`lifecycle_type`変数で示されます。

### 自動追跡

ライフサイクル追跡モジュールを構成して、標準の`UIApplication`通知を自動的にリッスンし、`launch`、`wake`、`sleep`イベントを自動的にトリガーします。

プロジェクトから`TealiumIOSLifecycle.framework`をリンク解除または削除して、ライフサイクル追跡を削除します。

**起動イベント**  
`UIApplicationDidFinishLaunchingNotification`の検出時に生成されます。

**スリープイベント**  
`UIApplicationWillResignActiveNotification`の検出時に生成されます。

**ウェイクイベント**  
`UIApplicationWillEnterForegroundNotification`の検出時に生成されます。

### 手動追跡

特定のライフサイクルパラダイムや非標準的なライフサイクル追跡のために利用可能です。手動でライフサイクルイベントを追跡するには、`setLifecycleAutotrackingIsEnabled`を`NO`に構成して、ライフサイクル自動追跡を無効にします。

**起動イベント**  
`launch`イベントを手動で追跡するには、以下を呼び出します：

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] launch];
```

**スリープイベント**  
`sleep`イベントを手動で追跡するには、以下を呼び出します：

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] sleep];
```

**ウェイクイベント**  
`wake`イベントを手動で追跡するには、以下を呼び出します：

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] wake];
```