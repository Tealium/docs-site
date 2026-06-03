---
title: Quicklizardタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuicklizardタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quicklizard-tag/
---
## タグのヒント

* 必要なマッピング：
  * 商品IDのリスト
  * 価格のリスト

* 以下のE-Commerce拡張値をサポート：
  * 注文ID
  * 商品IDのリスト
  * 名前のリスト
  * ブランドのリスト
  * カテゴリのリスト
  * 価格のリスト

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Quicklizardタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **クライアントキー**  
Quicklizardから提供されるキー。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### カスタム

|変数| 説明|
|---| ---|
|カスタム|  &lt;ul&gt;&lt;li&gt;カスタム宛先を追加&lt;/li&gt;&lt;/ul&gt; |
