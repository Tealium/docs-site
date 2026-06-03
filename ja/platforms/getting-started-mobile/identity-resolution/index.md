---
title: アイデンティティ解決
description: アイデンティティ解決について学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/
---
## 匿名ID

Tealiumライブラリは、最初に起動されたときに一意の永続的な匿名IDを生成し、それを `tealium.visitorId` に保存します。この値は、追跡された各イベントに `tealium_visitor_id` 属性として含まれます。




```java
class TealiumHelper {
	lateinit var tealium: Tealium

    fun getVisitorId(): String {
        return tealium.visitorId
    }
}
```




```swift
class TealiumHelper {
	var tealium: Tealium?

    var visitorId: String? {
		tealium?.visitorId
	}
}
```




Tealium AudienceStreamを使用している場合、`visitorId` は訪問に関連付けられた匿名IDです。[AudienceStreamの匿名ID]()について詳しく学びましょう。

## 匿名IDのリセット

必要に応じて、このメソッドを呼び出すことで現在の `visitorId` をリセットできます：

```
tealium.resetVisitorId()
```

## ユーザー識別子

既知のユーザーを識別するときは、永続的なデータストレージにユーザー識別子属性を追加します。

ユーザー識別子、たとえば顧客IDを追加するには：




```java
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString(&#34;customer_id&#34;, id, Expiry.FOREVER)
}
```




```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: &#34;customer_id&#34;, value: id, expiration: .forever)
}
```




## 訪問の切り替え

アプリが複数のユーザーをサポートしている場合、AudienceStream CDPプロファイルを分けて、間違ったユーザーにターゲットメッセージや広告を送信するのを避けることが重要です。有効にすると、Tealium SDKの訪問切り替え機能は自動的にアプリのユーザー変更を監視し、新しいユーザーが検出されるたびに `tealium_visitor_id` をリセットします。

この機能を有効にするには、訪問の識別キーを `TealiumConfig` インスタンスに渡す必要があります。このキーは、新しい訪問がログインしたかどうかを判断するためにSDKが監視するデータレイヤー項目を指定します。新しい訪問が検出されると、新しい訪問IDが割り当てられ、データレイヤーに挿入され、訪問の切り替え時点から生成されるイベントに影響を与えます。

AudienceStreamで各ユーザーに割り当てられる訪問IDの数を減らすために（パフォーマンス上の理由で推奨）、SDKが以前にログインしたユーザーへの切り替えを検出した場合、そのユーザーの元の訪問IDが使用されます。この機能をサポートするために、`tealium_visitor_id` とカスタムデータレイヤーキーの値はデバイス上にローカルに保存されます。

IDは常に `SHA-256` アルゴリズムでハッシュ化されます。ハッシュ化されたIDは比較目的のみで使用されます。個人データをハッシュ化解除する方法はありませんし、ハッシュ化された値はデバイスから送信されることはありません。

### 構成

訪問の切り替えは、アプリユーザーを識別するキーの名前をデータレイヤーに渡すことで有効になります：




```java
config.visitorIdentityKey = &#34;customer_id&#34;
```




```swift
config.visitorIdentityKey = &#34;customer_id&#34;
```




訪問の識別キーが構成されると、ユーザーの既知のID（この場合は `customer_id`）が変更されるたびに、SDKはデータレイヤー内の現在の `tealium_visitor_id` を変更します。顧客IDがすでに存在する場合、`tealium_visitor_id` はこの訪問の既存の顧客IDに構成されます。しかし、顧客IDが存在しない場合、新しい `tealium_visitor_id` が生成されます。

### 保存された識別子の削除

ユーザーの削除リクエストに準じるなど、一部のケースでは、ユーザーのデバイスからすべての保存された識別子を削除する必要があるかもしれません。これを行うには：

```
tealium.clearStoredVisitorIds()
```

`visitorIdentityKey` が `TealiumConfig` インスタンスに存在し、`dataLayer` が訪問識別子を含んでいる場合、訪問IDの保存は現在の識別子と新しい `tealium_visitor_id` で自動的に再生成されます。

すべての以前に保存された識別子をクリアした後、現在の訪問の `tealium_visitor_id` は新しい識別子にリセットされます。

これは絶対に必要な場合にのみ実行することを強く推奨します。なぜなら、保存されたIDを定期的にクリアすると、機能が意図した通りに動作しなくなり、AudienceStreamの構成に問題が生じる可能性があるからです。

## 匿名IDの変更をリッスンする

Tealiumインスタンスは、`onVisitorId` にサブスクライブできる観測可能なプロパティを提供します。以下のインスタンスで現在の `tealium_visitor_id` とともにサブスクリプションが呼び出されます：

* アプリの起動時。
* `resetVisitorId` が呼び出された後に `tealium_visitor_id` が変更されたとき。
* SDKがデータレイヤー内のvisitorIdentityKeyに基づいて訪問の変更を自動的に検出したとき。
