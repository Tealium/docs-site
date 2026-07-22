---
title: TAPIDクッキーについて
description: このドキュメントでは、TAPIDクッキーとは何か、Tealiumプラットフォームがそれをどのように使用するかについて説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/tapid/
---
## 仕組み

TAPIDはHTTP専用のブラウザクッキーです。元々はクロスドメイン識別を容易にするために設計され、Tealiumのサーバーサイド製品（例：AudienceStream）が使用する[匿名ID](https://docs.tealium.com/anonymous-user-visitor-id-attributes/#anonymous-id)を保存します。


<blockquote>
訪問のコンピュータに[Collect Tag]()のターゲットドメインに構成されたTAPIDクッキーがまだない場合、そのドメインはCollect Tagのペイロードに基づいて一つを生成します。
</blockquote>


TAPIDクッキーの値はそのユーザーの訪問IDに構成されます。この値は通常、クライアントデバイスから来ます。TAPIDは、ユーザーのデバイスが訪れたアカウントとプロファイルの値の連結リストに値を保存します。以下の形式を使用します：

```
account-1/profile-1>visitor_id_value-1|account-2/profile-2>visitor_id_value-2
```

TAPIDは通常、サードパーティのクッキーですが、[ファーストパーティドメイン]()を使用すると、ファーストパーティのクッキーになることもあります。

一度構成されると、クッキー内の`visitor_id_value`は通常変更されません。

### TAPIDのアカウントとプロファイルの値

ウェブページ上のTAPIDクッキーのアカウントとプロファイルの値を見つけるには、以下の手順を実行します：

1. ブラウザでTealium Collectタグを読み込むウェブページを開きます。
1. ブラウザの開発者コンソールを開きます。
1. `teal`で**Network**リクエストをフィルタリングします。
1. ページを更新します。
1. collectタグの参照（`i.gif`または`/event`）を見つけます。
1. リクエストヘッダーを調べて、ターゲットアカウントとプロファイルを決定します。
1. TAPIDクッキーの値を確認するためにレスポンスを調べます。
1. アカウントとプロファイルに関連するTAPIDクッキーの部分を抽出します。

## アイデンティティ解決

AudienceStreamは、以下の順序に基づいて訪問プロファイルIDを決定します：

1. TAPIDクッキー、別名`tealium_thirdparty_visitor_id`。
1. `tealium_visitor_id`イベント属性。
1. `utag_main v_id cookie`、別名`tealium_firstparty_visitor_id`。

AudienceStreamは、入力リクエストに存在する場合、常にTAPID識別子を主要な識別子として使用します。ユーザーが2つのドメイン間で追跡されている場合、AudienceStreamは2つ目のドメインのファーストパーティクッキーを使用してユーザーを識別しません。したがって、AudienceStreamでは、2つ目のドメインのファーストパーティクッキーに基づいてユーザーを検索することはできません。

### 訪問のスティッチング問題

複数の訪問がデバイス（共有スマートテレビや公共のキオスクなど）を使用すると、訪問のプロファイルデータが汚染される可能性があります。2番目のユーザーが匿名クッキーでそのデバイスにログインすると、AudienceStreamは最初のユーザーの活動を続けて記録します。デバイス上のすべての匿名ユーザーからのトラフィックは、TAPIDクッキーの最初のユーザーに記録されます。

詳細については、[訪問の切り替え](https://docs.tealium.com/ja/platforms/http-api/endpoint/#visitor-switching)を参照してください。

### ブラウザのサポート

サードパーティクッキーに対するブラウザのサポートが減少し続ける中で、ドメイン間でユーザーを匿名で追跡する能力はますます困難になっています。[訪問のスティッチング]()を使用すると、AudienceStreamはデータレイヤーで自分自身を識別するユーザーを2つ以上のドメイン間で解決することができます。

## ファーストパーティドメインとTAPID  

ファーストパーティドメインを使用すると、Tealiumのサービスはファーストパーティリクエストを使用でき、これにより広告ブロッカーや同様の技術によるデータ損失を減らすことができます。

ファーストパーティドメインとは、ユーザーが訪れているウェブサイトをホストするドメインのことです。サードパーティドメインとは、現在のウェブサイトのドメインと一致しない任意のドメインを指します。

ファーストパーティドメインを使用すると、TAPIDクッキーは引き続きHTTP専用のブラウザクッキーとなりますが、Tealiumのサードパーティドメインではなく、ウェブサイトをホストするファーストパーティドメインに割り当てられます。したがって、ファーストパーティドメインはTAPIDクッキーがクロスドメイン追跡機能を失う原因となります。

詳細については、[ファーストパーティドメインについて](https://docs.tealium.com/about-first-party-domains/)を参照してください。

## TAPIDクッキーデータの変更

APIリクエストには、TAPIDクッキーの値を変更するための3つのパラメータが含まれています。これらのパラメータは、現在の入力リクエストに関連するTAPIDのアカウントとプロファイルの値のみに影響を与えます。それ以外のアカウントとプロファイルの値は変更されません。

パラメータは以下のエンドポイントをサポートします：

* `i.gif` - [Tealium Collect tag]()
* `vdata` - [Visitor Data Enrichment]()
* `/event` - [HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/#visitor-switching)


<blockquote>
`/event`エンドポイントは、事前に構成されたTAPIDの値を読み取ることができますが、TAPIDクッキー内の値を変更することはできません。
</blockquote>


| パラメータ | タイプ | アクション | ノート | 
|--------|--------|--------|--------|
| `tealium_override_tapid`  | String  | <ul><li>このイベントの訪問IDとして提供された値をAudienceStreamとサーバーサイド製品が使用するようにします。</li><li>`i.gif`と`vdata`では、しかし`/event`ではなく、`Set-Cookie`レスポンスヘッダーを変更して、TAPIDを変更するために渡す値を使用します。</li></ul> |このパラメータは、クロスドメイン追跡のためのTAPIDを保持しながら、最後に知られているユーザーに基づいて訪問の切り替えを可能にします。 |
| `tealium_delete_3rd_party_vid_cookies`  | Boolean |  <ul><li>このイベントの訪問プロファイルIDの優先順位を見るときに、AudienceStreamとサーバーサイド製品がTAPIDクッキーの入力リクエスト値を無視します。</li><li>`i.gif`と`vdata`では、しかし`/event`ではなく、現在のアカウントとプロファイルのTAPIDを削除するために`Set-Cookie`レスポンスヘッダーを変更します。</li></ul> | |
| `tealium_skip_3rd_party_vid_cookies`  | Boolean | このイベントのTAPID値をAudienceStreamとサーバーサイド製品が無視します。 | |

パラメータは現在のイベントのみに影響します。例えば、一つのイベントで`skip`パラメータを渡し、次のイベントでは渡さない場合、次のイベントはTAPIDクッキーをスキップしません。しかし、`override`パラメータを一度構成すると、TAPIDは指定した値に変更されます。

### 例

以下の例は、3つのパラメータがTAPIDデータをどのように変更するかを示しています。

#### オーバーライド

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user"
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Set Cookie (オーバーライド):  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user", // オーバーライド
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // オーバーライド
}
```

#### スキップ

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_skip_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Set Cookie:  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/alt>67890|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPIDスキップ
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "67890"
}
```

#### 削除

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Set Cookie (リセット):  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/main>12345|;
```

TAPIDが`account/profile`部分のTAPIDを削除した後に空になる場合、`set-cookie maxAge=0`がクライアントからクッキーを完全に削除するために返されます。`i.gif`と`vdata`のみ、`/event`ではない

##### イベント

```
{
  "visitorId": "user@tealium.com",
  "firstPartyCookieId": "user@tealium.com"
}
```

#### オーバーライド & スキップ

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
"tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user",
  "tealium_skip_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

クッキー構成（上書き）:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPIDはスキップされます
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // 上書きされます
}
```

#### 上書き & 削除

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user",
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

クッキー構成:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

`tealium_override_tapid`は`tealium_delete_3rd_party_vid_cookies`より優先されます

##### イベント

```
{
  "visitorId": "user", 
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // 上書きされます
}
```

#### スキップ & 削除

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_skip_3rd_party_vid_cookies": true,
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

クッキー構成（リセット）:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/main>12345|;
```

TAPIDが`account/profile`部分のTAPIDを削除した後に空になる場合、クライアントからクッキーを完全に削除するために`set-cookie maxAge=0`が返されます。`i.gif`と`vdata`のみ、`/event`は除く

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPIDは削除され、とにかくスキップされます
  "firstPartyCookieId": "user@tealium.com"
}
```

#### 上書き、スキップ、& 削除

##### リクエスト

**ボディ:**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user",
  "tealium_skip_3rd_party_vid_cookies": true,
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**クッキー:**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

クッキー構成:  `i.gif`と`vdata`のみ、`/event`は除く


```
TAPID=tealium/alt>user|tealium/main>12345|;
```

`tealium_override_tapid`は`tealium_delete_3rd_party_vid_cookies`より優先されます


##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPIDはスキップされます
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // 上書きされます
}
```