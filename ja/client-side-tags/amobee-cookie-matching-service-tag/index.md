---
title: Amobee Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAmobee Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amobee-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* 以下のサーバーサイド属性をTealiumに送信します：
  * `amobee_id`
* 空白の場合、Tealiumのアカウント名とプロファイル名が自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* Amobeeトークン（あなたのAmobeeトークン）
* Tealiumアカウント：
* Tealiumプロファイル

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`amobee_token`|  &lt;ul&gt;&lt;li&gt;Amobeeトークン&lt;/li&gt;&lt;li&gt;Amobeeから提供されるあなたのAmobeeトークン。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント名&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル名&lt;/li&gt;&lt;/ul&gt; |
