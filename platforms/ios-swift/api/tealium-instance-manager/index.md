---
title: TealiumInstanceManager
description: Provides a method of accessing a previously instantiated instance of Tealium using the key format account.profile.environment.
url: https://docs.tealium.com/platforms/ios-swift/api/tealium-instance-manager/
---
## Class: `TealiumInstanceManager`

The following summarizes the commonly used methods of the iOS (Swift) `TealiumInstanceManager` class.

| Method | Description |
| ----- | ------ |
| [`getInstanceByName()`](#getinstancebyname) | Returns a Tealium instance for a specified account/profile/environment key |
| [`removeInstance()`](#removeinstance) | Removes a Tealium instance for a specified `TealiumConfig` instance |
| [`removeInstanceForKey()`](#removeinstanceforkey) | Removes a Tealium instance for a specified key (format: `ACCOUNT.PROFILE.ENVIRONMENT`)|



### `getInstanceByName()`

Returns a Tealium instance for a specified key in the following format: `ACCOUNT.PROFILE.ENVIRONMENT`.

```swift
getInstanceByName(instanceKey: String) -&gt; Tealium?
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `instanceKey`| `String`  | The specified key of the `Tealium` instance to be retrieved | `companyXYZ.main.dev` |      

The following example shows how to get a Tealium instance for a specified account/profile/environment key:

```swift
let instanceManager = TealiumInstanceManager.shared
let myTealiumInstance = instanceManager.getInstanceByName(&#34;ACCOUNT.PROFILE.ENVIRONMENT&#34;)
// call any methods on the Tealium instance you just retrieved
// myTealiumInstance?.track(&#34;myevent&#34;)
```
### `removeInstance()`

Removes (deallocates) a Tealium instance for a specified `TealiumConfig` instance. If neither this method nor the `removeInstanceForKey()` method is called, then a permanent reference is held and the instance is not removed.

```swift
removeInstance(config)
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `config`| `TealiumConfig`  | The Tealium configuration instance to be removed | `myTealiumConfig` |      

The following example removes a Tealium instance for a specified account/profile/environment key:

```swift
instanceManager.removeInstance(myTealiumConfig)
```

### `removeInstanceForKey()`

Removes (deallocates) a Tealium instance for a specified key (format: `ACCOUNT.PROFILE.ENVIRONMENT`). If neither this method nor the `removeInstance()` method is called, then a permanent reference is held and the instance is not removed.

```swift
removeInstanceForKey(instanceKey)
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `instanceKey`| `String`  | The specified key of the `Tealium` instance to be removed | `&#34;companyXYZ.main.dev&#34;` |      

The following example removes a Tealium instance for a specified account/profile/environment key:

```swift
let instanceManager = TealiumInstanceManager.shared
instanceManager.removeInstanceForKey(&#34;ACCOUNT.PROFILE.ENVIRONMENT&#34;)
```


**`tealiumInstances` variable**  
Stores a dictionary of all registered Tealium instances.

The following example shows how to use the variable to retrieve all registered Tealium instances:

```swift
let instanceManager = TealiumInstanceManager.shared
let allTealiumInstances = instanceManager.tealiumInstances
// do any required processing with the dictionary of valid Tealium instances
```
