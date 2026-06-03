---
title: Schema App タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Schema App タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/schema-app-tag/
---
## タグのヒント

* アカウントIDはアプリケーション内の **Integrations &gt; JavaScript** で見つけることができます。

## タグの構成

タグマーケットプレイスに行って新しいタグを追加します。詳細については、を参照してください。

タグを追加した後、以下の構成を構成します：

* **Account ID**: あなたの Schema App アカウントID。
* **Output Cache**: 出力キャッシュを有効にします。デフォルト値は `False` です。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

|変数| タイプ | 説明|
|---| ---| ---|
| `account_id` | 文字列 | アカウントID。|
| `output_cache` | ブール値 | 出力キャッシュを有効にします。 |
| `base_url` | 文字列 | ベースURL/APIエンドポイント。 |