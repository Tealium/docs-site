---
title: LiveRamp Match Partner タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで LiveRamp Match Partner タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/liveramp-match-partner-tag/
---
## タグのヒント

* Email タグタイプに必要なパラメーター:
  * タグ ID
  * Email（マッピングされた）
* Customer ID タグタイプに必要なパラメーター:
  * タグ ID
  * アカウント ID
  * Customer ID（E-Commerce 拡張機能またはマッピングされた）
* マッピングを使用して:
  * 標準構成値を動的に上書きします。
  * Email の値を渡します。
  * Customer ID の E-Commerce 拡張機能値を動的に上書きします。
* Email の値に `@` 記号が含まれている場合、メールアドレスはすべて小文字に変換され、すべての空白が削除され、SHA-1 を使用してハッシュ化されます。
* 次の E-Commerce 拡張機能値をサポート:
  * Customer ID
* E-Commerce 拡張機能を使用しており、Customer ID を使用するように構成されている場合、このタグの Customer ID にデータマッピングは必要ありません。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します:

* **タグタイプ**: タグタイプを選択します: **Email** または **Customer ID**。
* **タグ ID**: あなたの LiveRamp タグ ID。
* **アカウント ID**: あなたの LiveRamp アカウント ID（**Customer ID** タグタイプのみ）。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです:

### Email タグ

| 変数    | 説明  |
|:--------|:------|
| `email` | Email |

### Customer ID タグ

| 変数          | 説明        |
|:--------------|:------------|
| `customer_id` | Customer ID |
