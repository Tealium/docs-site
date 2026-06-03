---
title: Sizmek Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSizmek Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sizmek-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## 仕組み

Sizmek Cookie Matching Serviceは、Tealiumの訪問を識別するクッキーとSizmekのユーザーを識別するクッキーを関連付けることができます。

## タグのヒント

* このタグはTealium Visit Sessionごとに一度だけ発火します。
* 空白の場合、Tealiumアカウントとプロファイルは自動的に入力されます。
* 以下のサーバーサイド属性をTealiumに戻します：
  * `sizmek_id`

## タグの構成

まず、Tealiumのタグマーケットプレイスに行き、Sizmek Cookie Matching Serviceタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Sizmek UUID**
  * 必須。
  * Sizmekから提供されるユニークID。

* **Tealiumアカウント**
  * 必須。
  * あなたのTealiumアカウント名。

* **Tealiumプロファイル**
  * 必須。
  * あなたのTealiumプロファイル名。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`sizmek_uuid`| Sizmek ID|
|`tealium_account`| Tealiumアカウント名|
|`tealium_profile`| Tealiumプロファイル名|
