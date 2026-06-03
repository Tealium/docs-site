---
title: intelliAd Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでintelliAd Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intelliad-cookie-matching-service-tag/
---
intelliAd Cookie Matching Serviceは、Tealium Visitor IDとintelliAd User IDを関連付けます。

 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* このタグは、Tealium Visit Sessionごとに一度だけ発火します。
* 次のサーバーサイド属性をTealiumに戻します：
  * `intelliad_uid`
* 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Tealium Account**
  * 任意。
  * サーバーサイドリクエスト用の`tealium_account`を上書きします。
* **Tealium Profile**:
  * 任意。
  * サーバーサイドリクエスト用の`tealium_profile`を上書きします。
* **Data Layerに保存**
  * ユーザーのintelliAd IDを現在のウェブページのデータレイヤーオブジェクトの`intelliad_uid`として保存します。
* **Tealiumに送信（サーバーサイド）**
  * `intelliad_uid` intelliAd IDをサーバーサイド属性として利用可能にします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
|`store_in_datalayer`|  &lt;ul&gt;&lt;li&gt;Data Layerに保存&lt;/li&gt;&lt;li&gt;値は**yes**または**no**。&lt;/li&gt;&lt;/ul&gt; |
|`send_to_tealium`|  &lt;ul&gt;&lt;li&gt;Tealiumに送信&lt;/li&gt;&lt;li&gt;値は**yes**または**no**。&lt;/li&gt;&lt;/ul&gt; |

