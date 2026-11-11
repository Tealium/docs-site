---
title: Google Analytics Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでGoogle Analytics Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-analytics-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50のリリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降にアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Google Analytics Cookie Matching Serviceタグを使用すると、訪問をデフォルトのGoogleクライアントID Cookie（`_ga`）に関連付けることができます。関連付けられない場合は、デフォルトでTealium訪問IDが使用されます。

## タグに関するヒント

* **Advanced Settings**で、**Bundle Flag**が**Yes**に、**Wait Flag**が**No**に構成されていることを確認します。
* [Load Order Manager]](https://docs.tealium.com/load-order-manager/)で、このタグをTealium Collectタグより上に移動します。
* 詳細については、[Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide)のドキュメントを参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。