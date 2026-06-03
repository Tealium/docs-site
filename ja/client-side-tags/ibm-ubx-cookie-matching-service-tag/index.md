---
title: IBM UBX Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでIBM UBX Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/ibm-ubx-cookie-matching-service-tag/
---
IBM UBX Cookie Matching Serviceは、Tealiumの訪問を識別するクッキーとIBM UBXの訪問を識別するクッキーを関連付けます。

 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* このタグは、IBM UBX Visitor IDが見つかったときにTealium Visit Sessionごとに一度だけ発火します。
* 次のサーバーサイド属性をTealiumに戻します：
  * `ibm_ima_uid`
* 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグの概要]()の記事を読んでください。

タグを追加するときに、次の構成を行います：

* **Tealium Account**:
  * 任意。
  * サーバーサイドリクエスト用の`tealium_account`を上書きします。
* **Tealium Profile**
  * 任意。
  * サーバーサイドリクエスト用の`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile。&lt;/li&gt;&lt;/ul&gt; |

