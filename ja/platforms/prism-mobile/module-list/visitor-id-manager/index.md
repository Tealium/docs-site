---
title: Visitor ID Managerモジュール
description: Visitor ID Managerモジュールを使用して、モバイルアプリで匿名訪問IDを作成、保存、切り替えます。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/visitor-id-manager/
---
Visitor ID Managerモジュールは、デバイスの匿名訪問IDを管理するコレクターです。このモジュールは訪問IDを作成して保存し、すべてのトラッキングイベントに追加します。また、データレイヤー内のユーザーIDが変更されたときに、訪問IDを切り替えます。このモジュールはデフォルトで有効になっており、自動的に追加されるため、構成なしで動作します。

アプリで訪問IDを読み取って管理するには、`VisitorIdManager`を返す`tealium.visitorId`を使用します。

## 収集されるデータ

| データポイント | キー | 説明 |
| :--- | :--- | :--- |
| 訪問ID | `tealium_visitor_id` | デバイスの匿名訪問ID。 |

## 構成

| 構成 | JSONキー | 説明 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| 訪問IDキー | `visitor_identity_key` | メールアドレスやユーザーIDなど、現在のユーザーのIDを保持するデータレイヤーキー。このキーを構成すると、[訪問の切り替え](#visitor-switching)が有効になります。 | なし（訪問の切り替えは無効） |

このモジュールは、共通の`enabled`、`order`、`rules`モジュール構成もサポートしています。ルールの詳細については、[ルール](https://docs.tealium.com/rules/)を参照してください。

JSON構成ファイル、プログラム、またはその両方を使用してモジュールを構成します。

### JSON構成

ローカル構成ファイルを使用するには、`TealiumConfig`の`settingsFile`にファイル名を渡します。リモート構成を使用するには、`settingsUrl`にURLを渡します。両方を使用する場合、SDKによって構成がマージされ、リモート構成が優先されます。

```json
{
    "modules": {
        "VisitorId": {
            "module_type": "VisitorId",
            "enabled": true,
            "order": 1,
            "rules": {
                "operator": "and",
                "children": [
                    "rule_id_from_settings"
                ]
            },
            "configuration": {
                "visitor_identity_key": "email"
            }
        }
    }
}
```

### プログラムによる構成

SDKは、デフォルト構成でモジュールを追加します。モジュールの順序を変更する、構成を強制適用する、またはローカル構成やリモート構成に含まれている場合にのみモジュールを初期化するには、`TealiumConfig`の`modules`リストにモジュールを追加します。


<blockquote>
プログラムによる構成は、常にローカル構成およびリモート構成より優先されます。リモートで変更されてはならない値のみを強制適用してください。
</blockquote>


構成を強制適用するには、ビルダークロージャを渡します。



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.visitorId { builder ->
        builder.setVisitorIdentityKey("email")
    })
).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [
                               Modules.visitorId(forcingSettings: { builder in
                                   builder.setVisitorIdentityKey("email")
                               }),
                               // other modules...
                           ])
```



ローカル構成またはリモート構成にモジュールが含まれている場合にのみ初期化するには、次のようにします。



```kotlin
listOf(Modules.visitorId { null })
```


```swift
modules: [
    Modules.visitorId(forcingSettings: nil),
    // other modules...
]
```



### モジュールの無効化

モジュールを無効にするには、構成で`enabled`を`false`に構成するか、ビルダーで`setEnabled(false)`を呼び出します。モジュールが無効になっている間は、次のように動作します。

* トラッキングイベントに`tealium_visitor_id`が含まれません。
* すべての`tealium.visitorId`メソッドが失敗を返します。
* 訪問の切り替えが停止し、SDKはデータレイヤー内のIDの変更を無視します。
* Collectモジュールは引き続きイベントを送信し、訪問IDのないイベントをまとめてバッチ処理します。
* [Context APIモジュール](https://docs.tealium.com/platforms/prism-mobile/module-list/context-api/)は、エンジンのレスポンスを取得できません。

## 訪問の切り替え

訪問の切り替えでは、データレイヤーに書き込んだIDと訪問IDを関連付けるため、SDKは同じデバイス上でログインする同一人物を識別できます。SDKには、ログインまたはログアウトという概念はありません。SDKは、`visitor_identity_key`に構成されたデータレイヤーキーを監視します。

* 新しいIDを書き込んだときに、現在の訪問IDを所有する別のIDがない場合、SDKはそのIDを現在の訪問IDに関連付けます。
* 既知のIDを書き込むと、SDKは以前そのIDに関連付けられていた訪問IDを復元します。
* 別の未知のIDを書き込むと、SDKは新しい訪問IDを生成し、そのIDに関連付けます。
* キーを削除するか、キーの有効期限が切れた場合、訪問IDは変更されず、SDKはIDが存在しないものとしてマークします。

## 訪問IDの読み取り

訪問IDを一度だけ読み取るには、`current()`を呼び出します。現在の訪問IDと、その後のすべての変更を受け取るには、`tealium.visitorId`をサブスクライブします。SDKは、`regenerate()`、`eraseLocalHistory()`、または訪問の切り替え後に新しい値を発行します。



```kotlin
// Read the visitor ID once
tealium.visitorId.current().subscribe { result ->
    val visitorId = result.getOrNull()
}

