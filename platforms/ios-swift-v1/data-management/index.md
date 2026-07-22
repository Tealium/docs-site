---
title: Data Management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/ios-swift-v1/data-management/
---
<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.


## Persistent Data
Persistent data values are stored on the device and preserved between launches of the app. The values are merged with any dictionary passed to a tracking call.

The [`persistentData().add()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-persistent-data/#add) method stores persistent data, as shown in the following example:

```swift
tealium?.persistentData()?.add(data: ["KEY":"VALUE"])
```

To clear data for specific keys use the [`persistentData.deleteData()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-persistent-data/#deletedata) method, or to delete all data use the [`persistentData.deleteAllData()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-persistent-data/#deletealldata) method.

The following example demonstrates these methods:

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// Adds persistent data to be sent on each hit until manually cleared		
  // - Parameter data: `[String: Any]` containing key-value pairs to be stored as persistent data
	func addPersistentData(_ data: [String: Any]) {

		self.tealium?.persistentData()?.add(data)
	}

	// Deletes persistent data for specific keys
	// - Parameter keys: `[String]` containing keys to be deleted
	func deleteData(for keys: [String]) {
		// clear data for specific keys
		self.tealium?.persistentData.deleteData(forKeys: keys)
		self.tealium?.persistentData.deleteAllData()
	}
}
```

## Volatile Data
Volatile data values are merged into to each event, but discarded upon closing the app and restarting. The values are merged with any dictionary passed to a tracking call.

The [`volatileData().add()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-volatile-data/#add) method stores volatile data.

To clear data for specific keys use the [`voltileData.deleteData()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-volatile-data/#deletedata) method, or to delete all data use the [`volatileData.deleteAllData()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-volatile-data/#deletealldata) method.

The following example demonstrates these methods:

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// Adds volatile data to be sent on each hit until the app is terminated
  // - Parameter data: `[String: Any]` containing key-value pairs to be stored as volatile data
	func addVolatileData(_ data: [String: Any]) {

		self.tealium?.volatileData()?.add(data)
	}

	// Deletes volatile data for specific keys
  // - Parameter keys: `[String]` containing keys to be deleted
	func deleteData(for keys: [String]) {
		// clear data for specific keys
		self.tealium?.volatileData.deleteData(forKeys: keys)
		self.tealium?.volatileData.deleteAllData()
	}
}
```
