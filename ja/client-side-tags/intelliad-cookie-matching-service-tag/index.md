---
title: intelliAd Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでintelliAd Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intelliad-cookie-matching-service-tag/
---
intelliAd Cookie Matching Serviceは、Tealium Visitor IDとintelliAd User IDを関連付けます。


<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* このタグは、Tealium Visit Sessionごとに一度だけ発火します。
* 次のサーバーサイド属性をTealiumに戻します：
  * `intelliad_uid`
* 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

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

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
|`store_in_datalayer`|  <ul><li>Data Layerに保存</li><li>値は**yes**または**no**。</li></ul> |
|`send_to_tealium`|  <ul><li>Tealiumに送信</li><li>値は**yes**または**no**。</li></ul> |

