---
title: TealiumInstanceManager
description: アカウント.profile.environmentのキーフォーマットを使用して、以前にインスタンス化されたTealiumのインスタンスにアクセスする方法を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-instance-manager/
---
## クラス: `TealiumInstanceManager`

以下は、iOS（Swift）の`TealiumInstanceManager`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| [`getInstanceByName()`](#getinstancebyname) | 指定したアカウント/プロファイル/環境キーのTealiumインスタンスを返します |
| [`removeInstance()`](#removeinstance) | 指定した`TealiumConfig`インスタンスのTealiumインスタンスを削除します |
| [`removeInstanceForKey()`](#removeinstanceforkey) | 指定したキー（形式：`ACCOUNT.PROFILE.ENVIRONMENT`）のTealiumインスタンスを削除します |



### `getInstanceByName()`

以下の形式の指定したキーのTealiumインスタンスを返します：`ACCOUNT.PROFILE.ENVIRONMENT`。

```swift
getInstanceByName(instanceKey: String) -&gt; Tealium?
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `instanceKey`| `String`  | 取得する`Tealium`インスタンスの指定キー | `companyXYZ.main.dev` |      

以下の例は、指定したアカウント/プロファイル/環境キーのTealiumインスタンスを取得する方法を示しています：

```swift
let instanceManager = TealiumInstanceManager.shared
let myTealiumInstance = instanceManager.getInstanceByName(&#34;ACCOUNT.PROFILE.ENVIRONMENT&#34;)
// 取得したTealiumインスタンスで任意のメソッドを呼び出す
// myTealiumInstance?.track(&#34;myevent&#34;)
```
### `removeInstance()`

指定した`TealiumConfig`インスタンスのTealiumインスタンスを削除（デアロケート）します。このメソッドまたは`removeInstanceForKey()`メソッドのいずれも呼び出されない場合、永続的な参照が保持され、インスタンスは削除されません。

```swift
removeInstance(config)
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `config`| `TealiumConfig`  | 削除するTealium構成インスタンス | `myTealiumConfig` |      

以下の例は、指定したアカウント/プロファイル/環境キーのTealiumインスタンスを削除する方法を示しています：

```swift
instanceManager.removeInstance(myTealiumConfig)
```

### `removeInstanceForKey()`

指定したキー（形式：`ACCOUNT.PROFILE.ENVIRONMENT`）のTealiumインスタンスを削除（デアロケート）します。このメソッドまたは`removeInstance()`メソッドのいずれも呼び出されない場合、永続的な参照が保持され、インスタンスは削除されません。

```swift
removeInstanceForKey(instanceKey)
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `instanceKey`| `String`  | 削除する`Tealium`インスタンスの指定キー | `&#34;companyXYZ.main.dev&#34;` |      

以下の例は、指定したアカウント/プロファイル/環境キーのTealiumインスタンスを削除する方法を示しています：

```swift
let instanceManager = TealiumInstanceManager.shared
instanceManager.removeInstanceForKey(&#34;ACCOUNT.PROFILE.ENVIRONMENT&#34;)
```


**`tealiumInstances` 変数**  
すべての登録済みTealiumインスタンスの辞書を保存します。

以下の例は、この変数を使用してすべての登録済みTealiumインスタンスを取得する方法を示しています：

```swift
let instanceManager = TealiumInstanceManager.shared
let allTealiumInstances = instanceManager.tealiumInstances
// 有効なTealiumインスタンスの辞書で必要な処理を行う
```
