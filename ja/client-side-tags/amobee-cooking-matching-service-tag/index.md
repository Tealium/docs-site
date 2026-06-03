---
title: Amobeeクッキーマッチングサービスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAmobee Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amobee-cooking-matching-service-tag/
---
## タグのヒント

* 以下のサーバーサイド属性をTealiumに戻します：
  * `amobee_id`
* 空白の場合、Tealiumのアカウント名とプロファイル名が自動的に入力されます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* Amobeeトークン（あなたのAmobeeトークン）
* Tealiumアカウント：
* Tealiumプロファイル

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`amobee_token`|  &lt;ul&gt;&lt;li&gt;Amobeeトークン&lt;/li&gt;&lt;li&gt;Amobeeから提供されるあなたのAmobeeトークン。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント名&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル名&lt;/li&gt;&lt;/ul&gt; |
