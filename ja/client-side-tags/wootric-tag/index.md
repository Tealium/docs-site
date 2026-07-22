---
title: Wootricタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでWootricタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/wootric-tag/
---Wootricは、NPSから最大の利益を得るための支援をします—顧客のロイヤルティを測定し、製品を最適化し、顧客を維持し、ブランドの支持者の軍団を構築します。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **アカウントトークン**：あなたのアカウントを識別する一意のID。Wootricから提供されます。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Wootricタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリーは次のとおりです：

### 標準

|**宛先名**| **説明**|
|---| ---|
|Email (email)| 現在ログインしているユーザーのメールアドレス|
|User ID (external\_id)| 現在ログインしているユーザーのカスタムID|
|Created At (created\_at)| 現在ログインしているユーザーのサインアップ日。10桁のUNIXタイムスタンプ（秒）である必要があります|
|Product Name (product\_name)| トラッキングされている製品またはサービスの名前|
|Account Token (account\_token)| あなたのアカウントの一意のID。タグ構成のデフォルトを上書きするために使用します|

## ベンダードキュメンテーション

* [Wootric Docs](http://docs.wootric.com/)
* [Knowledge Base](http://help.wootric.com/help_center)

