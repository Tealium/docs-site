---
title: Flashtalking Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFlashtalking Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/flashtalking-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()および[utag 4.50&#43;へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* 標準の構成値を上書きするためにマッピングを使用します。
* カスタムマッピングはTealiumへのクッキー同期リクエストに含まれます。
* このタグはセッションごとに一度だけ実行され、その実行は`utag_main_flashtalking_cms_&lt;tag UID&gt;`クッキーで制御されます。
* 以下のサーバーサイド属性をTealiumに戻します：
  * `flashtalking_id`

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Flashtalking Key**
  * あなたのFlashtalking Key。
* **Tealium Account**:
  * 任意
  * サーバーサイドリクエストに使用される`tealium_account`を上書きします。
* **Tealium Profile**:
  * 任意
  * サーバーサイドリクエストに使用される`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`key`|  &lt;ul&gt;&lt;li&gt;Flashtalking Key&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
|`tealium_event`|  &lt;ul&gt;&lt;li&gt;Tealium Event&lt;/li&gt;&lt;/ul&gt; |
