---
title: アイデンティティ解決
description: アイデンティティ解決について学びましょう。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/identity-resolution/
---これはTealium for iOS (Swift)の以前のバージョン（1.x）です。最新バージョンは[Tealium for iOS (Swift) 2.x](/ja/platforms/ios-swift/)をご覧ください。

## 動作原理

Tealium Swiftライブラリは、最初に[`getVisitorId()`](/ja/platforms/ios-swift-v1/api/tealium/#getvisitorid)メソッドで起動されたときにランダムかつ一意の永続的な訪問IDを生成します。この値は、`tealium_visitor_id`属性として各トラッキングイベントに含まれます。この値はTealium AudienceStreamで使用される主要な訪問IDです。必要に応じて、永続的なデータ保存に追加の訪問ID属性を追加することができます。

AudienceStreamを使用している場合、これがこの訪問に関連付けられた主要な第一者訪問IDになります。必要に応じて、追跡コールで変数として追加の既知の訪問IDを提供することができます。

[AudienceStreamで訪問IDの構成についてもっと学ぶ]()。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// 必要に応じてTealiumの第一者訪問IDを取得
	func getVisitorId() -&gt; String? {
		return self.tealium?.visitorId
	}

	// 永続的データストアに既知の訪問ID（例：メールアドレス）を追加
	func setKnownVisitorId(_ id: String) {
		self.tealium?.persistentData()?.addPersistentData([&#34;customer_id&#34;: id])
	}

}
```