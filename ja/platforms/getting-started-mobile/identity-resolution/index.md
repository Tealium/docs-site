---
title: ID 解決
description: ID 解決について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/
---
## 匿名 ID

Tealium ライブラリは、初回起動時に一意で永続的な匿名 ID を生成し、`tealium.visitorId` に保存します。この値は、属性 `tealium_visitor_id` として、トラッキングされる各イベントに含まれます。




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




Customer Data Platform（CDP）を使用している場合、`visitorId` は訪問に関連付けられた匿名 ID です。詳しくは、[Customer Data Platform（CDP）の匿名 ID](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

## 匿名 ID のリセット

必要に応じて、次のメソッドを呼び出すことで、現在の `visitorId` をリセットできます。

```
tealium.resetVisitorId()
```

## ユーザー識別子

既知のユーザーを識別する場合は、永続データ保存にユーザー識別子属性を追加します。

顧客 ID などのユーザー識別子を追加するには、次のようにします。




```java
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString("customer_id", id, Expiry.FOREVER)
}
```




```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: "customer_id", value: id, expiration: .forever)
}
```




## 訪問の切り替え

アプリが複数のユーザーに対応している場合、ターゲットメッセージや広告が誤ったユーザーに送信されるのを防ぐため、ユーザーごとに CDP プロファイルを分けることが重要です。有効にすると、Tealium SDK の訪問切り替え機能がアプリ内のユーザー変更を自動的に監視し、新しいユーザーを検出するたびに `tealium_visitor_id` をリセットします。

この機能を有効にするには、訪問 ID キーを `TealiumConfig` インスタンスに渡す必要があります。このキーは、新しい訪問がログインしたかどうかを判定するために監視するデータレイヤー項目を SDK に指定します。新しい訪問が検出されると、新しい訪問 ID が割り当てられてデータレイヤーに挿入されます。これにより、訪問が切り替わった時点以降に生成されるすべてのイベントが影響を受けます。

各ユーザーに割り当てられる訪問 ID の数を減らすため（CDP のパフォーマンス上の理由から推奨）、以前にログインしたことのあるユーザーへの切り替えを SDK が検出した場合は、そのユーザーの元の訪問 ID が使用されます。この機能をサポートするため、`tealium_visitor_id` とカスタムデータレイヤーキーの値はデバイス上にローカル保存されます。


<blockquote>
ID は常に `SHA-256` アルゴリズムでハッシュ化されます。ハッシュ化された ID は比較目的にのみ使用されます。個人データのハッシュ化を元に戻すことはできず、ハッシュ値がデバイスから送信されることもありません。
</blockquote>


### 構成

データレイヤー内でアプリユーザーを識別するキーの名前を `TealiumConfig` インスタンスに渡すことで、訪問切り替えを有効にします。




```java
config.visitorIdentityKey = "customer_id"
```




```swift
config.visitorIdentityKey = "customer_id"
```




訪問 ID キーを構成すると、ユーザーの既知の ID（この場合は `customer_id`）が変更されるたびに、SDK はデータレイヤー内の現在の `tealium_visitor_id` を変更します。顧客 ID がすでに存在する場合、`tealium_visitor_id` には、この訪問に対する既存の顧客 ID が構成されます。顧客 ID が存在しない場合は、新しい `tealium_visitor_id` が生成されます。

### 保存された識別子の削除

ユーザーからの削除リクエストに対応する場合など、ユーザーのデバイスから保存済みの識別子をすべて削除する必要があることがあります。削除するには、次を実行します。

```
tealium.clearStoredVisitorIds()
```

`visitorIdentityKey` が `TealiumConfig` インスタンスに存在し、`dataLayer` に訪問識別子が含まれている場合、訪問 ID 保存には、現在の ID と新しい `tealium_visitor_id` が自動的に再登録されます。

以前に保存された識別子をすべて消去すると、現在の訪問の `tealium_visitor_id` は新しい識別子にリセットされます。


<blockquote>
この操作は、どうしても必要な場合にのみ実行することを強く推奨します。保存された ID を定期的に消去すると、機能が意図どおりに動作しなくなり、CDP の構成で問題が発生する可能性があります。
</blockquote>


## 匿名 ID の変更の監視

Tealium インスタンスには、サブスクライブ可能な監視対象プロパティ `onVisitorId` が用意されています。次の場合に、現在の `tealium_visitor_id` を引数としてサブスクリプションが呼び出されます。

* アプリの起動時。
* `resetVisitorId` の呼び出し後に `tealium_visitor_id` が変更されたとき。
* SDK がデータレイヤー内の visitorIdentityKey に基づいて訪問の変更を自動的に検出したとき。