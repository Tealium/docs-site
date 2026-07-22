---
title: アプリ拡張機能
description: アプリ拡張機能について学びましょう。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/app-extensions/
---
<blockquote>
これはTealium for iOS (Swift)の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for iOS (Swift) 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)をご覧ください。
</blockquote>


## 今日の拡張機能

**今日の拡張機能**はデバイスの「今日」画面に表示されるウィジェットです。これらのアプリ拡張機能はOSから非常に限られたリソースを許可されており、メモリや処理能力を多く消費すると終了される可能性があります。

Today Extension内でSwiftライブラリを通常通り使用しますが、メモリの使用量を低く保つために、データ送信には[Collectモジュール](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/collect/)のみを使用することをお勧めします。[Tag Managementモジュール](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/)はリソースを多く消費する可能性があり、ウィジェットが終了する原因となるかもしれません。

選択したオプションに関わらず、ウィジェットが期待通りに動作するかどうかを徹底的にテストし、確認することが重要です。ウィジェットにTealiumモジュールを少なく組み込むことで、パフォーマンスが向上し、メモリの使用量が低くなります。

## watchOS拡張機能と独立したアプリ

TealiumがインストールされているiOSプロジェクトにwatchOSターゲットを追加する場合は、必要なモジュールと`TealiumHelper`をWatch Extensionターゲットに追加し、必要なトラッキングコールを行います。`WKWebView`への依存性のため、Tag ManagementモジュールはwatchOSではサポートされていません。データ収集の唯一のサポートされた方法はCollectモジュールです。

または、`WatchConnectivty`フレームワークの`WCSession` APIを使用して、トラッキングコールを送信したいたびにホストiOSアプリにメッセージを送ることができます。これにより、Tag Managementモジュールを使用している場合にイベントを追跡できますが、独立したwatchOSアプリではオプションになりません。

## アプリ拡張機能での訪問ID

アプリ拡張機能は、ホストiOSアプリ（利用可能な場合）と共有されない独自のサンドボックス化されたデータ保存を持っています。そのため、デフォルトではアプリが初めて起動されたときに新しい永続的な訪問IDが生成されます。

iOSアプリ、Todayウィジェット、およびwatchOS拡張機能を持つ場合、同じ訪問に対して3つの異なる訪問IDが発生する問題があります。訪問のスティッチングを使用しており、すでにアプリユーザーの既知の訪問IDがある場合は問題ありません。この状況を避けるために、アプリとその拡張機能間で訪問IDを同期させます。これは、Tealiumを初期化する際にアプリ拡張機能の`TealiumConfig`オブジェクトに現在のTealium第一者訪問IDを渡すことによって行われます。IDは保存され、アプリの将来の起動時に再生成されることなく使用されます。

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

		// 既存のIDはアプリ拡張機能で第一者IDとして使用される
        config.existingVisitorId = id
        self.tealium = Tealium(config: config)
	}

}
```

代わりに、訪問IDを中央で生成し、初期化時に各Tealiumインスタンスに渡すことをお勧めします。UUIDの使用が推奨されます。


<blockquote>
最初の訪問IDに単純なID（例：メールアドレス）を使用しないでください。
</blockquote>
