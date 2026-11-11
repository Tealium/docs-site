---
title: Google Ad Manager および DV360 向け Google Cookie Matching Service（Tealium ホスト型）タグ構成ガイド
description: この記事では、タグ管理アカウントで Google Ad Manager および DV360 向け Google Cookie Matching Service（Tealium ホスト型）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-cookie-matching-service/
---

<blockquote>
このタグを `utag` バージョン4.50以降で使用する場合は、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を `true` に構成する必要があります。この構成により、Cookie の同期に訪問 ID を使用できるようになります。詳細については、[utag 4.50のリリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および [utag 4.50以降へアップグレードする際の tealium_visitor_id に関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Google の Cookie Matching Service を使用すると、購入者は、Tealium の訪問を識別する Cookie と、Google でユーザーを識別する doubleclick.net Cookie を関連付けることができます。Tealium ホスト型タグを使用すると、クライアントは Google Cookie の値を顧客データプラットフォーム（CDP）に保持し、関連するコネクタで使用できます。

## タグに関するヒント

* マッピングを使用して標準構成を上書きします。
* 空白のままにすると、Tealium アカウントと Tealium プロファイルが自動的に入力されます。
* 許可されている地域では、このタグはサーバーサイド属性 `google_gid` を Tealium に送り返します。
* [同意管理](https://docs.tealium.com/about-consent-management/)または CMP 連携を使用し、訪問が広告または同等のカテゴリーについて同意した場合にのみタグが実行されるようにします。
* 同意を取得した場合にのみ、`process_consent` を値 `T` にマッピングします。
* IAB の透明性と同意に関するフレームワーク（TCF）に準拠しておらず、`process_consent` をマッピングする場合は、`gdpr` と `gdpr_consent` を省略する必要があります。これらのパラメータが存在すると、Google は `process_consent` を無視します。詳細については、[Google：マッチタグの URL パラメータ](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters)を参照してください。

詳細については、[Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide) のドキュメントを参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **ネットワーク ID**：サーバーサイドリクエストで `google_gid` を渡すには `tealium_dmp` を使用し、その他のソリューションでは Google から提供されたネットワーク ID または購入者 ID を使用します。
* **Tealium アカウント**：Tealium アカウント。
* **Tealium プロファイル**：Tealium プロファイル。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
| --- | --- |
| `google_nid` | ネットワーク ID または購入者 ID。 |
| `tealium_trace_id`| トレース ID。 |
| `tealium_selector`| Tealium セレクター。 |
| `tealium_account` | Tealium アカウント。 |
| `tealium_profile` | Tealium プロファイル。 |
| `process_consent` | エンドユーザーから同意を取得したことを示します。エンドユーザーが同意した場合は `T` にマッピングします。IAB の透明性と同意に関するフレームワーク（TCF）に準拠していない場合は、`gdpr` または `gdpr_consent` を含めないでください。これらのパラメータが存在すると、Google は `process_consent` を無視します。詳細については、[Google：マッチタグの URL パラメータ](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters)を参照してください。 |