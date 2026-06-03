---
title: API リファレンス
description: TealiumのReact Native用クラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/react-native/api/
---
## クラス: `Tealium`

以下は、React Nativeライブラリ用の`Tealium`クラスで一般的に使用されるメソッドをまとめたものです。

| メソッド                                                      | 説明                                                           |
|:------------------------------------------------------------|:--------------------------------------------------------------|
| [`addRemoteCommand()`](#addRemoteCommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します                   |
| [`addData()`](#addData)                                     | 永続データレイヤーにデータを追加します                                    |
| [`gatherTrackData()`](#gatherTrackData)                     | コレクターとデータレイヤーからすべてのトラックデータを収集します                 |
| [`getData()`](#getData)                                     | データレイヤーから指定された値を取得します                       |
| [`getConsentCategories()`](#getConsentCategories)           | ユーザーの同意したカテゴリを取得します                             |
| [`getConsentStatus()`](#getConsentStatus)                   | ユーザーの同意状態を取得します                                   |
| [`getSessionId()`](#getSessionId)                           | 現在の`tealium_session_id`を取得します                            |
| [`getVisitorId()`](#getVisitorId)                           | 現在の訪問IDを取得します                                      |
| [`initialize()`](#initialize)                               | 構成パラメータを使用してTealiumを初期化します                     |
| [`joinTrace()`](#joinTrace)                                 | 与えられたIDでトレースに参加します                                       |
| [`leaveTrace()`](#leaveTrace)                               | アクティブなトレースセッションを離れます                                           |
| [`removeData()`](#removeData)                               | `addData()`を使用して以前に構成された永続データを削除します |
| [`removeRemoteCommand()`](#removeRemoteCommand)             | リモートコマンドマネージャーからリモートコマンドを削除します              |
| [`setConsentCategories()`](#setConsentCategories)           | ユーザーの同意カテゴリを構成します                                 |
| [`setConsentExpiryListener()`](#setConsentExpiryListener)   | 同意期限が切れたときのリスナー/コールバックを構成します                            |
| [`setConsentStatus()`](#setConsentStatus)                   | ユーザーの同意状態を構成します                                     |
| [`setVisitorServiceListener()`](#setVisitorServiceListener) | 訪問サービスのリスナー/コールバックを定義します                         |
| [`terminateInstance()`](#terminateInstance)                 | Tealiumインスタンスを無効にして破棄します                            |
| [`track()`](#track)                                         | イベントまたは画面表示をトラックします                                         |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
Tealium.addRemoteCommand(id, callback);
```

| パラメータ | タイプ        | 説明                                                                                                                                                     | 例          |
|:-----------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | タグ構成からのコマンドIDの名前                                                                                                                           | `&#34;test_command&#34;` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキーと値のペアのペイロードを返します。 | (例を参照)    |

例:

```javascript
Tealium.addRemoteCommand(&#34;firebase&#34;, payload =&gt; {

  var eventName = payload[&#34;firebase_event_name&#34;];
  var eventProperties = payload[&#34;firebase_event_properties&#34;];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`

指定された有効期限で永続データ保存にデータを追加します。

```javascript
Tealium.addData(data, expiry);
```
| パラメータ | タイプ                | 説明                                                                                                   | 例                                   |
|:-----------|:--------------------|:------------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | 文字列のキーと、値が文字列または文字列の配列であるキーバリューペアのJSONオブジェクト | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |
| `expiry`   | [`Expiry`](#expiry) | データを永続させる時間の長さ                                                                  | `Expiry.forever`                          |

### コレクター

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hubに送信される前にデータレイヤーに追加するモジュールです。いくつかのコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてインストールされています。

以下の表は、利用可能なコレクターをリストしています。デフォルトのコレクターはコレクター名の隣に`*`が付けられています。

| コレクター名   | TealiumConfig 参照     |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

これらのモジュールは、以下に説明されている[`TealiumConfig`](#tealiumconfig)の`collectors`プロパティを使用して有効または無効にされます

### ConsentExpiry

同意の構成の有効期限を定義します

| パラメータ | タイプ       | 説明                          | 例         |
|:-----------|:-----------|:-----------------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間 | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位   | `TimeUnit.days` |

例:

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| 値    | 説明 |
|:---------|:------------|
| .minutes | 分     |
| .hours   | 時間       |
| .months  | 月      |
| .days    | 日        |

### ConsentPolicy

遵守すべき同意ポリシーを定義します。[`TealiumConfig`](#tealiumconfig)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例:

`ConsentPolicy.gdpr`

| 値 | 説明 |
|:------|:------------|
| .gdpr | GDPR        |
| .ccpa | CCPA        |

### ディスパッチャー

ディスパッチャーは、データレイヤーからのデータを収集し、Tealiumのエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは以下の通りです:

| ディスパッチャー名  | TealiumConfig 参照      |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |

少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはどこにも送信されません。
### 有効期限

カスタムデータの有効期限を定義します。

例：

`Expiry.session`

| パラメータ | タイプ       | 説明                              | 例               |
|:-----------|:-----------|:----------------------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間                | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間の単位          | `TimeUnit.days` |

例：

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| 値         | 説明       |
|:-----------|:-----------|
| .minutes   | 分         |
| .hours     | 時間       |
| .months    | 月         |
| .days      | 日         |

### `gatherTrackData()`

コレクターやデータレイヤーからすべてのトラックデータを収集します。

```javascript
Tealium.gatherTrackData(callback);
```

| パラメータ | タイプ       | 説明                                          | 例               |
|:-----------|:-----------|:---------------------------------------------|:----------------|
| `callback` | `Function` | 取得した値を使用するコールバック関数。コールバックはJSONオブジェクトを返します。 | (例を参照) |

例：

```javascript
Tealium.gatherTrackData(value =&gt; {
   console.log(&#34;Track data: &#34; &#43; JSON.stringify(value))
});
```

### `getData()`

永続データレイヤーで指定されたキーの値を取得し、コールバック関数の形で返します。

```javascript
Tealium.getData(key, callback);
```

| パラメータ | タイプ       | 説明                                          | 例               |
|:-----------|:-----------|:---------------------------------------------|:----------------|
| `key`      | `String`   | データレイヤーから取得するキー                | (例を参照) |
| `callback` | `Function` | 取得した値を使用するコールバック関数 | (例を参照) |

例：

```javascript
Tealium.getData(&#39;test_session_key&#39;, value =&gt; {
   console.log(&#34;Value: &#34; &#43; value)
});
```

### `getConsentCategories()`

ユーザーの同意したカテゴリを取得します。

```javascript
Tealium.getConsentCategories(callback);
```

| パラメータ | タイプ       | 説明                                     | 例               |
|:-----------|:-----------|:----------------------------------------|:----------------|
| `callback` | `Function` | 同意カテゴリを使用するコールバック関数   | (例を参照) |

例：

```javascript
Tealium.getConsentCategories(categories =&gt; {
    console.log(&#34;Consent Categories: &#34; &#43; categories)
});
```

### `getConsentStatus()`

ユーザーの同意状態を取得し、コールバック関数の形で返します。

```javascript
Tealium.getConsentStatus(callback);
```

| パラメータ | タイプ       | 説明                                 | 例               |
|:-----------|:-----------|:------------------------------------|:----------------|
| `callback` | `Function` | 同意状態を使用するコールバック関数   | (例を参照) |

例：

```javascript
Tealium.getConsentStatus(status =&gt; {
    console.log(&#34;Consent Status: &#34; &#43; status)
});
```

### `getSessionId()`

現在のセッションIDを取得し、コールバック関数の形で返します。

```javascript
Tealium.getSessionId(callback);
```

| パラメータ | タイプ       | 説明                             | 例               |
|:-----------|:-----------|:--------------------------------|:----------------|
| `callback` | `Function` | セッションIDを使用するコールバック関数 | (例を参照) |

例：

```javascript
Tealium.getSessionId(value =&gt; {
    console.log(&#34;Sesssion ID: &#34; &#43; value)
});
```

### `getVisitorId()`

ユーザーのビジターIDを取得し、コールバック関数の形で返します。

```javascript
Tealium.getVisitorId(callback);
```

| パラメータ | タイプ       | 説明                             | 例               |
|:-----------|:-----------|:--------------------------------|:----------------|
| `callback` | `Function` | ビジターIDを使用するコールバック関数 | (例を参照) |

例：

```javascript
Tealium.getVisitorId(value =&gt; {
    console.log(&#34;Visitor ID: &#34; &#43; value)
});
```

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```javascript
Tealium.initialize(config);
```

| パラメータ | タイプ                              | 説明                                                      | 例               |
|:-----------|:----------------------------------|:---------------------------------------------------------|:----------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealiumの構成パラメータ                                   | (例を参照) |
| `callback` | `Function`                        | (オプション) Tealiumインスタンスが準備できた後のコールバック関数 | (例を参照) |

例：

```javascript
let config: TealiumConfig =
{
	account: &#39;tealiummobile&#39;,
	profile: &#39;demo&#39;,
	environment: TealiumEnvironment.dev,
	dispatchers: [Dispatchers.Collect,
	 			  Dispatchers.TagManagement,
	  			  Dispatchers.RemoteCommands],
	collectors: [Collectors.AppData,
				 Collectors.DeviceData,
				 Collectors.Lifecycle,
				 Collectors.Connectivity],
	consentLoggingEnabled: true,
	consentPolicy: ConsentPolicy.gdpr,
	visitorServiceEnabled: true
};

Tealium.initialize(config, success =&gt; {
    if (!success) {
        // インスタンスの作成に失敗しました。
    }
    // 準備ができたら何かを行います
});
```

### `joinTrace()`

指定されたIDでトレースに参加します。Tealium Customer Data Hubの[Trace]()機能についてもっと学びましょう。

```javascript
Tealium.joinTrace(id);
```

| パラメータ | タイプ     | 説明                       | 例          |
|:-----------|:---------|:--------------------------|:-----------|
| `id`       | `String` | CDHから取得したトレースID | `abc123xy` |

### `leaveTrace()`

`leaveTrace()`メソッドが呼ばれるまで、トレースはアプリセッションの間アクティブのままです。このメソッドは以前に参加したトレースを離れ、訪問セッションを終了します。

```javascript
Tealium.leaveTrace();
```

### LogLevel

ログレベルプロパティを構成し、どれだけの情報がログに記録されるかを以下の値のいずれかで制御します：

| 値         | 説明                                                         |
|:----------|:------------------------------------------------------------|
| `.dev`    | アプリケーションの進行を強調する情報イベント                 |
| `.qa`     | アプリケーションのデバッグに使用されるデバッグレベルのイベント |
| `.prod`   | 重大なエラーや失敗などのエラーイベント                       |
| `.silent` | ログなし（デフォルト）                                       |

例：

`LogLevel.dev`

### `setConsentCategories()`

ユーザーの同意カテゴリを構成します。カテゴリの配列を渡して構成します。デフォルトは、`ConsentStatus`が`.consented`に構成されるまで空の配列です。同意状態が`.consented`で`setConsentCategories()`メソッドでカテゴリが指定されていない場合、すべてのカテゴリが構成されます。

```javascript
Tealium.setConsentCategories(categories);
```

| パラメータ   | タイプ                  | 説明                       | 例                                                        |
|:-------------|:----------------------|:--------------------------|:-----------------------------------------------------------|
| `categories` | `ConsentCategories[]` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```
#### 同意カテゴリー

| 値                  | 説明             |
|:------------------|:----------------|
| `analytics`       | アナリティクス   |
| `affiliates`      | アフィリエイト   |
| `displayAds`      | ディスプレイ広告 |
| `email`           | メール           |
| `personalization` | パーソナライゼーション |
| `search`          | 検索             |
| `social`          | ソーシャル       |
| `bigData`         | ビッグデータ     |
| `mobile`          | モバイル         |
| `engagement`      | エンゲージメント |
| `monitoring`      | モニタリング     |
| `crm`             | CRM             |
| `cdp`             | CDP             |
| `cookieMatch`     | クッキーマッチ   |
| `misc`            | その他           |

### `setConsentExpiryListener()`

ユーザーの同意構成が期限切れになった後に実行するコールバックを定義します。[`ConsentExpiry`](#consentexpiry)に従います。

```javascript
Tealium.setConsentExpiryListener(callback);
```

| パラメータ | タイプ       | 説明                               | 例             |
|:-----------|:-----------|:--------------------------------------|:--------------|
| `callback` | `Function` | 同意が期限切れになった後に実行するコード | (例を参照) |

例:

```javascript
Tealium.setConsentExpiryListener(() =&gt; {
    console.log(&#34;Consent Expired&#34;);
});
```

### `setConsentStatus()`

ユーザーの同意状態を構成します。デフォルトは `.unknown` で、変更されるまでそのままです。

```javascript
Tealium.setConsentStatus(status);
```

| パラメータ | タイプ            | 説明             | 例                           |
|:-----------|:----------------|:--------------------|:--------------------------|
| `status`   | `ConsentStatus` | ユーザーの同意状態 | `ConsentStatus.consented` |

例:

```javascript
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### 同意状態

| 値                  | 説明             |
|:----------------|:--------------|
| `.consented`    | 同意済み       |
| `.notConsented` | 同意していない |
| `.unknown`      | 不明           |

### `setVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](#visitorprofile)がコールバックの応答で提供されます。

VisitorServiceモジュールはTealium Customer Data Hubの[Data Layer Enrichment]()機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを持っており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させたい場合に推奨されます。AudienceStreamのライセンスを持っていない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```javascript
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | タイプ       | 説明                                                   | 例             |
|:-----------|:-----------|:--------------------------------------------------------------|:--------------|
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード | (例を参照) |

例:

```javascript
Tealium.setVisitorServiceListener(profile =&gt; {
    console.log(JSON.stringify(profile[&#34;audiences&#34;]));
});
```

### `removeData()`

以前に`Tealium.setPersistentData()`を使用して構成された永続データを削除します。

```javascript
Tealium.removeData(keys);
```

| パラメータ | タイプ       | 説明            | 例                |
|:-----------|:-----------|:-------------------|:-----------------|
| `keys`     | `String[]` | キー名の配列       | `[&#34;foo&#34;, &#34;bar&#34;]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
Tealium.removeRemoteCommand(id);
```

| パラメータ | タイプ     | 説明                          | 例                |
|:-----------|:---------|:---------------------------------|:-----------------|
| `id`       | `String` | 削除するコマンドIDの名前       | `&#34;test_command&#34;` |

例:

```javascript
Tealium.removeRemoteCommand(&#34;firebase&#34;);
```

### TealiumEnvironment

環境はデフォルトの3つの環境（Dev, QA, Prod）またはTealiumが公開する任意のカスタム環境のいずれかです。これらの環境のいずれかを選択します。

例:

`TealiumEnvironment.dev`

| 値       | 説明         |
|:--------|:------------|
| `.dev`  | 開発         |
| `.qa`   | QA/UAT      |
| `.prod` | 本番         |
### TealiumConfig

以下は、`TealiumConfig` クラスのプロパティについての要約です。

| パラメータ                         | タイプ                                          | 説明                                                                                                                                                                                                                                                       | 例                                                                                                            |
|:-------------------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | （必須）Tealiumアカウント名                                                                                                                                                                                                                                 | `&#34;companyXYZ&#34; `                                                                                               |
| `profile`                      | `String`                                    | （必須）Tealiumプロファイル名                                                                                                                                                                                                                               | `&#34;main&#34;`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium環境名                                                                                                                                                                                                                                       | `&#34;TealiumEnvironment.dev&#34;`                                                                                    |
| `dataSource`                   | `String`                                    | CDHデータソースキー                                                                                                                                                                                                                                         | `&#34;abc123&#34;`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | （必須）Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成します                                                                                                                                                                  | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | （必須）Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成します                                                                                                                                                                | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | カスタムビジターIDを構成します                                                                                                                                                                                                                              | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | DeviceDataモジュールでのメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                        | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Tealium Collect URLをオーバーライドして、データを別のエンドポイントに送信します。イベントバッチ機能を使用する場合は、`overrideCollectBatchURL`プロパティもオーバーライドしてください。                                                                 | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Tealium CollectバッチURLをオーバーライドして、データを別のエンドポイントに送信します。                                                                                                                                                                       | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Tealium Collectプロファイルをオーバーライドして、データを別のTealiumプロファイルに送信します。                                                                                                                                                               | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Tealium Collect URLのドメイン名をオーバーライドして、データを別のエンドポイントに送信します。                                                                                                                                                               | `custom-domain`                                                                                               |
| `overrideLibrarySettingsURL`   | `String`                                    | 公開構成URLをオーバーライドします。                                                                                                                                                                                                                         | `https://custom-domain.com/mobile.html`                                                                       |
| `overrideTagManagementURL`     | `String`                                    | タグ管理モジュールで使用されるデフォルトURLをオーバーライドします。これは、TealiumのJavaScriptファイルを自己ホスティングする場合に必要です。                                                                                                               | `https://custom-domain.com/path/env/utag.js`                                                                  |
| `deepLinkTrackingEnabled`      | `Boolean`                                   | [標準的なディープリンクの自動追跡](/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします。これには、FacebookなどのソースからアプリへのリンクやQRトレースなどが含まれます（デフォルト：有効）。                                  | `false`                                                                                                       |
| `qrTraceEnabled`               | `Boolean`                                   | QRトレースを有効または無効にします。 (デフォルト: 有効)                                                                                                                                                           | `false`                                                                                                       |
| `loglevel`                     | [`LogLevel`](#loglevel)                     | ログレベルプロパティを構成し、どれだけの情報がログに記録されるかを制御します (デフォルト: サイレント)                                                                                                                                                                | `LogLevel.dev`                                                                                                |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | ユーザーの同意の有効期限を構成します。 (デフォルトはポリシーに依存)                                                                                                                                                                     | `ConsentExpiry(90, TimeUnit.days)`                                                                            |
| `consentLoggingEnabled`        | `Boolean`                                   | 同意ログ機能を有効にします。これにより、すべての同意状態の変更が監査目的でTealium Customer Data Hubに送信されます。 (デフォルト: 有効)   | true                                                                                                          |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | 同意ポリシーを構成します。例えば、CCPAやGDPRなどです。このプロパティが構成されている場合のみConsent Managerが有効になります。                                                                                                                                                        | `ConsentPolicy.gdpr`                                                                                          |
| `lifecycleAutotrackingEnabled` | `Boolean`                                   | ライフサイクル自動追跡を有効または無効にします。 (デフォルト: 有効)                                                                                                                                                                                             | `false`                                                                                                       |
| `useRemoteLibrarySettings`     | `Boolean`                                   | モバイルパブリッシュ構成を有効または無効にします。 (デフォルト: 有効) Tealium iQタグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にします。 | `false`                                                                                                       |
| `visitorServiceEnabled`        | `Boolean`                                   | データレイヤーエンリッチメントAPIを使用して訪問プロファイルの自動取得を有効または無効にします。 (デフォルト: 無効)                                | `true`                                                                                                        |
| `sessionCountingEnabled`       | `Boolean`                                   | Tealium iQアカウントのセッションカウントを有効または無効にします。TealiumのJavaScriptファイルを自己ホスティングしている場合は、これを`false`に構成します。 (デフォルト: 有効)                                                                                                            | `false`                                                                                                        |
| `remoteCommands`               | `RemoteCommand[]`                           | インスタンスが準備ができたときに追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成します                                                                                                                                                                    | `[{ id: &#34;hello-world&#34;, callback: (payload) =&gt; { console.log(&#34;hello-world: &#34; &#43; JSON.stringify(payload)); } }]` |

### `terminateIntance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成して再度有効にしてください。

`Tealium.terminateIntance();`

### `track()`

`TealiumEvent`または`TealiumView`ディスパッチでイベントを追跡します。

`Tealium.track(dispatch);`

| パラメータ | タイプ      | 説明      | 
|:-----------|:----------|:-----------------|
| `tealEvent` | [`TealiumDispatch`](#tealiumdispatch) | イベント名とデータレイヤーを含むTealiumディスパッチ | 

```javascript
let tealEvent = new TealiumEvent(
    &#39;cart_add&#39;, 
    {
        &#34;customer_id&#34;: &#34;abc123&#34;, 
        &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
        &#34;product_price&#34;: [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```
### 訪問プロファイル

訪問プロファイルは、各属性に対して親しみやすい名前が含まれているオブジェクトです。`currentVisit`プロパティを使用して、訪問/訪問属性のタイプを区別できます。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合は、`null`が返されます。以下のリストを参照してください。

**属性タイプ**

| パラメータ           | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                     | `id: &#34;5129&#34;, value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                      | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                      | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: &#34;tealiummobile\_demo\_103&#34;, value: &#34;iOS Users&#34;`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                       | `id: &#34;2815&#34;, value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                       | `id: &#34;4868&#34;, value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])` |
| `dates`            | id: String, value: Number                                                                                        | `id: &#34;22&#34;, value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                        | `id: &#34;5728&#34;, value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set(String)                                                                                   | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                        | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Number                                                                                        | `[&#34;category 1&#34;: 2.0]`                                                                                                             |

### リモートコマンド

リモートコマンドを定義するインターフェース

| 値          | 説明                                                      |
|:-----------|:---------------------------------------------------------|
| `id`       | リモートコマンドの一意の識別名                            |
| `path`     | (オプション) マッピングに使用するローカルファイル         |
| `url`      | (オプション) マッピングに使用するリモートファイル         |
| `callback` | (オプション) リモートコマンドのコールバック関数           |

パスとURLはオプションですが、どちらか一方のみを提供するか、Tealium iQタグ管理でタグによってマッピングが処理される場合は両方を省略します。

コマンドがReact Nativeアプリの範囲内で処理される場合は、コールバックを提供します。ハンドラが既にネイティブに登録されている場合は、コールバックを省略します。

以下は、Javascriptで処理されるコマンドのローカルマッピングファイルの例です：
```javascript
let localCommand: RemoteCommand = {
    id: &#34;hello-world&#34;,
    path: &#34;hello-mappings.json&#34;,
    callback: (payload) =&gt; {
        //...
    }
}
```

以下は、ネイティブで処理されるコマンドのリモートマッピングファイルの例です：
```javascript
let remoteNativeCommand: RemoteCommand = {
    id: &#34;hello-world&#34;,
    url: &#34;https://you.domain.com/hello-mappings.json&#34;
}
```

## インターフェース: `TealiumDispatch`

追跡するイベントのタイプを定義するインターフェース。以下のクラスが`TealiumDispatch`を実装しています：

### クラス: `TealiumEvent`

ユーザーの画面とのやり取りを追跡するには、`TealiumEvent(tealiumEvent, dataLayer)`のインスタンスを[`track()`](#track)メソッドに渡します。`TealiumEvent`は、追跡コールに`tealium_event`として表示されるイベント名と、オプションのイベントデータオブジェクトで構成されます。

```javascript
let tealEvent = TealiumEvent(tealiumEvent, {eventData})
tealium?.track(tealEvent)
```

| パラメータ      | タイプ    | 説明      |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event`として渡されるイベント名  |
| `eventData` | `object` | (オプション) イベントに送信されるキー値形式のデータ。 | 

例：

```javascript
let tealEvent = new TealiumEvent(
    &#39;cart_add&#39;, 
    {
        &#34;customer_id&#34;: &#34;abc123&#34;, 
        &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
        &#34;product_price&#34;: [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```

### クラス: `TealiumView`

画面ビューを追跡するには、`TealiumView(tealiumEvent, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumView`は、追跡コールに`tealium_event`として表示されるビュー名と、オプションのデータ辞書で構成されます。

```swift
let screenView = TealiumView(tealiumEvent, {eventData})
tealium?.track(screenView)
```

| パラメータ      | タイプ    | 説明      | 例    |
|:------------|:--------|:-----------------|:-----------|
| `tealiumEvent`  | `string`                     | ビューイベントまたは画面の`tealium_event`名。          | `purchase`                                                 |
| `eventData` | `Dictionary&lt;string, object&gt;` | オプション。イベントに送信されるキー値形式のデータ。 | `&#39;purchase&#39;, {&#34;customer_id&#34;, &#34;abc123&#34;, &#34;order_total&#34;: 10.00, &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], &#34;order_id&#34;: &#34;0123456789&#34;}` |

例：

```javascript
let screenView = new TealiumView(
    &#39;purchase&#39;, 
    {
        &#34;customer_id&#34;: &#34;abc123&#34;, 
        &#34;order_total&#34;: 10.00, 
        &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
        &#34;order_id&#34;: &#34;0123456789&#34;
    }
);
Tealium.track(screenView);
```

