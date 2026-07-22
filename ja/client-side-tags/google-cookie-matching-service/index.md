---
title: Google Ad Manager および DV360 (Tealiumホスト) タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Google Ad Manager および DV360 (Tealiumホスト) タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cookie-matching-service/
---

<blockquote>
このタグを `utag` バージョン 4.50 以降で使用する場合、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) を `true` に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50 リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および [utag 4.50+ へのアップグレード時の tealium_visitor_id の考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-) を参照してください。
</blockquote>


GoogleのCookie Matching Serviceは、Tealiumの訪問を識別するクッキーと、Googleのユーザーを識別するdoubleclick.netクッキーを購入者が関連付けることを可能にします。Tealiumホストのタグは、関連するコネクタで使用するためにGoogleクッキー値をAudienceStreamに保持することをクライアントに許可します。

## タグのヒント

* 標準構成を上書きするためにマッピングを使用します。
* 空白の場合、TealiumアカウントとTealiumプロファイルは自動的に入力されます。
* 許可された地域では、このタグはサーバーサイド属性 `google_gid` をTealiumに戻します。
* [同意管理](https://docs.tealium.com/about-consent-management/)またはCMP統合を使用して、訪問が広告または同等のカテゴリに同意した場合にのみタグが実行されるようにします。
* 同意が得られた場合にのみ、`process_consent` を値 `T` にマップします。
* IABの透明性と同意フレームワーク（TCF）に従わない場合、`process_consent` をマッピングする場合は `gdpr` と `gdpr_consent` を省略する必要があります。Googleはこれらのパラメータが存在する場合 `process_consent` を無視します。詳細については、[Google: Match Tag URL Parameters](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters) を参照してください。

詳細については、[Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide) のドキュメントを参照してください。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、次の構成を構成します：

* **ネットワークID**: `tealium_dmp` を使用してサーバーサイドリクエストで `google_gid` を渡すか、他のソリューション用にGoogleが提供するネットワークIDまたはバイヤーIDを使用します。
* **Tealiumアカウント**: あなたのTealiumアカウント。
* **Tealiumプロファイル**: あなたのTealiumプロファイル。

## 読み込みルール

すべてのページでタグを読み込むか、タグが読み込まれる条件を構成します。読み込みルールについての詳細は、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。変数をタグの宛先にマッピングする方法についての説明は、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
| --- | --- |
| `google_nid` | ネットワークまたはバイヤーID。 |
| `tealium_trace_id`| トレースID。  |
| `tealium_selector`| Tealiumセレクタ。  |
| `tealium_account` | Tealiumアカウント。 |
| `tealium_profile` | Tealiumプロファイル。  |
| `process_consent` | 最終ユーザーから同意が得られたことを示します。最終ユーザーが同意を与えた場合は `T` にマップします。IABの透明性と同意フレームワーク（TCF）に従わない場合は、Googleが `process_consent` を無視するため、`gdpr` や `gdpr_consent` を含めないでください。詳細については、[Google: Match Tag URL Parameters](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters) を参照してください。 |
