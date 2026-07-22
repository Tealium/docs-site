---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/data-management/
---
<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[iOS（Swift）用Tealium 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)を参照してください。
</blockquote>


## 使用方法

すべてのイベントに必要な変数があります。毎回必要な変数データを手動で追加するのを避けるために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)についてもっと学びましょう。


## 永続的データ
永続的データ値はデバイスに保存され、アプリの起動間で保持されます。これらの値は、トラッキングコールに渡された任意の辞書とマージされます。

次の例に示すように、[`persistentData().add()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-persistent-data/#add) メソッドは永続的データを保存します：

```swift
tealium?.persistentData()?.add(data: ["KEY":"VALUE"])
```

特定のキーのデータをクリアするには、[`persistentData.deleteData()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-persistent-data/#deletedata) メソッドを使用し、すべてのデータを削除するには [`persistentData.deleteAllData()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-persistent-data/#deletealldata) メソッドを使用します。

次の例はこれらのメソッドを示しています：

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// 永続的データを追加し、手動でクリアされるまで各ヒットに送信されます
  // - Parameter data: 永続的データとして保存されるキーと値のペアを含む `[String: Any]`
	func addPersistentData(_ data: [String: Any]) {

		self.tealium?.persistentData()?.add(data)
	}

	// 特定のキーの永続的データを削除します
	// - Parameter keys: 削除されるキーを含む `[String]`
	func deleteData(for keys: [String]) {
		// 特定のキーのデータをクリアします
		self.tealium?.persistentData.deleteData(forKeys: keys)
		self.tealium?.persistentData.deleteAllData()
	}
}
```

## 揮発性データ
揮発性データ値は各イベントにマージされますが、アプリを閉じて再起動すると破棄されます。これらの値は、トラッキングコールに渡された任意の辞書とマージされます。

[`volatileData().add()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-volatile-data/#add) メソッドは揮発性データを保存します。

特定のキーのデータをクリアするには、[`voltileData.deleteData()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-volatile-data/#deletedata) メソッドを使用し、すべてのデータを削除するには [`volatileData.deleteAllData()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-volatile-data/#deletealldata) メソッドを使用します。

次の例はこれらのメソッドを示しています：

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// 揮発性データを追加し、アプリが終了するまで各ヒットに送信されます
  // - Parameter data: 揮発性データとして保存されるキーと値のペアを含む `[String: Any]`
	func addVolatileData(_ data: [String: Any]) {

		self.tealium?.volatileData()?.add(data)
	}

	// 特定のキーの揮発性データを削除します
  // - Parameter keys: 削除されるキーを含む `[String]`
	func deleteData(for keys: [String]) {
		// 特定のキーのデータをクリアします
		self.tealium?.volatileData.deleteData(forKeys: keys)
		self.tealium?.volatileData.deleteAllData()
	}
}
```