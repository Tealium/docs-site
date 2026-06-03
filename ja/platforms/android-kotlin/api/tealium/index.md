---
title: Tealium
description: Tealiumクラスとメソッドに関する参照ガイド（Android用Kotlin）
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/
---
## クラス: `Tealium`

`Tealium` クラスは、画面表示とイベントの追跡用のメソッドを提供します。以下のドキュメントでは、Kotlin用の `Tealium` クラスの一般的に使用されるメソッドとプロパティをまとめています。個々のモジュールも、有効になっている場合は `Tealium` クラスの独自の拡張を提供することがあります。

| メソッド/プロパティ                                           | 説明                                                                                       |
|:----------------------------------------------------------|:--------------------------------------------------------------------------------------------------|
| [`cancelTimedEvent()`](#canceltimedevent)                 | タイムドイベントのタイマーをキャンセルします。                                                              |
| [`consentManager`](#consentmanager)                       | ユーザーの同意構成を管理するConsent Managerにアクセスします。                       |
| [`dataLayer`](#datalayer)                                 | デバイス上の永続的な保存へのアクセス - データレイヤー内のアイテムは各イベントに追加されます。 |
| [`endTraceVisitorSession()`](#endtracevisitorsession)     | リモートで訪問セッションを終了し、セッション終了イベントをテストします。                                  |
| [`events`](#events)                                       | Tealium SDK全体で多くのイベントに対してリスナークラスを提供します。           |
| [`gatherTrackData()`](#gathertrackdata)                   | データレイヤーとコレクターからすべてのトラックデータを公開します。                                             |
| [`joinTrace()`](#jointrace)                               | 現在のセッションのデータレイヤーに提供されたトレースIDを追加します。                             |
| [`leaveTrace()`](#leavetrace)                             | トレースIDを削除してトレースを離脱します。                                                        |
| [`linkEcidToKnownIdentifier`](#linkecidtoknownidentifier) | 現在のECIDを既知のセカンダリIDにリンクします。                                                   |
| [`modules`](#modules)                                     | システム内のモジュールにアクセスを提供します。                                                 |
| [`resetVisitor()`](#resetvisitor)                         | 次のトラッキングコールで新しいものを取得することにより、訪問のECIDをリセットします。                        |
| [`sendQueuedDispatches()`](#sendqueueddispatches)         | すべてのDispatchValidatorsを再評価するように要求します。                                             |
| [`session`](#session)                                     | 現在のセッションに関連する情報を提供します。                                             |
| [`startTimedEvent()`](#starttimedevent)                   | 指定された名前でタイムドイベントを開始します。                                                         |
| [`stopTimedEvent()`](#stoptimedevent)                     | タイムドイベントのタイマーを停止し、`timed_event` トラッキングコールをトリガーします。                 |
| [`Tealium`](#tealium)                                     | `Tealium` インスタンスを作成するコンストラクターメソッド。                                             |
| [`track()`](#track)                                       | 画面表示またはイベントを追跡するためのメソッド。                                                  |
| [`visitor`](#visitor)                                     | 完全な `AdobeVisitor` インスタンスを返します。                                                         |
| [`visitorId`](#visitorid)                                 | データレイヤーに保存されている現在の訪問ID。                                          |


### `cancelTimedEvent()`

以前に開始されたタイムドイベントをキャンセルします。タイムドイベントは追跡されません。

```java
tealium.cancelTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| パラメータ | タイプ     | 説明                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | タイムドイベントの名前 |

### `consentManager`

現在の同意ステータスとカテゴリを構成し、現在施行されているポリシーを確認することができます。[同意管理](/ja/platforms/android-kotlin/consent-management/)ガイドで詳細を学びましょう。

```java
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED
```

### `dataLayer`

キーバリューペアのためのデバイス上の永続的な保存を提供し、有効期限の構成も可能です。各エントリは、[`track()`](#track) メソッドを通じて送信するすべてのディスパッチにも追加されます。[データ管理](/ja/platforms/android-kotlin/data-layer/)ガイドで詳細を学びましょう。

```java
tealium.dataLayer.putString(&#34;key&#34;, &#34;value&#34;, Expiry.FOREVER)
```

### `endTraceVisitorSession()`

リモートで訪問セッションを終了します。SDKセッションを終了させたり、セッションIDをリセットしたりすることはありません。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.endTraceVisitorSession()
```

### `events`

`Tealium`インスタンスにリスナークラスを提供して、SDKからの有用な情報を受け取ります。

以下の例では、任意の同意構成変更に対するリスナーを登録します。このリスナーは、新しい同意構成と現在施行されているポリシーを提供されます。
`com.tealium.core.messaging`で利用可能な追加のリスナーがあります。

```java
tealium.events.subscribe(object: UserConsentPreferencesUpdatedListener {
    override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences, policy: ConsentManagementPolicy) {
        // 同意変更に対するアクションを取る
    }
})
```

### `gatherTrackData()`

データレイヤーとコレクターからトラックデータを取得します。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.gatherTrackData()
```

### `joinTrace()`

現在のセッションのデータレイヤーに提供されたトレースIDを追加します。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.joinTrace(traceId)
```

| パラメータ | タイプ     | 説明 |
|:-----------|:---------|:------------|
| `traceId`  | `String` | トレースID    |


### `leaveTrace()`

トレースIDを削除してトレースを離脱します。

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.leaveTrace()
```

### `linkEcidToKnownIdentifier()`

現在のECIDを既知のセカンダリ識別子（例えば、メールアドレスや他の内部IDなど）にリンクします。

```java
linkEcidToKnownIdentifier(
  knownId: String,
  adobeDataProviderId: String,
  authState: Int?,
  adobeResponseListener: ResponseListener&lt;AdobeVisitor&gt;?
  )
```

| パラメータ              | タイプ                             | 説明                         |
|:------------------------|:---------------------------------|:------------------------------------|
| `knownId`               | `String`                         | 既知の識別子。               |
| `adobeDataProviderId`   | `String`                         | Adobeデータプロバイダー識別子。 |
| `authState`             | `Int`                            | 認証状態。            |
| `adobeResponseListener` | `ResponseListener&lt;AdobeVisitor&gt;` | Adobeレスポンスリスナー。        |


例:

```java
var tealium: Tealium?
...

tealium.adobeVisitorApi?.linkEcidToKnownIdentifier(
  &#34;myidentifier&#34;,
  &#34;123456&#34;,
  AdobeAuthState.AUTH_STATE_AUTHENTICATED,
  null
  )
```

### `modules`

SDKのモジュールマネージャーにアクセスを提供し、特定のモジュールへのアクセスを提供するために使用されます。

```java
tealium.modules.getModule(VisitorService::class.java)?.delegate = myDelegate
```

### `resetVisitor()`

次のトラッキングコールで新しいものを取得することにより、訪問のECIDをリセットします。

```java
resetVisitor()
```

例:

```java
var tealium: Tealium?
//...
tealium?.adobeVisitorApi?.resetVisitor()
```
### `sendQueuedDispatches()`

DispatchValidatorによってさまざまな理由でキューに入れられたディスパッチを、イベントバッチ処理の制限を無視して再評価するためにこのメソッドを使用できますが、他のDispatchValidatorには従います。例えば、接続がなく、依然として接続がない場合、キューに入れられたディスパッチはキューに残ります。

```java
tealium.sendQueuedDispatches()
```

### `session`

現在のセッションに関連するすべてのデータを含みます。

```java
val sessionId = tealium.session.id
```

### `startTimedEvent()`

指定された名前でタイムドイベントを開始します。同じイベント名でこのメソッドが再び呼び出された場合、イベントが終了またはキャンセルされていない限り無視されます。イベントの開始時間は保存されません。

イベント名とともにオプショナルデータが渡された場合、タイマーが[`stopTimedEvent()`](#stoptimedevent)呼び出しで停止されたときにトラックコールに追加されます。

```java
tealium.startTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;, mapOf(&#34;custom_value&#34; to &#34;custom_key&#34;))
```

| パラメータ                              | タイプ     | 説明                                                                 |
|:----------------------------------------|:---------|:----------------------------------------------------------------------------|
| `name`                                  | `String` | タイムドイベントの名前                                                 |
| `mapOf(&#34;custom_key&#34; to &#34;custom_value&#34;)` | `Map`    | (オプショナル) データレイヤーで追跡されるキー値ペアデータのオブジェクト |

### `stopTimedEvent()`

タイムドイベントのタイマーを停止し、`timed_event`トラッキングコールをトリガーします。

```java
tealium.stopTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| パラメータ | タイプ     | 説明                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | タイムドイベントの名前 |

### `Tealium`

`Tealium`インスタンスを作成するコンストラクターメソッド。

```java
val config = TealiumConfig(key, config);
```

| パラメータ | タイプ             | 説明                            | 例         |
|:-----------|:-----------------|:---------------------------------------|:----------------|
| `key`      | `String`         | 新しいTealiumインスタンスの名前              | `&#34;abc123&#34;`      |
| `config`   | `Tealium.Config` | 新しいインスタンスの構成 | `tealConfigObj` |

```java
// Assuming execution is within Application.onCreate()
val config = TealiumConfig(this, &#34;ACCOUNT_NAME&#34;, &#34;PROFILE_NAME&#34;, Environment.PROD)
val tealium = Tealium.create(&#34;main&#34;, config)
```

モジュールはバックグラウンドスレッドで初期化されるため、Tealiumオブジェクトの作成直後には準備が整っていない場合があります。インスタンスが準備でき次第、必要な追加構成を追加するために完了ブロックを追加します：

```java
val tealium = Tealium.create(&#34;main&#34;, config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev(&#34;--&#34;, &#34;VisitorProfile updated: $visitorProfile&#34;)
        }
    })
}
```

### `track()`

オプショナルイベントデータを含む画面表示またはイベントをトラックします。

```java
tealium.track(tealiumlEvent)
```

| パラメータ  | タイプ         | 説明       | 
|:------------|:-------------|:------------------|
| `tealiumlEvent`  | `TealiumView` or `TealiumEvent`     | イベント名とオプショナルイベントデータを含むディスパッチオブジェクト。   |

イベントをトラックするには、[`TealiumView`](#class-tealiumview)または[`TealiumEvent`](#class-tealiumevent)オブジェクトを`track()`メソッドに渡します：

```java
val tealiumlEvent = TealiumView(
  &#34;purchase&#34;, 
  mutableMapOf(
    &#34;customer_id&#34; to &#34;abc123&#34;, 
    &#34;order_total&#34; to 10.00, 
    &#34;product_id&#34; to listOf(&#34;PROD123&#34;, &#34;PROD456&#34;),
    &#34;order_id&#34; to &#34;0123456789&#34;
  )
)
tealium.track(tealiumlEvent);
```

### `visitor`

完全なAdobeVisitorインスタンスを返します。

```java
var tealium: Tealium?
//...
val visitor = tealium.adobeVisitorApi?.visitor?.let { visitor -&gt;
    val ecid = visitor.experienceCloudId
    val nextRefresh = visitor.nextRefresh
    val blob = visitor.blob
    val region = visitor.region
   

