---
title: Google Ad ManagerおよびDV360向けGoogle Cookie Matching Service（Googleホスト型）タグ構成ガイド
description: この記事では、タグ管理アカウントでGoogle Ad ManagerおよびDV360向けGoogle Cookie Matching Service（Googleホスト型）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cookie-matching-admgr-dv360/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


GoogleのCookie Matching Serviceを使用すると、購入者は、訪問を識別するファーストパーティCookieと、Googleでユーザーを識別するdoubleclick.net Cookieを関連付けることができます。このGoogleホスト型マッチタグは、照合のためにTealium訪問ID、またはクライアントが指定した識別子をGoogleへ送信します。この識別子は、その後Ad ManagerおよびDV360コネクタで使用できます。

## タグに関するヒント

* ホスト型Cookieマッチングを利用するには、Googleアカウントマネージャーに連絡してアカウントを構成する必要があります。
* マッピングで上書きしない限り、`tealium_visitor_id`（MD5ハッシュ化済み）は、ホスト型マッチング用の`google_hm`としてGoogleへ自動的に送信されます（どちらもBase64でエンコードされます）。
* このタグで送信する識別子属性は、DV360／Ad ManagerコネクタのPartner Provided IDにマッピングする必要があります。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **ネットワークID**：Googleから提供されたNetwork IDまたはBuyer ID。

### ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

### データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数へ送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

#### 標準

| 変数 | 説明 |
|:---------|:------------|
| `google_nid` | GoogleネットワークID（文字列） |
| `google_hm`  | Googleホスト型マッチデータ（文字列） |
| `process_consent` | IAB対応の同意管理プラットフォームを使用していない場合、エンドユーザーが同意したことを示すために、この変数へ`T`をマッピングします。 |