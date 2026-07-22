---
title: ティリウム
description: ティリウムが提供するAndroid用のTealiumクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/tealium/
---

## クラス: `Tealium`

以下は、`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `createInstance()`| 新しいTealium Multitonを作成します |
| `disableConsentManager()`| Consent Managerを無効にします |
| `getConsentManager()`| Consent Managerが有効な場合、そのインスタンスを返します |
| `requestFlush()` | イベントのバッチキューをディスパッチするリクエスト |
| `trackEvent()` | イベントをトラックします |
| `trackView()` | 表示されたビューをトラックします |


### `createInstance()`

新しいTealium Multitonを作成し、新しく作成されたインスタンスを返します。インスタンスは`getInstance()`でアクセス可能で、`destroyInstance()`で破棄可能です。複数のインスタンスがサポートされています。

```java
Tealium.createInstance(key, config);
```
| パラメータ  | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` |新しいTealiumインスタンスの名前 |  `"abc123"` |
| `config` | `Tealium.Config` | 新しいインスタンスの設定 | `tealConfigObj` |

| 戻り値 | 戻り値のタイプ |
| --- | --- |
| Tealium Multiton | `Tealium` |

### `disableConsentManager()`

Consent Managerを無効にします。Tealiumが完全に初期化された後にこのメソッドを呼び出してConsent Managerを無効にします。

```java
final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);

tealiumInstance.disableConsentManager();
```

### `getConsentManager()`

Consent Managerが有効な場合、そのインスタンスを返します。

```java
final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);

ConsentManager consentManager = tealiumInstance.getConsentManager();
```

| 戻り値 | 戻り値のタイプ |
| --- | --- |
| Consent Manager | `ConsentManager` |

### `requestFlush()`

バッチ制限が達成されていない場合にイベントのバッチキューをディスパッチするリクエストをします。他のすべてのディスパッチチェックがOKの場合（オンライン、同意管理、ディスパッチバリデータ）、キューはディスパッチされます。

```java
Tealium instance = Tealium.getInstance("my_instance_name");
instance.requestFlush();
```


### `trackEvent()`

非ビューイベントをトラックします。

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackEvent(eventName, data);
```

| パラメータ | タイプ | 説明  | 例 |
|-----------|-------------| ---- | ------- |
| `eventName`| `String` |非ビューイベントの名前 | `"Button Click"` |
| `data`    |`[Map<String, dynamic>]` | (オプション) キーと値のペアとしてのイベントデータ（ない場合は`null`を使用）| `{"key1": "value1"}` |


### `trackView()`

表示されたビューをトラックします。

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackView(screenName, data);
```
| パラメータ | タイプ | 説明 | 例 |
|-----------|------| ---- | ------- |
| `screenName`| `String` | ビューのスクリーン名 | `"Home screen"` |
| `data`    | `[Map<String, dynamic>]` | (オプション) キーと値のペアとしてのイベントデータ（ない場合は`null`を使用）| `{"key1": "value1"}` |

