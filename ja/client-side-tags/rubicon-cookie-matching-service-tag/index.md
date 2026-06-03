---
title: Rubicon Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでRubicon Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rubicon-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* 以下のサーバーサイド属性をTealiumに戻します：
  * `rubicon_vid`

* すべてのパラメータはマッピングを通じて構成可能です。
* GDPRとGDPR Consent変数は、欧州経済領域（EEA）でマッピングする必要があります。
* GDPRは、ユーザーがEEA国にいる場合は`1`に、それ以外の場合は`0`に構成する必要があります。
* GDPR Consentは、Base64でエンコードされた&#34;DaisyBit&#34;同意文字列を含む文字列です。
* GDPRに関する追加の詳細については、[IAB Europe](https://advertisingconsent.eu/)を参照してください。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Rubicon Project Cookie Matching Serviceタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **Tealiumアカウント**
  * EventStreamのアカウント名を指定するvdataエンドポイントのパススルーパラメータ。

* **Tealiumプロファイル**
  * EventStreamのプロファイル名を指定するvdataエンドポイントのパススルーパラメータ。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル&lt;/li&gt;&lt;/ul&gt; |
|`gdpr`|  &lt;ul&gt;&lt;li&gt;GDPR&lt;/li&gt;&lt;/ul&gt; |
|`gdpr_consent`|  &lt;ul&gt;&lt;li&gt;GDPR Consent&lt;/li&gt;&lt;/ul&gt; |
