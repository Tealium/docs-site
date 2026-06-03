---
title: TAPIDクッキーについて
description: このドキュメントでは、TAPIDクッキーとは何か、Tealiumプラットフォームがそれをどのように使用するかについて説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/tapid/
---
## 仕組み

TAPIDはHTTP専用のブラウザクッキーです。元々はクロスドメイン識別を容易にするために設計され、Tealiumのサーバーサイド製品（例：AudienceStream）が使用する[匿名ID]()を保存します。

 訪問のコンピュータに[Collect Tag]()のターゲットドメインに構成されたTAPIDクッキーがまだない場合、そのドメインはCollect Tagのペイロードに基づいて一つを生成します。

TAPIDクッキーの値はそのユーザーの訪問IDに構成されます。この値は通常、クライアントデバイスから来ます。TAPIDは、ユーザーのデバイスが訪れたアカウントとプロファイルの値の連結リストに値を保存します。以下の形式を使用します：

```
account-1/profile-1&gt;visitor_id_value-1|account-2/profile-2&gt;visitor_id_value-2
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

詳細については、[訪問の切り替え](/ja/platforms/http-api/endpoint/#visitor-switching)を参照してください。

### ブラウザのサポート

サードパーティクッキーに対するブラウザのサポートが減少し続ける中で、ドメイン間でユーザーを匿名で追跡する能力はますます困難になっています。[訪問のスティッチング]()を使用すると、AudienceStreamはデータレイヤーで自分自身を識別するユーザーを2つ以上のドメイン間で解決することができます。

## ファーストパーティドメインとTAPID  

ファーストパーティドメインを使用すると、Tealiumのサービスはファーストパーティリクエストを使用でき、これにより広告ブロッカーや同様の技術によるデータ損失を減らすことができます。

ファーストパーティドメインとは、ユーザーが訪れているウェブサイトをホストするドメインのことです。サードパーティドメインとは、現在のウェブサイトのドメインと一致しない任意のドメインを指します。

ファーストパーティドメインを使用すると、TAPIDクッキーは引き続きHTTP専用のブラウザクッキーとなりますが、Tealiumのサードパーティドメインではなく、ウェブサイトをホストするファーストパーティドメインに割り当てられます。したがって、ファーストパーティドメインはTAPIDクッキーがクロスドメイン追跡機能を失う原因となります。

詳細については、[ファーストパーティドメインについて]()を参照してください。

## TAPIDクッキーデータの変更

APIリクエストには、TAPIDクッキーの値を変更するための3つのパラメータが含まれています。これらのパラメータは、現在の入力リクエストに関連するTAPIDのアカウントとプロファイルの値のみに影響を与えます。それ以外のアカウントとプロファイルの値は変更されません。

パラメータは以下のエンドポイントをサポートします：

* `i.gif` - [Tealium Collect tag]()
* `vdata` - [Visitor Data Enrichment]()
* `/event` - [HTTP API](/ja/platforms/http-api/endpoint/#visitor-switching)

 `/event`エンドポイントは、事前に構成されたTAPIDの値を読み取ることができますが、TAPIDクッキー内の値を変更することはできません。

| パラメータ | タイプ | アクション | ノート | 
|--------|--------|--------|--------|
| `tealium_override_tapid`  | String  | &lt;ul&gt;&lt;li&gt;このイベントの訪問IDとして提供された値をAudienceStreamとサーバーサイド製品が使用するようにします。&lt;/li&gt;&lt;li&gt;`i.gif`と`vdata`では、しかし`/event`ではなく、`Set-Cookie`レスポンスヘッダーを変更して、TAPIDを変更するために渡す値を使用します。&lt;/li&gt;&lt;/ul&gt; |このパラメータは、クロスドメイン追跡のためのTAPIDを保持しながら、最後に知られているユーザーに基づいて訪問の切り替えを可能にします。 |
| `tealium_delete_3rd_party_vid_cookies`  | Boolean |  &lt;ul&gt;&lt;li&gt;このイベントの訪問プロファイルIDの優先順位を見るときに、AudienceStreamとサーバーサイド製品がTAPIDクッキーの入力リクエスト値を無視します。&lt;/li&gt;&lt;li&gt;`i.gif`と`vdata`では、しかし`/event`ではなく、現在のアカウントとプロファイルのTAPIDを削除するために`Set-Cookie`レスポンスヘッダーを変更します。&lt;/li&gt;&lt;/ul&gt; | |
| `tealium_skip_3rd_party_vid_cookies`  | Boolean | このイベントのTAPID値をAudienceStreamとサーバーサイド製品が無視します。 | |

パラメータは現在のイベントのみに影響します。例えば、一つのイベントで`skip`パラメータを渡し、次のイベントでは渡さない場合、次のイベントはTAPIDクッキーをスキップしません。しかし、`override`パラメータを一度構成すると、TAPIDは指定した値に変更されます。

### 例

以下の例は、3つのパラメータがTAPIDデータをどのように変更するかを示しています。

#### オーバーライド

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

Set Cookie (オーバーライド):  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user&#34;, // オーバーライド
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // オーバーライド
}
```

