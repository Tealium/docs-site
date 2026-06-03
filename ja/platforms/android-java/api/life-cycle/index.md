---
title: Lifecycle
description: Tealium for Androidで提供されているLifeCycleクラスおよびメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/life-cycle/
---
## クラス：`LifeCycle`

以下は、一般的に使用される `Lifecycle` クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
|`setupInstance()` | アプリケーションのライフサイクルインスタンスを構成します。|


### `setupInstance()`

アプリケーションのライフサイクルインスタンスを構成します。データが適切にトラッキングするようになるには、`Tealium.createInstance(config)`を呼び出す前にこのメソッドを呼び出す必要があります

```java
setupInstance(instanceId, config, isAutoTracking);
```

| パラメータ  | 型| 説明| 例|
| --- | ---| --- | --- |
| `instanceId` | `String` | Tealiumインスタンス名|  `&#34;abc123&#34;`  |
| `config` | `Tealium.Config` | Tealium構成オブジェクト|  `&#34;configObject&#34;`  |     
| `isAutoTracking` | `boolean` | 自動トラッキングが有効かどうか|  [`&#34;true&#34;`, `&#34;false&#34;`]|                      
