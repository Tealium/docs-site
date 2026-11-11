---
title: Yahoo ID Cookie Syncタグ
description: この記事では、Yahoo User ID Cookie Syncタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yahoo-id-cookie-sync-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Yahoo Cookie Syncタグを使用すると、データパートナーはCookieの同期を開始し、パートナーごとに一意の暗号化されたYahoo Cookie ID（AXID）を受信できます。この暗号化されたIDを使用して、Yahoo DataXコネクタ経由でCookieデータを送信できます。このタグは、取り込みのためにAXIDをサーバーサイドへ送信します。

## タグに関するヒント

* このタグは、セッションごとに1回だけトリガーされます。
* このタグは`visitor_id`をYahooへ送信し、対応する`yahoo_id`と`visitor_id`を含むレスポンスをサーバーサイドで受信します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Pixel ID**：Pixel IDを表す数値ID。
* **Partner ID**：各データプロバイダーのYahoo ID。
* **GDPR**：ユーザーがGDPR規制対象地域にいるかどうかを示します。
* **GDPR Consent**：GDPRにおけるユーザーの同意文字列。GDPRパラメータが`True`に構成されている場合は必須です。
* **Tealium Account**：デフォルトでは、現在のTealiumアカウント。
* **Tealium Profile**：デフォルトでは、現在のTealiumプロファイル。
* **Tealium Event**：デフォルトでは`yahoo_cookie_sync`。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| Visitor ID `visitor_id`  | 文字列 |
| Pixel ID `pixel_id`  | 文字列 |
| Partner ID `partner_id`  | 文字列 |
| GDPR `gdpr`  | ブール値 |
| GDPR Consent `gdpr_consent`  | 文字列 |
| Tealium Account `tealium_account`  | 文字列 |
| Tealium Profile `tealium_profile`  | 文字列 |
| Tealium Event `tealium_event`  | 文字列 |