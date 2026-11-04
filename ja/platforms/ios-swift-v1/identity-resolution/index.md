---
title: ID 解決
description: ID 解決について説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/identity-resolution/
---
<blockquote>
これは Tealium for iOS（Swift）の旧バージョン（1.x）です。最新バージョンについては、[Tealium for iOS（Swift）2.x](https://docs.tealium.com/ja/platforms/ios-swift/)を参照してください。
</blockquote>


## 仕組み

Tealium Swift ライブラリは、初回起動時に [`getVisitorId()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#getvisitorid) メソッドを使用して、ランダムかつ一意の永続的な訪問 ID を生成します。この値は、属性 `tealium_visitor_id` として、トラッキングされる各イベントに含まれます。この値は、Customer Data Platform（CDP）で使用されるプライマリ訪問 ID です。必要に応じて、セカンダリ訪問 ID 属性を永続データ保存に追加できます。

Customer Data Platform（CDP）を使用している場合、これは対象の訪問に関連付けられる主要なファーストパーティ訪問 ID になります。必要に応じて、追加の既知の訪問 ID をトラッキング呼び出しの変数として送信できます。

CDP での訪問 ID の構成について、[詳細はこちら](https://docs.tealium.com/server-side/getting-started/tutorials/visitor-profile-management/visitor-stitching-id/)を参照してください。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// Retrieve Tealium's first party visitor ID, if needed
	func getVisitorId() -> String? {
		return self.tealium?.visitorId
	}

	// adds a known visitor ID (such as an email address) to the persistent data store
	func setKnownVisitorId(_ id: String) {
		self.tealium?.persistentData()?.addPersistentData(["customer_id": id])
	}

}
```