#### スキップ

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

Set Cookie:  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/alt&gt;67890|tealium/main&gt;12345|;
```

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPIDスキップ
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;67890&#34;
}
```

#### 削除

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

Set Cookie (リセット):  `i.gif`と`vdata`のみ、`/event`ではない

```
TAPID=tealium/main&gt;12345|;
```

TAPIDが`account/profile`部分のTAPIDを削除した後に空になる場合、`set-cookie maxAge=0`がクライアントからクッキーを完全に削除するために返されます。`i.gif`と`vdata`のみ、`/event`ではない

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;,
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;
}
```

#### オーバーライド &amp; スキップ

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
&#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

クッキー構成（上書き）:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPIDはスキップされます
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // 上書きされます
}
```

#### 上書き &amp; 削除

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

クッキー構成:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

`tealium_override_tapid`は`tealium_delete_3rd_party_vid_cookies`より優先されます

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user&#34;, 
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // 上書きされます
}
```

#### スキップ &amp; 削除

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

クッキー構成（リセット）:  `i.gif`と`vdata`のみ、`/event`は除く

```
TAPID=tealium/main&gt;12345|;
```

TAPIDが`account/profile`部分のTAPIDを削除した後に空になる場合、クライアントからクッキーを完全に削除するために`set-cookie maxAge=0`が返されます。`i.gif`と`vdata`のみ、`/event`は除く

##### イベント

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPIDは削除され、とにかくスキップされます
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;
}
```

#### 上書き、スキップ、&amp; 削除

##### リクエスト

**ボディ:**

```
{
  &#34;tealium_account&#34;: &#34;tealium&#34;,
  &#34;tealium_profile&#34;: &#34;alt&#34;,
  &#34;tealium_visitor_id&#34;: &#34;user@tealium.com&#34;,
  &#34;tealium_override_tapid&#34;: &#34;user&#34;,
  &#34;tealium_skip_3rd_party_vid_cookies&#34;: true,
  &#34;tealium_delete_3rd_party_vid_cookies&#34;: true
}
```

**クッキー:**

```
TAPID=tealium/main&gt;12345|tealium/alt&gt;67890|;
```

##### レスポンス

クッキー構成:  `i.gif`と`vdata`のみ、`/event`は除く


```
TAPID=tealium/alt&gt;user|tealium/main&gt;12345|;
```

`tealium_override_tapid`は`tealium_delete_3rd_party_vid_cookies`より優先されます


##### イベント

```
{
  &#34;visitorId&#34;: &#34;user@tealium.com&#34;, // TAPIDはスキップされます
  &#34;firstPartyCookieId&#34;: &#34;user@tealium.com&#34;,
  &#34;thirdPartyCookieId&#34;: &#34;user&#34; // 上書きされます
}
```