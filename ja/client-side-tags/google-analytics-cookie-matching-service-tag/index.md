---
title: Google Analytics Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGoogle Analytics Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-analytics-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Google Analytics Cookie Matching Serviceタグを使用すると、訪問をデフォルトのGoogleクライアントIDクッキー(`_ga`)またはTealium訪問IDに関連付けることができます。

## タグのヒント

* **詳細構成**の下で、**バンドルフラグ**を**はい**に、**待機フラグ**を**いいえ**に構成します。
* このタグをTealium Collectタグより上に移動します。[Load Order Manager](https://docs.tealium.com/load-order-manager/)を参照してください。
* 詳細については、[Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide)のドキュメンテーションを参照してください。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

