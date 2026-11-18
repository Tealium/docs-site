---
title: Adobe Advertising Cookie Syncタグ構成ガイド
description: この記事では、タグ管理アカウントでAdobe Advertising Cookie Syncタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-advertising-cookie-sync-tag/
--- 

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に必要な訪問IDを確実に利用できます。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Adobe Advertising Cookie Syncは、オーディエンスの同期とアクティベーションのために、Adobe Advertising Cookie IDをTealium訪問IDに関連付けます。

## タグに関するヒント

* このタグはTealiumの訪問セッションごとに1回発火し、Tealium訪問IDが利用可能になるまで待機します。
* 次の属性をTealiumに送り返します。
  * `adobe_advertising_user_id`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealiumアカウント**：Tealiumアカウント名です。デフォルトでは、Tealium iQアカウントが使用されます。
* **Tealiumプロファイル**：Tealiumプロファイル名です。デフォルトでは、Tealium iQプロファイルが使用されます。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングとは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 構成

タグ構成で構成された値を上書きする宛先を選択します。

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `tealium_account` | 文字列 | タグ構成で構成されたTealiumアカウントを上書きします。 |
| `tealium_profile` | 文字列 | タグ構成で構成されたTealiumプロファイルを上書きします。 |
