---
title: Merkle Merkuryタグ構成ガイド
description: この記事では、タグ管理アカウントでMerkle Merkuryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/merkle-merkury-tag/
---
## タグに関するヒント

* Adobe MediaSDKを使用するには、Adobe Experience Cloud ID ServiceおよびAppMeasurement for JSを先に読み込む必要があります。これらはバンドルすることを推奨します。
* このタグは`utag.track('video', data);`を通じて発火します。このコードを動画イベントハンドラーに実装してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **CID**  
Merkuryチームによって生成される、クライアント固有の数値アカウント番号。
* **ドメイン**  
クライアントWebサイトのドメイン。例：`merkleinc.com`。
* **Merkury Identityイベントを送信**  
次の情報を含む`merkury_identity`イベントを生成するかどうかを指定します。
  * `event`
  * `merkury_email_sha256`
  * `merkury_hmid`
  * `merkury_confidence_score`

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 説明|変数|
|---| ---|
| `sv_cid`|CID|
| `sv_origin`| ドメイン
| `uID`| クライアントID |
| `em`|メールアドレス|
| `eme`|MD5メールハッシュ|
| `emID`| クライアントメールID|
| `base_url` | ベースURL |