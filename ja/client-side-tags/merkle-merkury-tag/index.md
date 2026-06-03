---
title: Merkle Merkuryタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMerkle Merkuryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/merkle-merkury-tag/
---
## タグのヒント

* Adobe MediaSDKは、Adobe Experience Cloud ID ServiceとAppMeasurement for JSを最初にロードすることを必要とします。できればバンドルされていることが望ましいです。
* このタグは`utag.track(&#39;video&#39;, data);`を通じて発火されます。これはあなたのビデオイベントハンドラに実装されるべきです。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに行きます。タグを追加する一般的な手順については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **CID**  
Merkuryチームから生成されたクライアント固有の数値アカウント番号。
* **ドメイン**  
クライアントのウェブサイトのドメイン。例：`merkleinc.com`。
* **Merkury Identityイベントの送信**  
`merkury_identity`イベントを生成するかどうか。このイベントには以下の情報が含まれます：
  * `event`
  * `merkury_email_sha256`
  * `merkury_hmid`
  * `merkury_confidence_score`

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 説明|変数|
|---| ---|
| `sv_cid`|CID|
| `sv_origin`| ドメイン |
| `uID`| クライアントID |
| `em`|メールアドレス|
| `eme`|MD5メールハッシュ|
| `emID`| クライアントメールID|
| `base_url` | ベースURL |
