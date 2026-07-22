---
title: Firebase リモートコマンド注文イベントの例
description: TealiumのFirebase用リモートコマンド統合について学ぶ
url: https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-order-event-example/
---
### インストール

[詳細を見る](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/) AndroidとSwift/iOSでのTealiumのFirebase用リモートコマンド統合について

### タグ構成

カスタムコマンドタグは、Tealiumモバイルライブラリに登録したカスタムネイティブコードブロックをトリガーするために必要なAPIの実装を含む特別なタグです。

[詳細を見る](https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-tag/) Tealium iQタグ管理アカウントでFirebaseモバイルリモートコマンドタグを構成する方法について。

アプリからのトラッキングコールを介して送信されるデータを更新するために拡張機能が必要になる場合があります。例えば、「注文確認」画面でTealium SDKを使用して画面ビューをトラッキングしている場合、Firebase SDKでこれをログに記録することも望まれるかもしれません。

以下は、iOS（Swift）でTealiumのトラッキングコールの例です：

```
tealium?.trackView("order_confirmation", ["order_id":"A123456",
"user_id": "john.doe@someprovider.com", "user_loyalty_status":"vip", "travel_class" : "first"])
```

Firebase SDKでは、`logEvent` APIコールを使用してこのイベントをログに記録し、`user_id`というユーザープロパティを構成することが望まれます。Tealium iQでは、これはいくつかの異なる方法で行われます。

`command_name`変数の値は、実行するコマンドのコンマ区切りの文字列に構成されます。含まれる可能性のある5つの値は以下の通りです：

* `config`
* `setUserId`
* `setScreenName`
* `setUserProperty`
* `logEvent`.

この例では、Tealium iQでの操作の順序を理解することが重要です。同じ「スコープ」の拡張機能は、Extensionsタブで見ることができるように、上から下への順序で実行されることが保証されています。したがって、ロジックは異なる拡張機能に簡単に分割されますが、以前の拡張機能で定義された変数に書き込みを続けます。

1. Tealium iQプロファイルで`firebase_command_name`という新しいデータレイヤー変数を作成します。

1. **Set Data Values**拡張機能を作成し、ドロップダウンリストから新しい変数`firebase_command_name`を選択し、データ入力フィールドを空白のままにします。これにより、変数が空の文字列で初期化されます。

1. 以下にリストされている構成で**Set Data Values**拡張機能のリストを作成します：

#### config

セッションごとにこの構成を一度だけ実行します。以下はTealium iQの構成変数のリストです：

|TiQ変数名| タイプ| 例| 備考|
|---| ---| ---| ---|
|`command_name`| テキスト| `config`| 必須、大文字小文字を区別|
|`firebase_minimum_session_length`| テキスト| `10`| 任意|
|`firebase_session_timeout`| テキスト| `3600`| 任意|
|`firebase_analytics_enabled`| テキスト| `true`| 任意、大文字小文字を区別、デフォルト = true|
|`firebase_log_level`| テキスト| `error`| 任意、大文字小文字を区別|

これにより、ネイティブFirebase APIで以下のコールが生成されます：

Android：

```
mFirebaseAnalytics = FirebaseAnalytics.getInstance(mCurrentActivity.getApplicationContext());
mFirebaseAnalytics.setSessionTimeoutDuration(3600);
mFirebaseAnalytics.setMinimumSessionDuration(10);
mFirebaseAnalytics.setAnalyticsCollectionEnabled(true);
```

Swift：

```
let firConfig = FirebaseConfiguration.shared
let firAnalyticsConfig = AnalyticsConfiguration.shared()
firAnalyticsConfig.setSessionTimeoutInterval(3600)
firAnalyticsConfig.setMinimumSessionInterval(10)
firAnalyticsConfig.setAnalyticsCollectionEnabled(true)
firAnalyticsConfig.setLoggerLevel(FirebaseLoggerLevel.error)
firConfig.analyticsConfiguration = firAnalyticsConfig
FirebaseApp.configure()
```

#### setUserId

以下のユーザーID変数が利用可能です：

|TiQ変数名| タイプ| 例| 備考|
|---| ---| ---| ---|
|`firebase_command_name`| JSコード| `b.firebase_command_name + ",setUserId"`| 大文字小文字を区別、コンマ区切り、スペースなし|
|`firebase_user_id`| テキスト| `john.doe@someprovider.com`| （必須）有効な文字列|

これにより、ネイティブFirebase APIで以下のコールが生成されます：

Android：

```
FirebaseAnalytics.setUserId("john.doe@someprovider.com");
```

Swift：

```
Analytics.setUserID("john.doe@someprovider.com")
```

#### setScreenName

以下の画面名変数が利用可能です：

|TiQ変数名| タイプ| 例| 備考|
|---| ---| ---| ---|
|`firebase_command_name`| JSコード| `b.firebase_command_name + ",setScreenName"`| 大文字小文字を区別、コンマ区切り、スペースなし|
|`firebase_screen_name`| テキスト| `Order Confirmation`| （必須）有効な文字列|
|`firebase_screen_class`| テキスト| `Order`| （任意）有効な文字列|

これにより、ネイティブFirebase APIで以下のコールが生成されます：

Android：

```
FirebaseAnalytics.setCurrentScreen(<current activity reference>, "Order Confirmation", "Order");
```

Swift：

```
Analytics.setScreenName("Order Confirmation", screenClass: "Order")
```

#### setUserProperty

以下のユーザープロパティ変数が利用可能です：

|TiQ変数名| タイプ| 例| 備考|
|---| ---| ---| ---|
|`firebase_command_name`| JSコード| `b.firebase_command_name + ",setUserProperty"`| 大文字小文字を区別、コンマ区切り、スペースなし|
|`firebase_property_name`| テキスト| `user_loyalty_status`| （必須）有効な文字列|
|`firebase_property_value`| テキスト| `vip`| （必須）有効な文字列。以前に構成された値をクリアするには空の文字列に構成します。|

これにより、ネイティブFirebase APIで以下のコールが生成されます：

Android：

```
FirebaseAnalytics.setUserProperty("user_loyalty_status", "vip");
```

Swift：

```
Analytics.setUserProperty("vip", forName: "user_loyalty_status")
```

#### logEvent

以下のログイベント変数が利用可能です：

|TiQ変数名| 変数| 例| 備考|
|---| ---| ---| ---|
|`firebase_command_name`| JSコード| `b.firebase_command_name + ",logEvent"`| 大文字小文字を区別、コンマ区切り、スペースなし|
|`firebase_event_name`| テキスト| `event_ecommerce_purchase`| （必須）有効な文字列。最適な結果を得るために、上記で推奨されているイベントタイプのいずれかを使用します。|
|`firebase_event_params`| JSコード| `{"param_travel_class" : b.travel_class, "param_transaction_id": b.order_id};`| （任意）有効なJSONオブジェクト。最適な結果を得るために、上記で推奨されているデフォルトパラメータのいずれかを使用します。カスタムパラメータはFirebaseコンソールで定義される必要があります。|

これにより、ネイティブFirebase APIで以下のコールが生成されます：

Android：

```
Bundle b = new Bundle();
b.putString("param_travel_class", "first");
b.putString("param_transaction_id", "A123456")

FirebaseAnalytics.logEvent(FirebaseAnalytics.Event.ECOMMERCE_PURCHASE, b);
```

Swift：

```
Analytics.logEvent(AnalyticsEventEcommercePurchase, parameters: [AnalyticsParameterTravelClass: "first", AnalyticsParameterTransactionID: "A123456"])
```
