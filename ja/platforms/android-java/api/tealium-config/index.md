---
title: Tealium.Config
description: Tealium for Androidで提供されているTealium.Configクラスおよびメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/
---

## クラス：`Tealium.Config`

以下は、一般的に使用される`Tealium.Config`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| [`create()`](#create)| Create instance of the Config object |
| [`enableConsentManager()`](#enableconsentmanager)| Enable Consent Manager |
| [`isConsentManagerEnabled()`](#isconsentmanagerenabled)| Checks if Consent Manager is enabled |
| [`sessionCountingEnabled`](#sessioncountingenabled) | Tealium iQ accountsアカウント用のセッション カウントを無効化します。Tealium JavaScript ファイルをセルフホストしている場合にこれを用います|
| [`setDatasourceId()`](#setdatasourceid) | データソースキーを構成します|
| [`setForceOverrideLogLevel()`](#setforceoverrideloglevel) | 初期化時に特定のログレベルを強制するように構成します|
| [`setOverrideCollectDispatchProfile()`](#setoverridecollectdispatchprofile) | Tealium Collect プロファイルをオーバーライドします|
| [`setOverrideCollectDispatchUrl()`](#setoverridecollectdispatchurl) | Tealium Collect URLをオーバーライドします|
| [`setOverrideVisitorServiceDomain()`](#setoverridevisitorservicedomain) | Tealium Collect訪問サービスドメインをオーバーライドします|
| [`setSecondsBeforeBatchTimeout()`](#setsecondsbeforebatchtimeout) | バッチタイムアウトまでの秒数を構成します|

### `create()`

Configオブジェクトのインスタンスを作成します。

```java
Tealium.Config config = Tealium.Config.create(
      application,
      account,
      profile,
      environment);
```

Tealium `Config`インスタンスは、次のパラメータを使用して構成されます。

| パラメータ  | 型| 説明| 例|
| --- | ---| --- | --- |
| `application` | `Application` |アプリケーションインスタンス|  `applicationObj` |
| `account` | `String` |Tealiumアカウントの名前|  `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealiumプロファイルの名前|  `&#34;main&#34;` |
| `environment` | `String` |Tealium環境の名前|  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]|

### `enableConsentManager()`

Consent Managerを有効にします。このメソッドは、Tealiumの初期化前に使用します。

```java
public final String TEALIUM_INSTANCE = &#34;main&#34;;
final Tealium.Config config = Tealium.Config.create(...);
config.enableConsentManager(TEALIUM_INSTANCE);
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `instance` | `String` | Tealiumインスタンス名| `&#34;main&#34;` |

### `isConsentManagerEnabled()`

Consent Managerが有効かどうかを確認します。

```java
config.isConsentMangerEnabled()
```

### `sessionCountingEnabled`
Tealium iQ accountsアカウント用のセッション カウントを無効化します。Tealium JavaScript ファイルをセルフホストしている場合にこれを用います。デフォルトは `true`となっています。

```swift
config.sessionCountingEnabled = false
```

### `setDatasourceId()`

データソースキーを構成します。

```java
config.setDataSourceId(dataSourceId);
```
| パラメータ  | 型| 説明| 例|
| --- | ---| --- | --- |
| `dataSourceId` | `String` | データソースキー（ない場合は`null`に構成）| `&#34;abc123&#34;` |

### `setForceOverrideLogLevel()`

初期化時に特定のログレベルを強制するように構成します。メソッドチェーンの構成オブジェクトのインスタンスを返します。

```java
config.setForceOverrideLogLevel(forceOverrideLogLevel);
```

`forceOverrideLogLevel`には以下の`String`オプションを使用できます。

| ログレベル | 説明|
|------------ | -------------------------------|
| `&#34;dev&#34;`     | アクティビティ、情報提供、警告、エラー|
| `&#34;qa&#34;`      | 情報提供、警告、エラー|
| `&#34;prod&#34;`    | エラー|
| `&#34;silent&#34;`  | なし|

### `setOverrideCollectDispatchProfile()`

Tealium Collect ディスパッチ プロファイルをオーバーライドします。

```java
config.setOverrideCollectDispatchProfile(profile);
```

| パラメータ  | 型| 説明|
| --- | ---| --- |
| `profile` | `String` | Tealium Collect プロファイルのオーバーライド|


### `setOverrideCollectDispatchUrl()`

データを別のエンドポイントに送信するようにTealium CollectのディスパッチURLをオーバーライドします。

```java
config.setOverrideCollectDispatchUrl(url);
```

| パラメータ  | 型| 説明|
| --- | ---| --- |
| `url` | `String` | オーバーライドするURL|

デフォルトのURLは次のとおりです。
```bash
https://collect.tealiumiq.com/event/
```
イベントバッチ処理を使用するデフォルトのURLは次のとおりです。
```bash
https://collect.tealiumiq.com/bulk-event/
```
このメソッドは通常、カスタムホスト名を構成するため、または特定の地域のホスト名を構成するために使用されます。次の例では、Tealium CollectのベースURLが中央ヨーロッパ地域内に留まるように構成されます。

```java
config.setOverrideCollectDispatchUrl(&#34;https://collect-eu-central-1.tealiumiq.com/event/&#34;);
```


### `setOverrideVisitorServiceDomain()`

データを別のドメインに送信するようにTealium Collectの訪問サービスドメインをオーバーライドします。

```java
config.setOverrideVisitorServiceDomain(domain);
```

| パラメータ  | 型| 説明|
| --- | ---| --- |
| `domain` | `String` | オーバーライドする訪問サービスドメイン|

### `setSecondsBeforeBatchTimeout()`

バッチタイムアウトまでの秒数を構成します。タイムアウトに達する前にバッチサイズの制限に達しなかった場合、キューに入れられたイベントはディスパッチされます。

```java
config.setSecondsBeforeBatchTimeout(timeout);
```

| パラメータ  | 型| 説明| 例|
| --- | ---| --- | --- |
| `timeout` | `int` |バッチが送信されるまでのタイムアウト時間（秒単位）。| `30` |

