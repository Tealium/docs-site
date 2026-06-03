---
title: Tealium
description: Tealiumクラスは、すべてのモジュールのための主要なAPIエントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/
---
## クラス: `Tealium`

以下は、iOS (Swift) の `Tealium` クラスで一般的に使用されるメソッドをまとめたものです。

| メソッド/プロパティ                                           | 説明                |
|:----------------------------------------------------------|:---------------------------|
| [`cancelTimedEvent()`](#canceltimedevent)                 | タイムドイベントのタイマーをキャンセルします。 |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids)       | visitorIdsの保存されたキャッシュを削除し、`resetVisitorId`を呼び出します。 |
| [`clearAllTimedEvents()`](#clearalltimedevents)           | 以前に開始されたすべてのタイムドイベントをクリアします。 |
| [`decorateUrl()`](#decorateurl)                           | URLをAdobe ECIDパラメータで装飾します。 |
| [`disable()`](#disable)                                   | Tealiumライブラリを無効にします。 |
| [`flushQueue()`](#flushqueue)                             | キューに入れられたディスパッチをすぐに送信します。 |
| [`gatherTrackData()`](#gathertrackdata)                   | すべてのカスタムデータレイヤー値とコレクターモジュールのデータレイヤー値を返します。 |
| [`getTagManagementWebView()`](#gettagmanagementwebview)   | TagManagement WebViewを返します。 |
| [`joinTrace()`](#jointrace)                               | 指定されたIDでトレースに参加します。 |
| [`leaveTrace()`](#leavetrace)                             | 以前に参加したトレースを離れ、訪問セッションを終了します。 |
| [`linkECIDToKnownIdentifier`](#linkecidtoknownidentifier) | 現在のECIDを既知のセカンダリIDにリンクします。 |
| [`onVisitorId`](#onvisitorid)                             | `visitorId`の変更を購読することができます。 |
| [`resetVisitor()`](#resetvisitor)                         | 次のトラッキングコールで新しいものを取得することにより、訪問のECIDをリセットします。 |
| [`resetVisitorId()`](#resetvisitorid)                     | ユーザーの新しい訪問IDを生成します。 |
| [`startTimedEvent()`](#starttimedevent)                   | 指定された名前でタイムドイベントを開始します。 |
| [`stopTimedEvent()`](#stoptimedevent)                     | タイムドイベントのタイマーを停止し、`timed_event`トラッキングコールをトリガーします。 |
| [`Tealium()`](#tealium)                                   | 新しい`Tealium`オブジェクトのコンストラクター。 |
| [`track()`](#track)                                       | 関連データを持つイベントをトラッキングし、オプションでコールバック関数をトリガーします。 |
| [`visitor`](#visitor)                                     | 完全な`AdobeVisitor`インスタンスを返します。 |
| [`visitorId`](#visitorid)                                 | ランダムに生成され、一意の永続的な訪問IDを返します。 |

### `cancelTimedEvent()`

タイムドイベントのタイマーをキャンセルします。タイムドイベントは追跡されません。

```swift
tealium?.cancelTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| パラメータ | タイプ     | 説明                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | タイムドイベントの名前 |

### `clearAllTimedEvents()`

以前に開始されたすべてのタイムドイベントをクリアします。タイムドイベントは追跡されません。

```swift
tealium?.clearAllTimedEvents()
```

### `clearStoredVisitorIds()`

以前に保存された訪問IDとハッシュ化された顧客識別子をすべてクリアします。

```swift
tealium?.clearStoredVisitorIds()
```

### `decorateUrl()`

入力されたURLをAdobe ECIDクエリパラメータで装飾します。

```swift
decorateUrl(_ url: URL, completion: ((URL) → Void)
```

| パラメータ            | タイプ                          | 説明                    |
|:----------------------|:------------------------------|:-------------------------------|
| `url`                 | `URL`                         | 装飾するURL            |
| `completion`          | `URL` -&gt; Void                 | 装飾されたURLで呼び出されるブロック。 |

例:

```swift
var tealium: Tealium?
...
let url = URL(string: &#34;https://www.tealium.com&#34;)!
tealium?.adobeVisitorApi?.decorateUrl(url) { newUrl in
    // 新しいURLを使用
}
```

### `disable()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成して再度有効にします。

```swift
tealium?.disable()
```

### `flushQueue()`

キューに入れられたすべてのディスパッチをすぐに送信します。リクエストは`DispatchValidator`（例：Consent Manager）によってブロックされる可能性があります。

```swift
tealium?.disable()
```

### `gatherTrackData()`

現在のカスタムデータレイヤー値とコレクターモジュールのデータレイヤー値を取得します。結果は後続の呼び出しのためにキャッシュされ、非同期で返されます。最新の値を取得するには`retrieveCachedData`を`false`に構成します。返された値を処理するためにコンプリーションハンドラを使用します。カスタムデータレイヤー値は直接カスタムキーを使用して参照し、コレクターモジュール値は`TealiumDataKey.`を使用して参照します。  

```swift
 tealium?.gatherTrackData(retreiveCachedData: false, completion: { allData in
    let lifecycleTotalWakeCount = allData[TealiumDataKey.totalWakeCount]
    let visitorId = allData[TealiumDataKey.visitorId]
    let userLanguage = allData[&#34;user_language&#34;]
})
```

参照：[`Tealium.dataLayer.all`](/ja/platforms/ios-swift/data-layer/#retrieve-all-data).

### `getTagManagementWebView()`
([v2.10.0](/ja/platforms/ios-swift/release-notes/#2100-may-2023)で新規)

TagManagement WebViewを返し、クライアントが`isInspectable`フラグを構成し、XCode 14.3&#43;でデバッグできるようにします。

プライベートWebviewオブジェクトの他の使用、例えば別のウェブページをロードすることは、予測不可能な挙動を引き起こす可能性があり、強く非推奨です。

```swift
 tealium?.getTagManagementWebView { webView in
    if #available(iOS 16.4, *) {
        webView.isInspectable = true // XCode 14.3&#43;およびiOS 16.4&#43;でtagManagement webviewsを検査するため
    }
  }
```

### `joinTrace()`

指定されたIDでトレースに参加します。トレースはアプリセッションの間、`leaveTrace()`が呼ばれるまでアクティブのままです。Tealium Customer Data Hubの[トレース機能]()についてもっと学びましょう。

```swift
joinTrace(traceId: String)
```

| パラメータ | タイプ     | 説明                               | 例   |
|:-----------|:---------|:------------------------------------------|:----------|
| `traceId`  | `String` | Traceツールから取得したトレースID | `&#34;12345&#34;` |


### `leaveTrace()`

以前に参加したトレースを離れ、訪問セッションを終了します。トレースを離れる際にトレース訪問セッションを保持するオプションパラメータ。

```swift
tealium?.leaveTrace(killVisitorSession: false)
```

| パラメータ           | タイプ   | 説明                                                                                                               | 例 |
|:---------------------|:-------|:--------------------------------------------------------------------------------------------------------------------------|:--|
| `killVisitorSession` | `Bool` | (オプション) パラメータが渡されない場合は`true`に構成します。訪問セッションを終了したくない場合は`false`に構成します。デフォルトは`true`です。 | `false` |
### `linkECIDToKnownIdentifier()`

現在のECIDを既知のセカンダリ識別子（例えば、メールアドレスや他の内部IDなど）にリンクします。

```swift
linkECIDToKnownIdentifier(
  _ knownID: String,
  adobeDataProviderId: String,
  authState: AdobeVisitorAuthState?,
  completion: ((Result&lt;AdobeVisitor, Error&gt;) → Void)
```

| パラメーター              | 型                            | 説明                          |
|:----------------------|:------------------------------|:-------------------------------|
| `knownId`             | `String`                      | 既知の識別子。                  |
| `adobeDataProviderId` | `String`                      | Adobeデータプロバイダー識別子。 |
| `authState`           | `AdobeVisitorAuthState`       | 認証状態。                     |
| `completion`          | `Result&lt;AdobeVisitor, Error&gt;` | Adobeの応答リスナー。           |

例:

```swift
var tealium: Tealium?
...

tealium?.adobeVisitorApi?.linkECIDToKnownIdentifier(
  &#34;myidentifier&#34;, adobeDataProviderId: &#34;123456&#34;, .unknown
  )
```

### `onVisitorId`

訪問IDの変更を通知します。

```swift
let subscription = tealium?.onVisitorId.subscribe { newVisitor in
    // ここで訪問の変更を処理します
}
```

### `resetVisitor()`

次のトラッキングコールで新しいECIDを取得することにより、訪問のECIDをリセットします。

```swift
resetVisitor()
```

例:

```swift
var tealium: Tealium?
//...
tealium?.adobeVisitorApi?.resetVisitor()
```

### `resetVisitorId()`

ユーザーの新しい訪問IDを生成します。

```swift
tealium?.resetVisitorId()
```

### `startTimedEvent()`

指定された名前でタイムドイベントを開始します。同じイベント名でこのメソッドが再び呼び出された場合、イベントが終了またはキャンセルされていない限り無視されます。イベントの開始時間は保存されません。

イベント名と共にオプショナルデータが渡された場合、タイマーが[`stopTimedEvent()`](#stoptimedevent)コールで停止されたときにトラックコールに追加されます。

```swift
tealium.startTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;, with: [&#34;custom_key&#34;: &#34;custom_value&#34;])
```

| パラメーター                                  | 型     | 説明                   |
|:--------------------------------------------|:---------|:------------------------------|
| `name`                                      | `String` | タイムドイベントの名前   |
| `[&#34;custom_key&#34;: &#34;custom_value&#34;]` (オプショナル) | `Map`    | データレイヤーで追跡されるキー値ペアデータのオブジェクト |

### `stopTimedEvent()`

タイムドイベントのタイマーを停止し、`timed_event`トラッキングコールをトリガーします。

```swift
tealium?.stopTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| パラメーター | 型     | 説明                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | タイムドイベントの名前 |

### `Tealium()`
新しい`Tealium`オブジェクトのコンストラクタ。

```swift
Tealium(config: TealiumConfig, completion: Closure)
```

| パラメーター   | 型            | 説明                                           |
|:-------------|:----------------|:------------------------------------------------------|
| `config`     | `TealiumConfig` | アカウントの詳細を含む`TealiumConfig`オブジェクトでTealiumオブジェクトを初期化します。 |
| `completion` | `Closure`       | (オプショナル) 初期化完了時に呼び出される完了クロージャ`()-&gt; Void )?` |

### `track()`

オプショナルイベントデータを持つスクリーンビューまたはイベントをトラッキングします。

```swift
tealium?.track(tealiumEvent)
```

| パラメーター | 型  | 説明 | 
|:-----------|:------|:------------|
| `tealiumEvent` | `TealiumView` または `TealiumEvent` | イベント名とオプショナルイベントデータを持つディスパッチオブジェクト。 |

イベントをトラッキングするには、[`TealiumView`](#class-tealiumview) または [`TealiumEvent`](#class-tealiumevent) オブジェクトを `track()` メソッドに渡します：

```swift
let tealiumEvent = TealiumView(
  &#34;purchase&#34;,
  dataLayer: [
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;order_total&#34;: 10.00,
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;order_id&#34;: &#34;0123456789&#34;
  ]
)
tealium?.track(tealiumEvent)
```

### `visitor`

完全なAdobeVisitorインスタンスを返します。

```swift
var tealium: Tealium?
//...
let visitor = tealium?.adobeVisitorApi?.visitor
let id: String? = visitor?.experienceCloudId
let nextRefresh: Date? = visitor?.nextRefresh
let blob: String? = visitor?.blob
let region: String? = visitor?.dcsRegion
let ttl: String? = visitor?.idSyncTTL
```

### `visitorId`

ランダムに生成された一意の永続的な訪問IDを返します。

```swift
let visitorId: String? = tealium.visitorId
```

