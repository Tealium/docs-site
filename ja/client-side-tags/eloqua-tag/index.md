---
title: Eloqua タグ構成ガイド
description: この記事では、Eloquaタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/eloqua-tag/
---
## タグのヒント

* デフォルト構成の **Wait = Yes** を保持して、Eloqua JavaScript (JS) ファイルがDOM Readyで実行されるようにします。
* フォーム追跡のために、以下のパラメーターに値を構成するためのマッピングを使用します：
  * `form_tracking`（オン）
  * `elqFormName`
  * `elqFormGUIDElement`

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Site ID**: あなたのサイトID番号。
* **First-Party Cookie Domain Name**: ファーストパーティクッキーのドメイン名。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `form_tracking` | フォーム追跡。 |
| `elqFormName` | フォーム名。 |
| `elqFormGUIDElement` | フォーム要素。 |
| `base_url` | JavaScriptファイルのURL。 |
| `elqDomainName` | ファーストパーティクッキーのドメイン名。 |
| `page_url` | ページURL。 |