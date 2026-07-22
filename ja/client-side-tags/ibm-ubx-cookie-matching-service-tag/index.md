---
title: IBM UBX Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでIBM UBX Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/ibm-ubx-cookie-matching-service-tag/
---
IBM UBX Cookie Matching Serviceは、Tealiumの訪問を識別するクッキーとIBM UBXの訪問を識別するクッキーを関連付けます。


<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* このタグは、IBM UBX Visitor IDが見つかったときにTealium Visit Sessionごとに一度だけ発火します。
* 次のサーバーサイド属性をTealiumに戻します：
  * `ibm_ima_uid`
* 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加するときに、次の構成を行います：

* **Tealium Account**:
  * 任意。
  * サーバーサイドリクエスト用の`tealium_account`を上書きします。
* **Tealium Profile**
  * 任意。
  * サーバーサイドリクエスト用の`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account。</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile。</li></ul> |

