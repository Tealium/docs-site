---
title: Tealium.Config
description: Android向けにTealiumが提供するTealium.Configクラスおよびメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/tealium-config/
---

## クラス：`Tealium.Config`

以下に、`Tealium.Config`クラスでよく使用されるメソッドの概要を示します。

| メソッド | 説明 |
| ----- | ------ |
| [`create()`](#create)| Configオブジェクトのインスタンスを作成します |
| [`enableConsentManager()`](#enableconsentmanager)| 同意管理を有効にします |
| [`isConsentManagerEnabled()`](#isconsentmanagerenabled)| 同意管理が有効かどうかを確認します |
| [`sessionCountingEnabled`](#sessioncountingenabled) | タグ管理アカウントのセッションカウントを無効にします。Tealium JavaScriptファイルをセルフホスティングする場合に使用します |
| [`setDatasourceId()`](#setdatasourceid) | データソースキーを構成します |
| [`setForceOverrideLogLevel()`](#setforceoverrideloglevel) | 初期化時に特定のログレベルを強制的に適用するよう構成します |
| [`setOverrideCollectDispatchProfile()`](#setoverridecollectdispatchprofile) | Tealium Collectプロファイルを上書きします |
| [`setOverrideCollectDispatchUrl()`](#setoverridecollectdispatchurl) | Tealium Collect URLを上書きします |
| [`setOverrideVisitorServiceDomain()`](#setoverridevisitorservicedomain) | Tealium Collect訪問サービスドメインを上書きします |
| [`setSecondsBeforeBatchTimeout()`](#setsecondsbeforebatchtimeout) | バッチがタイムアウトするまでの秒数を構成します |

### `create()`

Configオブジェクトのインスタンスを作成します。

```java
Tealium.Config config = Tealium.Config.create(
      application,
      account,
      profile,
      environment);
```

Tealiumの`Config`インスタンスは、次のパラメータを使用して構成されます。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `application` | `Application` | アプリケーションのインスタンス | `applicationObj` |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ"` |
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 | [`"dev"`, `"qa"`, `"prod"`] |

### `enableConsentManager()`

同意管理を有効にします。このメソッドは、Tealiumを初期化する前に使用します。

```java
public final String TEALIUM_INSTANCE = "main";
final Tealium.Config config = Tealium.Config.create(...);
config.enableConsentManager(TEALIUM_INSTANCE);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `instance` | `String` | Tealiumインスタンス名 | `"main"` |

### `isConsentManagerEnabled()`

同意管理が有効かどうかを確認します。

```java
config.isConsentMangerEnabled()
```

### `sessionCountingEnabled`

タグ管理アカウントのセッションカウントを無効にします。Tealium JavaScriptファイルをセルフホスティングする場合に使用します。デフォルトは`true`です。

```swift
config.sessionCountingEnabled = false
```

### `setDatasourceId()`

データソースキーを構成します。

```java
config.setDataSourceId(dataSourceId);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `dataSourceId` | `String` | データソースキー（存在しない場合は`null`に構成） | `"abc123"` |

### `setForceOverrideLogLevel()`

初期化時に特定のログレベルを強制的に適用するよう構成します。メソッドチェーン用にConfigオブジェクトのインスタンスを返します。

```java
config.setForceOverrideLogLevel(forceOverrideLogLevel);
```

`forceOverrideLogLevel`には、次の`String`オプションを使用できます。

| ログレベル | 説明 |
|------------ | ------------------------------- |
| `"dev"`     | アクティビティ、情報、警告、およびエラー |
| `"qa"`      | 情報、警告、およびエラー |
| `"prod"`    | エラー |
| `"silent"`  | なし |

### `setOverrideCollectDispatchProfile()`

Tealium Collectの送信プロファイルを上書きします。

```java
config.setOverrideCollectDispatchProfile(profile);
```

| パラメータ | 型 | 説明 |
| --- | --- | --- |
| `profile` | `String` | 上書きするTealium Collectプロファイル |


### `setOverrideCollectDispatchUrl()`

Tealium Collectの送信URLを上書きし、別のエンドポイントにデータを送信します。

```java
config.setOverrideCollectDispatchUrl(url);
```

| パラメータ | 型 | 説明 |
| --- | --- | --- |
| `url` | `String` | 上書きするURL |

デフォルトのURLは次のとおりです。  
```bash
https://collect.tealiumiq.com/event/
```

イベントのバッチ処理を使用する場合のデフォルトURLは次のとおりです。

```bash
https://collect.tealiumiq.com/bulk-event/
```

通常、このメソッドはカスタムホスト名または特定のリージョンのホスト名を構成するために使用します。次の例では、EU中央リージョン内にデータを保持するようにTealium CollectのベースURLを構成します。

```java
config.setOverrideCollectDispatchUrl("https://collect-eu-central-1.tealiumiq.com/event/");
```


### `setOverrideVisitorServiceDomain()`

Tealium Collectの訪問サービスドメインを上書きし、別のドメインにデータを送信します。

```java
config.setOverrideVisitorServiceDomain(domain);
```

| パラメータ | 型 | 説明 |
| --- | --- | --- |
| `domain` | `String` | 上書きする訪問サービスドメイン |

### `setSecondsBeforeBatchTimeout()`

バッチがタイムアウトするまでの秒数を構成します。タイムアウトに達するまでにバッチサイズの上限に達しなかった場合、キューに格納されているイベントが送信されます。

```java
config.setSecondsBeforeBatchTimeout(timeout);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `timeout` | `int` | バッチが送信されるまでのタイムアウト時間（秒）。 | `30` |