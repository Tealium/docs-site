---
title: Yahoo ID Cookie Syncタグ
description: この記事では、YahooユーザーID Cookie Syncタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yahoo-id-cookie-sync-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがCookie同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Yahoo Cookie Syncタグを使用すると、データパートナーがCookie同期を開始し、各パートナーに対して一意の暗号化されたYahoo Cookie ID（AXID）を受け取ることができます。この暗号化されたIDは、Yahoo DataX Connectorを介してCookieデータを投稿するために使用できます。このタグは、AXIDをサーバーサイドに送信して取り込みます。

## タグのヒント

* このタグは、セッションごとに一度だけトリガーされます。
* このタグは、`visitor_id`をYahooに送信し、`visitor_id`に一致する`yahoo_id`のレスポンスをサーバーサイドに送信します。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **Pixel ID**: Pixel IDを示す数値ID。
* **Partner ID**: 提供されるデータのYahoo識別子。
* **GDPR**: ユーザーがGDPR規制地域からのものかどうかを示します。
* **GDPR Consent**: GDPRユーザー同意文字列。GDPRパラメータが`True`に構成されている場合に必要です。
* **Tealium Account**: デフォルトでは現在のTealiumアカウント。
* **Tealium Profile**: デフォルトでは現在のTealiumプロファイル。
* **Tealium Event**: デフォルトでは`yahoo_cookie_sync`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

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

