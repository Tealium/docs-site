---
title: Rubicon Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでRubicon Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rubicon-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* 次のサーバーサイド属性をTealiumに返します。
  * `rubicon_vid`

* すべてのパラメータはマッピングで構成できます。
* 欧州経済領域（EEA）では、GDPR変数とGDPR Consent変数をマッピングする必要があります。
* ユーザーがEEA加盟国にいる場合はGDPRを`1`に、それ以外の場合は`0`に構成する必要があります。
* GDPR Consentは、Base64でエンコードされた「DaisyBit」同意文字列を含む文字列です。
* GDPRの詳細については、[IAB Europe](https://advertisingconsent.eu/)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealiumアカウント**
  * Event Streamingのアカウント名を指定する、vdataエンドポイントのパススルーパラメータです。

* **Tealiumプロファイル**
  * Event Streamingのプロファイル名を指定する、vdataエンドポイントのパススルーパラメータです。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li></ul> |
|`gdpr`|  <ul><li>GDPR</li></ul> |
|`gdpr_consent`|  <ul><li>GDPR Consent</li></ul> |