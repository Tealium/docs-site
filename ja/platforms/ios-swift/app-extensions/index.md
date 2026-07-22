---
title: アプリ拡張機能
description: アプリ拡張機能について学びましょう。
url: https://docs.tealium.com/ja/platforms/ios-swift/app-extensions/
---
## 今日の拡張機能

**今日の拡張機能**は、デバイスの「今日」画面に表示されるウィジェットです。これらのアプリ拡張機能はOSによって非常に限られたリソースが許可されており、メモリや処理能力を多く消費すると終了される可能性があります。

Today Extension内でSwiftライブラリを通常通り使用しますが、メモリの使用量を低く保つために、データを送信する[Collectモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/collect/)のみを使用することをお勧めします。[Tag Managementモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/tag-management/)はリソースを多く消費するため、ウィジェットが終了する可能性があります。

選択したオプションに関わらず、ウィジェットが期待通りに動作するかどうかを徹底的にテストし、確認することが重要です。ウィジェットに組み込むTealiumモジュールを少なくすることで、パフォーマンスが向上し、メモリの使用量が低くなります。

## watchOS拡張機能と独立したアプリ

TealiumがインストールされているiOSプロジェクトにwatchOSターゲットを追加する場合は、必要なモジュール、Tealiumをインポートする`TealiumHelper`（または他のアナリティクスマネージャークラス）をWatch Extensionターゲットに追加し、必要なトラッキングコールを行います。`WKWebView`への依存性のため、Tag ManagementモジュールはwatchOSではサポートされていません。データ収集の唯一のサポートされている方法はCollectモジュールです。

Tealiumを使用しているwatchOS拡張ターゲットの例については、[TealiumSwiftExample](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample/TealiumSwiftWatchExample%20Extension)を参照してください。独立したwatchOSアプリを作成する場合も同様です。各`Tealium###.framework`をwatchOS拡張ターゲットに割り当て、`TealiumHelper`クラスを追加します。

または、`WatchConnectivty`フレームワークの`WCSession` APIを使用して、トラッキングコールを送信したいたびにホストiOSアプリにメッセージを送信します。これにより、Tag Managementモジュールを使用している場合にイベントを追跡できますが、独立したwatchOSアプリではオプションになりません。

## WidgetKitとApp Clips

現在のiOSアプリにWidgetKitまたはApp Clip拡張機能を追加する場合は、TealiumをインポートするiOSの`TealiumHelper`（または他のアナリティクスマネージャークラス）をWidgetKitまたはApp Clipターゲットと共有します。その後、WidgetKitおよびApp Clipの`Views`内でトラッキングコールを追加し、WidgetまたはApp ClipからTealiumにイベントを送信します。例については、[TealiumSwiftExample](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample/WidgetExample)を参照してください。

## アプリ拡張機能の訪問ID

アプリ拡張機能は、ホストiOSアプリ（利用可能な場合）と共有されていない独自のサンドボックス化されたデータ保存を持っています。そのため、デフォルトでは、アプリが初めて起動されたときに新しい永続的な訪問IDが生成されます。

iOSアプリ、Todayウィジェット、およびwatchOS拡張機能を持っている場合、同じ訪問に対して3つの異なる訪問IDが発生する問題があります。これは、訪問のスティッチングを使用しており、すでにアプリユーザーの既知の訪問IDがある場合には問題になりません。この状況を避けるためには、アプリとその拡張機能間で訪問IDを同期させます。これは、Tealiumを初期化する際にアプリ拡張機能の`TealiumConfig`オブジェクトに現在のTealium第一者訪問IDを渡すことで行われます。IDは保存され、アプリの将来の起動時に再生成されることなく使用されます。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	// iOSアプリのTealium Swiftライブラリから現在の訪問IDを返す
	func getVisitorId() -> String? {
		return self.tealium.visitorId
	}

	// アプリ拡張機能で、iOSアプリから取得したIDを構成オブジェクトに渡す
	private func initTealium(existingVisitorId id: String) {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                 profile: "PROFILE",
        	   	                 environment: "ENVIRONMENT",
           		                 datasource: "DATASOURCE")

		// アプリ拡張機能で第一者IDとして使用される既存のID
        config.existingVisitorId = id
        self.tealium = Tealium(config: config)
	}
}
```

または、訪問IDを中央で生成し、初期化時に各Tealiumインスタンスに渡すことをお勧めします。UUIDの使用が推奨されます。


<blockquote>
最初のパーティ訪問IDには、メールアドレスのような単純なIDを使用しないでください。
</blockquote>