// Receive the current visitor ID and every later change
val subscription = tealium.visitorId.subscribe { result ->
    val visitorId = result.getOrNull()
}
```


```swift
// Read the visitor ID once
tealium.visitorId.current().subscribe { result in
    // Handle the result
}

// Receive the current visitor ID and every later change
tealium.visitorId.subscribe { result in
    switch result {
    case .success(let visitorId):
        print("Visitor ID: \(visitorId)")
    case .failure(.tealiumError(let error)):
        // The Tealium instance failed to initialize or shut down. This is the last emission.
        print("Visitor ID no longer available: \(error)")
    case .failure(let error):
        // The module is disabled. Values resume if the module is enabled again.
        print("Failed to resolve visitor ID: \(error)")
    }
}.addTo(disposable)
```



モジュールが無効になっている間、サブスクライバーは失敗を受け取り、モジュールが再び有効になると値の受信を再開します。Tealiumインスタンスの初期化に失敗した場合、またはインスタンスがシャットダウンした場合、サブスクライバーは最後の失敗を1回受け取り、サブスクリプションが終了します。

## 訪問IDのリセット

新しい匿名訪問IDを生成するには、`regenerate()`を呼び出します。結果は、呼び出し時にデータレイヤー内にIDが存在するかどうかによって異なります。

* IDが存在する場合、そのIDが新しい訪問IDを所有します。
* IDが存在しない場合、新しい訪問IDには所有者がありません。次にデータレイヤーに書き込まれる新しいIDがその訪問IDを引き継ぎ、以前使用されたIDの場合は以前の訪問IDが復元されます。

`regenerate()`の呼び出しは任意です。次の場合に使用します。

* **ログアウト後**：データレイヤーからIDキーを削除してから、`regenerate()`を呼び出します。ログアウトしたIDにはその訪問IDが維持され、デバイスでは新しい訪問IDを使用して匿名での操作が継続されます。キーを削除する前に`regenerate()`を呼び出すと、SDKはそのIDを新しい訪問IDに関連付けます。
* **ログイン前**：新しいIDをデータレイヤーに書き込む前に`regenerate()`を呼び出します。これにより、新しいIDがデバイスで以前使用されていた訪問IDを引き継ぐことを防止できます。SDKは、両方の呼び出しを順番に処理します。



```kotlin
tealium.visitorId.regenerate().subscribe { result ->
    val newVisitorId = result.getOrNull()
}
```


```swift
tealium.visitorId.regenerate().subscribe { result in
    // Handle the result
}
```


## ローカル履歴を消去する

デバイス上のデータ削除リクエストを処理するには、`eraseLocalHistory()`を呼び出します。このメソッドは、IDと訪問IDの間に保存されているすべてのリンクを消去し、新しい匿名訪問IDを生成します。

呼び出し時にデータレイヤーにIDが存在する場合、SDKはそのIDを新しい訪問IDにリンクします。リンクを一切残さずに消去するには、最初にデータレイヤーからIDを削除してください。


<blockquote>
`eraseLocalHistory()`はデバイスにのみ影響します。データレイヤーからIDを削除したり、サーバー側の訪問プロファイルを変更したりすることはありません。これらは別途処理してください。
</blockquote>




```kotlin
tealium.visitorId.eraseLocalHistory().subscribe { result ->
    val newVisitorId = result.getOrNull()
}
```


```swift
tealium.visitorId.eraseLocalHistory().subscribe { result in
    // Handle the result
}
```



`regenerate()`または`eraseLocalHistory()`が変更を保存できない場合、メソッドは失敗を返します。それでもSDKは、アプリが再起動されるまで新しい訪問IDを使用します。次回の起動時に、SDKは以前の訪問IDと保存されていたすべてのリンクを復元します。

## 最初の訪問IDを構成する

以前のSDKから訪問IDを移行するには、既存の訪問IDを`TealiumConfig`に構成します。SDKは、訪問IDがまだ保存されていない初回起動時にのみ、そのIDを使用します。



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.collect())
)
    .setExistingVisitorId("EXISTING_VISITOR_ID")
    .build()
```


```swift
var config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [Modules.collect()])
config.existingVisitorId = "EXISTING_VISITOR_ID"
```



## APIリファレンス

クラスおよびメソッドの詳細なシグネチャについては、APIリファレンスドキュメントを参照してください。

* [VisitorIdManager（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/VisitorIdManager.html)
* [VisitorIdManager（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-visitor-id-manager/index.html)