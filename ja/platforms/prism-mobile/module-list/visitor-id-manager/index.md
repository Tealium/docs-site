---
title: Visitor ID Manager モジュール
description: Visitor ID Manager モジュールを使用して、モバイルアプリで匿名訪問 ID を作成、保存、切り替えます。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/visitor-id-manager/
---
Visitor ID Manager モジュールは、デバイスの匿名訪問 ID を管理するコレクターです。このモジュールは訪問 ID を作成して保存し、すべてのトラッキングイベントに追加します。また、データレイヤー内のユーザー ID が変更されたときに訪問 ID を切り替えます。このモジュールはデフォルトで有効になっており、自動的に追加されるため、構成なしで動作します。

アプリで訪問 ID を読み取り、管理するには、`VisitorIdManager` を返す `tealium.visitorId` を使用します。

## 収集されるデータ

| データポイント | キー | 説明 |
| :--- | :--- | :--- |
| 訪問 ID | `tealium_visitor_id` | デバイスの匿名訪問 ID。 |

## 構成

| 構成 | JSON キー | 説明 | デフォルト値 |
| :--- | :--- | :--- | :--- |
| 訪問 ID キー | `visitor_identity_key` | メールアドレスやユーザー ID など、現在のユーザーの ID を保持するデータレイヤーキー。このキーを構成すると、[訪問の切り替え](#visitor-switching)が有効になります。 | なし（訪問の切り替えはオフ） |

このモジュールは、共通の `enabled`、`order`、`rules` モジュール構成にも対応しています。ルールの詳細については、[ルール](https://docs.tealium.com/rules/)を参照してください。

JSON 構成ファイル、プログラム、またはその両方を使用してモジュールを構成します。

### JSON 構成

ローカル構成ファイルを使用するには、`TealiumConfig` の `settingsFile` にファイル名を渡します。リモート構成を使用するには、`settingsUrl` に URL を渡します。両方を使用すると、SDK はそれらをマージし、リモート構成を優先します。

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

SDK は、デフォルト構成でモジュールを追加します。モジュールの順序を変更する場合、構成を強制する場合、またはローカル構成かリモート構成に含まれている場合にのみモジュールを初期化する場合は、`TealiumConfig` の `modules` リストにモジュールを追加します。


<blockquote>
プログラムによる構成は、常にローカル構成とリモート構成より優先されます。リモートで変更されてはならない値のみを強制してください。
</blockquote>


構成を強制するには、ビルダークロージャを渡します。



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

モジュールを無効にするには、その構成で `enabled` を `false` に構成するか、ビルダーで `setEnabled(false)` を呼び出します。モジュールが無効になっている間は、次のように動作します。

* トラッキングイベントに `tealium_visitor_id` が含まれません。
* すべての `tealium.visitorId` メソッドが失敗を返します。
* 訪問の切り替えが停止し、SDK はデータレイヤー内の ID の変更を無視します。
* Collect モジュールは引き続きイベントを送信し、訪問 ID のないイベントをまとめてバッチ処理します。
* [Context API モジュール](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/)はエンジンのレスポンスを取得できません。

## 訪問の切り替え

訪問の切り替えでは、訪問 ID とデータレイヤーに書き込んだ ID を関連付けます。これにより、SDK は同じデバイス上でログインをまたいで同一人物を認識できます。SDK にはログインやログアウトという概念はありません。SDK は、`visitor_identity_key` に構成されたデータレイヤーキーを監視します。

* 新しい ID を書き込み、現在の訪問 ID をほかの ID が所有していない場合、SDK はその ID を現在の訪問 ID に関連付けます。
* 既知の ID を書き込むと、SDK は以前その ID に関連付けられていた訪問 ID を復元します。
* 異なる未知の ID を書き込むと、SDK は新しい訪問 ID を生成し、その ID に関連付けます。
* キーを削除するかキーの有効期限が切れた場合、訪問 ID は変更されず、SDK は ID が存在しないものとして記録します。

## 訪問 ID の読み取り

訪問 ID を一度だけ読み取るには、`current()` を呼び出します。現在の訪問 ID と、その後のすべての変更を受信するには、`tealium.visitorId` をサブスクライブします。SDK は、`regenerate()`、`eraseLocalHistory()`、または訪問の切り替え後に新しい値を送出します。



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



モジュールが無効になっている間、サブスクライバーは失敗を受信します。モジュールが再度有効になると、値の受信も再開します。Tealium インスタンスの初期化に失敗した場合、またはインスタンスがシャットダウンした場合、サブスクライバーは最後の失敗を 1 回受信し、サブスクリプションが終了します。

## 訪問 ID のリセット

新しい匿名訪問 ID を生成するには、`regenerate()` を呼び出します。結果は、呼び出し時にデータレイヤーに ID が存在するかどうかによって異なります。

* ID が存在する場合、その ID が新しい訪問 ID の所有者になります。
* ID が存在しない場合、新しい訪問 ID には所有者がありません。次に新しい ID がデータレイヤーに書き込まれると、その ID が新しい訪問 ID を引き継ぎます。以前使用された ID が再び書き込まれた場合は、その ID に以前関連付けられていた訪問 IDが復元されます。

`regenerate()` の呼び出しは任意です。次の場合に使用します。

* **ログアウト後**：データレイヤーから ID キーを削除してから、`regenerate()` を呼び出します。ログアウトした ID にはその訪問 ID が保持され、デバイスでは新しい訪問 ID を使用して匿名での操作が継続されます。キーを削除する前に `regenerate()` を呼び出すと、SDK はその ID を新しい訪問 ID に関連付けます。
* **ログイン前**：新しい ID をデータレイヤーに書き込む前に `regenerate()` を呼び出します。これにより、新しい ID がデバイスで以前使用されていた訪問 ID を引き継ぐことを防ぎます。SDK は両方の呼び出しを順番に処理します。



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

デバイス上のデータ削除リクエストを処理するには、`eraseLocalHistory()` を呼び出します。このメソッドは、ID と訪問 ID の間に保存されているすべてのリンクを消去し、新しい匿名の訪問 ID を生成します。

呼び出し時にデータレイヤーに ID が存在する場合、SDK はその ID を新しい訪問 ID にリンクします。リンクを一切残さずに消去するには、まずデータレイヤーから ID を削除してください。


<blockquote>
`eraseLocalHistory()` が影響するのはデバイスのみです。データレイヤーから ID を削除したり、サーバー側の訪問プロファイルを変更したりすることはありません。これらは個別に処理してください。
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



`regenerate()` または `eraseLocalHistory()` が変更を保存できない場合、メソッドは失敗を返します。それでも、アプリが再起動されるまで SDK は新しい訪問 ID を使用します。次回の起動時に、SDK は以前の訪問 ID と保存されていたすべてのリンクを復元します。

## 最初の訪問 ID を構成する

以前の SDK から訪問 ID を移行するには、既存の訪問 ID を `TealiumConfig` に構成します。SDK がその ID を使用するのは、訪問 ID がまだ保存されていない初回起動時のみです。



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



## API リファレンス

クラスおよびメソッドの詳細なシグネチャについては、API リファレンスドキュメントを参照してください。

* [VisitorIdManager（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/VisitorIdManager.html)
* [VisitorIdManager（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-visitor-id-manager/index.html)