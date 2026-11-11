---
title: TAPID Cookie について
description: このドキュメントでは、TAPID Cookie の概要と Tealium プラットフォームでの使用方法について説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/tapid/
---
## 仕組み

TAPID は HTTP-only のブラウザー Cookie です。元々はクロスドメインでの識別を容易にするために設計されたもので、Customer Data Platform（CDP）など、Tealium のサーバーサイド製品で使用される[匿名 ID](https://docs.tealium.com/anonymous-user-visitor-id-attributes/#anonymous-id) を保存します。


<blockquote>
訪問のコンピューターに、[Collect タグ]()のターゲットドメインで構成された TAPID Cookie がまだ存在しない場合、そのドメインは Collect タグのペイロードに基づいて Cookie を生成します。
</blockquote>


TAPID Cookie の値には、そのユーザーの訪問 ID が構成されます。この値は通常、クライアントデバイスから取得されます。TAPID は、ユーザーのデバイスが訪問したアカウントとプロファイルの値を、次の形式で連結したリストとして保存します。

```
account-1/profile-1>visitor_id_value-1|account-2/profile-2>visitor_id_value-2
```

TAPID は通常サードパーティ Cookie ですが、[ファーストパーティドメイン]()を使用すると、ファーストパーティ Cookie にできます。

一度構成されると、Cookie 内の `visitor_id_value` は通常変更されません。

### TAPID 内のアカウントとプロファイルの値

Web ページ上の TAPID Cookie に含まれるアカウントとプロファイルの値を確認するには、次の手順を実行します。

1. ブラウザーで、Tealium Collect タグを読み込む Web ページを開きます。
1. ブラウザーの開発者コンソールを開きます。
1. **Network** リクエストを `teal` でフィルタリングします。
1. ページを更新します。
1. Collect タグの参照（`i.gif` または `/event`）を見つけます。
1. リクエストヘッダーを確認し、ターゲットのアカウントとプロファイルを特定します。
1. レスポンスを確認して、TAPID Cookie の値を表示します。
1. TAPID Cookie から、対象のアカウントとプロファイルに関連する部分を抽出します。

## ID 解決

CDP は、次の優先順位に基づいて訪問プロファイル ID を決定します。

1. TAPID Cookie（`tealium_thirdparty_visitor_id` とも呼ばれます）。
1. `tealium_visitor_id` イベント属性。
1. `utag_main v_id cookie`（`tealium_firstparty_visitor_id` とも呼ばれます）。

受信リクエストに TAPID 識別子が含まれている場合、CDP は常にこれをプライマリ識別子として使用します。ユーザーが 2 つのドメインにまたがって追跡される場合、CDP はユーザーの識別に 2 つ目のドメインのファーストパーティ Cookie を使用しません。そのため、CDP では、2 つ目のドメインのファーストパーティ Cookie に基づいてユーザーを検索できません。

### 訪問スティッチングの問題

共有スマートテレビや公共のキオスク端末など、複数の訪問が 1 台のデバイスを使用すると、訪問のプロファイルデータが混在する可能性があります。2 人目のユーザーが匿名 Cookie を使用してそのデバイスにログインしても、CDP は引き続き最初のユーザーのアクティビティとして記録します。デバイス上のすべての匿名ユーザーからのトラフィックが、TAPID Cookie 内の最初のユーザーに記録されます。

詳細については、[訪問の切り替え](https://docs.tealium.com/ja/platforms/http-api/endpoint/#visitor-switching)を参照してください。

### ブラウザーのサポート

サードパーティ Cookie に対するブラウザーのサポートが減少し続ける中、ドメインをまたいでユーザーを匿名で追跡することは難しくなっています。[訪問スティッチング]()を使用すると、ユーザーがデータレイヤーで自身を識別した際に、CDP は 2 つ以上のドメインにまたがってそのユーザーを解決できます。

## ファーストパーティドメインと TAPID

ファーストパーティドメインを使用すると、Tealium のサービスでファーストパーティリクエストを使用できるため、広告ブロッカーや同様のテクノロジーによって生じるデータ損失を軽減できます。

ファーストパーティドメインとは、ユーザーが訪問している Web サイトをホストするドメインです。サードパーティドメインとは、現在の Web サイトのドメインと一致しないドメインを指します。

ファーストパーティドメインを使用しても、TAPID Cookie は引き続き HTTP-only のブラウザー Cookie ですが、Tealium のサードパーティドメインではなく、Web サイトをホストするファーストパーティドメインに割り当てられます。そのため、ファーストパーティドメインを使用すると、TAPID Cookie のクロスドメイン追跡機能は失われます。

詳細については、[ファーストパーティドメインについて](https://docs.tealium.com/about-first-party-domains/)を参照してください。

## TAPID Cookie データの変更

API リクエストには、TAPID Cookie の値を変更できる 3 つのパラメータがあります。これらのパラメータは、現在の受信リクエストに関連する TAPID 内のアカウントとプロファイルの値にのみ影響します。その他のアカウントとプロファイルの値は変更されません。

これらのパラメータは、次のエンドポイントでサポートされています。

* `i.gif` - [Tealium Collect タグ]()
* `vdata` - [訪問データエンリッチメント]()
* `/event` - [HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/#visitor-switching)


<blockquote>
`/event` エンドポイントは、以前に構成されている TAPID 値を読み取ることはできますが、TAPID Cookie 内の値を変更することはできません。
</blockquote>


| パラメータ | 型 | アクション | 備考 |
|--------|--------|--------|--------|
| `tealium_override_tapid` | 文字列 | <ul><li>CDP およびサーバーサイド製品で、指定された値をこのイベントの訪問 ID として使用します。</li><li>`i.gif` と `vdata` では（`/event` を除く）、`Set-Cookie` レスポンスヘッダーを変更し、渡された値を使用して TAPID を変更します。</li></ul> | このパラメータを使用すると、クロスドメイン追跡用の TAPID を維持しながら、最後に認識されたユーザーに基づいて訪問を切り替えることができます。 |
| `tealium_delete_3rd_party_vid_cookies` | ブール値 | <ul><li>CDP およびサーバーサイド製品で、このイベントの訪問プロファイル ID の優先順位を確認する際に、受信リクエスト内の TAPID Cookie の値を無視します。</li><li>`i.gif` と `vdata` では（`/event` を除く）、`Set-Cookie` レスポンスヘッダーを変更し、現在のアカウントとプロファイルの TAPID を削除します。</li></ul> | |
| `tealium_skip_3rd_party_vid_cookies` | ブール値 | CDP およびサーバーサイド製品で、このイベントの TAPID 値を無視します。 | |

これらのパラメータは、現在のイベントにのみ影響します。たとえば、あるイベントでは `skip` パラメータを渡し、次のイベントでは渡さなかった場合、次のイベントでは TAPID Cookie はスキップされません。ただし、`override` パラメータを一度構成すると、TAPID は指定した値に変更されます。

### 例

次の例は、3 つのパラメータによって TAPID データがどのように変更されるかを示しています。

#### 上書き

##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user"
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie の構成（上書き）：`i.gif` と `vdata` のみ。`/event` は対象外

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user", // Overridden
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // Overridden
}
```

#### スキップ

##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_skip_3rd_party_vid_cookies": true
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie の構成：`i.gif` と `vdata` のみ。`/event` は対象外

```
TAPID=tealium/alt>67890|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPID skipped
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "67890"
}
```

#### 削除

##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie の構成（リセット）：`i.gif` と `vdata` のみ。`/event` は対象外

```
TAPID=tealium/main>12345|;
```

TAPID から `account/profile` 部分を削除した後に TAPID が空になった場合は、クライアントから Cookie を完全に削除するために `set-cookie maxAge=0` が返されます。これは `i.gif` と `vdata` のみが対象で、`/event` は対象外です。

##### イベント

```
{
  "visitorId": "user@tealium.com",
  "firstPartyCookieId": "user@tealium.com"
}
```

#### 上書きとスキップ
##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user",
  "tealium_skip_3rd_party_vid_cookies": true
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie を構成（上書き）：`i.gif` と `vdata` のみ。`/event` は対象外です。

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPID Skipped
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // Overridden
}
```

#### 上書きと削除

##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_override_tapid": "user",
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie を構成：`i.gif` と `vdata` のみ。`/event` は対象外です。

```
TAPID=tealium/alt>user|tealium/main>12345|;
```

`tealium_override_tapid` は `tealium_delete_3rd_party_vid_cookies` より優先されます。

##### イベント

```
{
  "visitorId": "user", 
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // Overridden
}
```

#### スキップと削除

##### リクエスト

**本文：**

```
{
  "tealium_account": "tealium",
  "tealium_profile": "alt",
  "tealium_visitor_id": "user@tealium.com",
  "tealium_skip_3rd_party_vid_cookies": true,
  "tealium_delete_3rd_party_vid_cookies": true
}
```

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie を構成（リセット）：`i.gif` と `vdata` のみ。`/event` は対象外です。

```
TAPID=tealium/main>12345|;
```

TAPID から `account/profile` の部分を削除した後に TAPID が空になった場合、クライアントから Cookie を完全に削除するために `set-cookie maxAge=0` が返されます。`i.gif` と `vdata` のみが対象で、`/event` は対象外です。

##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPID deleted and anyway skipped
  "firstPartyCookieId": "user@tealium.com"
}
```

#### 上書き、スキップ、削除

##### リクエスト

**本文：**

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

**Cookie：**

```
TAPID=tealium/main>12345|tealium/alt>67890|;
```

##### レスポンス

Cookie を構成：`i.gif` と `vdata` のみ。`/event` は対象外です。


```
TAPID=tealium/alt>user|tealium/main>12345|;
```

`tealium_override_tapid` は `tealium_delete_3rd_party_vid_cookies` より優先されます。


##### イベント

```
{
  "visitorId": "user@tealium.com", // TAPID Skipped
  "firstPartyCookieId": "user@tealium.com",
  "thirdPartyCookieId": "user" // Overridden
}
```