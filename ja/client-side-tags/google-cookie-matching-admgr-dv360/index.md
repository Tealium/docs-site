---
title: Google Ad ManagerとDV360 (Googleがホスト) のGoogle Cookie Matching Service タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGoogle Ad ManagerとDV360 (Googleがホスト) のGoogle Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cookie-matching-admgr-dv360/
---

<blockquote>
このタグを `utag` バージョン4.50以降で使用する場合、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) を `true` に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50 リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) および [utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-) を参照してください。
</blockquote>


GoogleのCookie Matching Serviceは、訪問を識別する第一者クッキーと、Googleのユーザーを識別するdoubleclick.netクッキーを関連付けることをバイヤーに可能にします。このGoogleがホストするマッチタグは、Tealium Visitor ID、またはクライアントが指定した識別子をGoogleに送信し、マッチングを行います。この識別子は、Ad ManagerとDV360コネクタで使用することができます。

## タグのヒント

* クッキーホストマッチングにアクセスするには、Googleアカウントマネージャーに連絡してアカウントを構成する必要があります。
* `tealium_visitor_id` (md5ハッシュ化)は、マッピングで上書きされない限り、`google_hm`としてGoogleに自動的に送信されます（どちらもbase64でエンコードされます）。
* このタグで送信される識別子属性は、DV360/Ad ManagerコネクタのPartner Provided IDにマッピングする必要があります。

## タグの構成

新しいタグを追加するために、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **ネットワークID**：Googleが提供するネットワークまたはバイヤーID。

### ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

### データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

#### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `google_nid` | Google Network ID (文字列) |
| `google_hm`  | Google Hosted Match Data (文字列) |
| `process_consent` | IABサポート付きの同意管理プラットフォームを使用していない場合、エンドユーザーが同意を与えたことを示すために、この変数に `T` をマップします。 |
