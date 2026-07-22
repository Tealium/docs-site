---
title: ライフサイクル
description: Tealium for Android (Kotlin)によって提供されるLifecycleクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/lifecycle/
---
## クラス: `Lifecycle`

以下は、アプリケーションのライフサイクルを手動で追跡するための`Lifecycle`クラスのメソッドをまとめたものです。Lifecycleモジュールがライフサイクルイベントを手動で追跡するようにするには、`TealiumConfig`オプションの`isAutotrackingEnabled`を`false`に構成して、ライフサイクルの自動追跡を無効にします。手動でのライフサイクル追跡の使用は、非標準的なライフサイクルパラダイムに対してのみ推奨されます。

| メソッド | 説明 |
| ----- | ------ |
|[`trackLaunchEvent()`](#tracklaunchevent) | 手動で起動イベントを追跡します |
|[`trackSleepEvent()`](#tracksleepevent) | 手動でスリープイベントを追跡します |
|[`trackWakeEvent()`](#trackwakeevent) | 手動でウェイクイベントを追跡します |

### `trackLaunchEvent()`

オプションのデータマップを使用して、手動で起動イベントを追跡します。

```java
tealiumInstance.lifecycle?.trackLaunchEvent(mapOf("key" to "launch-value"))
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | 起動イベントと一緒に送信するカスタムデータのマップ | mapOf("key" to "launch-value") |

### `trackSleepEvent()`

オプションのデータマップを使用して、手動でスリープイベントを追跡します。

```java
tealiumInstance.lifecycle?.trackSleepEvent(mapOf("key" to "sleep-value"))
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | スリープイベントと一緒に送信するカスタムデータのマップ | mapOf("key" to "sleep-value") |

### `trackWakeEvent()`

オプションのデータマップを使用して、手動でウェイクイベントを追跡します。

```java
tealiumInstance.lifecycle?.trackWakeEvent(mapOf("key" to "wake-value"))
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | ウェイクイベントと一緒に送信するカスタムデータのマップ | mapOf("key" to "wake-value") |
