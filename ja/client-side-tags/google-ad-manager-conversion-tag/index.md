---
title: Google Ad Manager コンバージョンタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGoogle Ad Managerコンバージョンタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-ad-manager-conversion-tag/
---
Google Ad Managerは、人々が視聴、プレイ、エンゲージメントを行う新しい方法と場所で、すべてのデジタル広告収益を成長させるための完全なプラットフォームです。

## タグのヒント

Google Ad Manager コンバージョンタグには以下の特徴があります：

* Order IDのためのE-Commerce Extensionをサポートします。
* `Order ID`が構成されていない場合、その値はランダムに生成された数値に構成されます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **アクティビティID (xsp)**：
* **オーダーID (ord)**： 値はオーダーIDまたは、空白のままでマッピングされていない場合はランダムに生成された数値になります。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
| `xsp`| アクティビティID|
| `ord`| オーダーID |
