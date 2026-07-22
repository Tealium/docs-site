---
title: Rubicon Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでRubicon Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rubicon-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* 以下のサーバーサイド属性をTealiumに戻します：
  * `rubicon_vid`

* すべてのパラメータはマッピングを通じて構成可能です。
* GDPRとGDPR Consent変数は、欧州経済領域（EEA）でマッピングする必要があります。
* GDPRは、ユーザーがEEA国にいる場合は`1`に、それ以外の場合は`0`に構成する必要があります。
* GDPR Consentは、Base64でエンコードされた"DaisyBit"同意文字列を含む文字列です。
* GDPRに関する追加の詳細については、[IAB Europe](https://advertisingconsent.eu/)を参照してください。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Rubicon Project Cookie Matching Serviceタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **Tealiumアカウント**
  * EventStreamのアカウント名を指定するvdataエンドポイントのパススルーパラメータ。

* **Tealiumプロファイル**
  * EventStreamのプロファイル名を指定するvdataエンドポイントのパススルーパラメータ。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li></ul> |
|`gdpr`|  <ul><li>GDPR</li></ul> |
|`gdpr_consent`|  <ul><li>GDPR Consent</li></ul> |
