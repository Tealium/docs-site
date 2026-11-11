---
title: Firebase リモートコマンドのコマンド実行順序イベントの例
url: https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-order-event-example/
---### インストール

AndroidおよびSwift/iOS向けFirebaseのTealiumリモートコマンド連携について、[詳細はこちら](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/)を参照してください。

### タグの構成

カスタムコマンドタグは、Tealiumモバイルライブラリに登録したカスタムネイティブコードブロックを実行するために必要なAPIの実装を含む特別なタグです。

タグ管理アカウントでFirebase Mobile Remote Commandタグを構成する方法について、[詳細はこちら](https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-tag/)を参照してください。

トラッキングコールを介してアプリから送信されるデータを更新するために、拡張機能が必要になる場合があります。たとえば、Tealium SDKを使用して「Order Confirmation」画面のスクリーンビューをトラッキングし、それをFirebase SDKにも記録する場合などです。

以下は、iOS（Swift）向けTealiumにおけるトラッキングコールの例です。

```
`tealium?.trackView("order_confirmation", ["order_id":"A123456",
"user_id": "john.doe@someprovider.com", "user_loyalty_status":"vip", "travel_class" : "first"])
`
```

Firebase SDKでは、`logEvent` APIコールを使用してこれをイベントとして記録し、さらに`user_id`というユーザープロパティを構成できます。タグ管理では、これを複数の方法で実行できます。

`command_name`変数の値には、実行するコマンドをカンマ区切りの文字列として構成します。指定できる値は次の5つです。

* `config`
* `setUserId`
* `setScreenName`
* `setUserProperty`
* `logEvent`

この例では、タグ管理における処理の実行順序を理解することが重要です。同じ「スコープ」を持つ拡張機能は、［拡張機能］タブに表示される順序どおりに、上から下へ実行されることが保証されています。そのため、ロジックを複数の拡張機能に簡単に分割できますが、前の拡張機能で定義された変数への書き込みを継続する必要があります。

1. タグ管理プロファイルに、`firebase_command_name`という新しいデータレイヤー変数を作成します。

1. **データ値を構成**拡張機能を作成し、ドロップダウンリストから新しい変数`firebase_command_name`を選択して、データ入力フィールドは空白のままにします。これにより、変数が空の文字列で初期化されます。

1. 以下の表に示す構成を使用して、次の**データ値を構成**拡張機能を作成します。

#### config

この構成は、セッションごとに1回だけ実行します。タグ管理の構成変数は次のとおりです。

|TiQ変数名|型|例|注記|
|---|---|---|---|
|`command_name`|テキスト|`config`|必須、大文字と小文字を区別|
|`firebase_minimum_session_length`|テキスト|`10`|任意|
|`firebase_session_timeout`|テキスト|`3600`|任意|
|`firebase_analytics_enabled`|テキスト|`true`|任意、大文字と小文字を区別、デフォルト = true|
|`firebase_log_level`|テキスト|`error`|任意、大文字と小文字を区別|

これにより、ネイティブFirebase APIで次の呼び出しが生成されます。

Android：

```
`mFirebaseAnalytics = FirebaseAnalytics.getInstance(mCurrentActivity.getApplicationContext());
mFirebaseAnalytics.setSessionTimeoutDuration(3600);
mFirebaseAnalytics.setMinimumSessionDuration(10);
mFirebaseAnalytics.setAnalyticsCollectionEnabled(true);
`
```

Swift：

```
`let firConfig = FirebaseConfiguration.shared
let firAnalyticsConfig = AnalyticsConfiguration.shared()
firAnalyticsConfig.setSessionTimeoutInterval(3600)
firAnalyticsConfig.setMinimumSessionInterval(10)
firAnalyticsConfig.setAnalyticsCollectionEnabled(true)
firAnalyticsConfig.setLoggerLevel(FirebaseLoggerLevel.error)
firConfig.analyticsConfiguration = firAnalyticsConfig
FirebaseApp.configure()`
```

#### setUserId

次のユーザーID変数を使用できます。

|TiQ変数名|型|例|注記|
|---|---|---|---|
|`firebase_command_name`|JSコード|`b.firebase\_command\_name + ",setUserId"`|大文字と小文字を区別、カンマ区切り、スペースなし|
|`firebase_user_id`|テキスト|`john.doe@someprovider.com`|（必須）任意の有効な文字列|

これにより、ネイティブFirebase APIで次の呼び出しが生成されます。

Android：

```
`FirebaseAnalytics.setUserId("john.doe@someprovider.com");
`
```

Swift：

```
`Analytics.setUserID("john.doe@someprovider.com")
`
```

#### setScreenName

次の画面名変数を使用できます。

|TiQ変数名|型|例|注記|
|---|---|---|---|
|`firebase_command_name`|JSコード|`b.firebase_command_name + ",setScreenName"`|大文字と小文字を区別、カンマ区切り、スペースなし|
|`firebase_screen_name`|テキスト|`Order Confirmation`|（必須）任意の有効な文字列|
|`firebase_screen_class`|テキスト|`Order`|（任意）任意の有効な文字列|

これにより、ネイティブFirebase APIで次の呼び出しが生成されます。

Android：

```
`FirebaseAnalytics.setCurrentScreen(&lt;current activity reference&gt;, "Order Confirmation", "Order");
`
```

Swift：

```
`Analytics.setScreenName("Order Confirmation", screenClass: "Order)
`
```

#### setUserProperty

次のユーザープロパティ変数を使用できます。

|TiQ変数名|型|例|注記|
|---|---|---|---|
|`firebase_command_name`|JSコード|`b.firebase_command_name + ",setUserProperty"`|大文字と小文字を区別、カンマ区切り、スペースなし|
|`firebase_property_name`|テキスト|`user_loyalty_status`|（必須）任意の有効な文字列|
|`firebase_property_value`|テキスト|`vip`|（必須）任意の有効な文字列。以前に構成した値を消去するには、空の文字列に構成します。|

これにより、ネイティブFirebase APIで次の呼び出しが生成されます。

Android：

```
`FirebaseAnalytics.setUserProperty("user_loyalty_status", "vip");
`
```

Swift：

```
`Analytics.setUserProperty("vip", forName: "user_loyalty_status")
`
```

#### logEvent

次のイベント記録用変数を使用できます。

|TiQ変数名|変数|例|注記|
|---|---|---|---|
|`firebase_command_name`|JSコード|`b.firebase_command_name + ",logEvent"`|大文字と小文字を区別、カンマ区切り、スペースなし|
|`firebase_event_name`|テキスト|`event_ecommerce_purchase`|（必須）任意の有効な文字列。最適な結果を得るには、上記の推奨イベントタイプのいずれかを使用してください。|
|`firebase_event_params`|JSコード|`{"param_travel_class" : b.travel_class, "param_transaction_id": b.order_id};`|（任意）任意の有効なJSONオブジェクト。最適な結果を得るには、上記の推奨デフォルトパラメータのいずれかを使用してください。カスタムパラメータをレポートに表示するには、事前にFirebaseコンソールで定義する必要があります。|

これにより、ネイティブFirebase APIで次の呼び出しが生成されます。

Android：

```
`Bundle b = new Bundle();
b.putString("param_travel_class", "first");
b.putString("param_transaction_id", "A123456")

FirebaseAnalytics.logEvent(FirebaseAnalytics.Event.ECOMMERCE_PURCHASE, b);
`
```

Swift：

```
`Analytics.logEvent(AnalyticsEventEcommercePurchase, parameters: [AnalyticsParameterTravelClass: "first", AnalyticsParameterTransactionID: "A123456"])`
```