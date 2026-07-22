---
title: Yahoo! Dot タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでYahoo Dotタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yahoo-dot-tag/
---

## タグのヒント

* マッピングを使用して：
  * 標準の構成値を動的に上書きします
  * E-Commerce拡張の値を動的に上書きします
  * 以下の標準カスタムイベントパラメータの値を構成します：
    * イベントカテゴリー (`ec`)
    * イベントアクション (`ea`)
    * イベントラベル (`el`)
    * イベント値 (`ev`)
    * ゴール値 (`gv`)
* E-Commerce拡張を使用している場合、ゴール値 (`gv`)は注文小計のE-Commerce拡張値で自動的に入力されます。ゴール値に直接値をマップして、E-Commerce拡張値を上書きします。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **プロジェクトID**
  * Yahoo DotコードスニペットからのprojectId値。
* **ピクセルID**
  * Yahoo Dotコードスニペットからの`pixelId`値。
  * 複数のピクセルIDをカンマ区切りのリストで入力することができます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### Yahoo Dot

|変数| 説明|
|---| ---|
|プロジェクトID| (projectId)|
|ピクセルID (pixelId)| [文字列または配列]|
|ユーザーのメール| (userEmail)|
|ユーザーのハッシュ化されたメール| (userHashedEmail)|

### カスタムイベントパラメータ

|変数| 説明|
|---| ---|
|イベントカテゴリ (ec)| [文字列または配列]|
|イベントアクション (ea)| [文字列または配列]|
|イベントラベル (el)| [文字列または配列]|
|イベント値 (ev)| [文字列または配列]|
|ゴール値 (gv) (E-Commerceの注文小計を上書き)| [数値]|
|タイムスタンプ| (timestamp)|
|広告主ID| (advertiser\_id)|

### E-Commerce

|変数| 説明|
|---| ---|
|小計| (order\_subtotal) (\_csubtotalを上書き)|
|製品IDのリスト (product\_id) (\_cprodを上書き)| [配列]|

