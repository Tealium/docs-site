---
title: Taboola Cookie Matching Service タグ構成ガイド
description: この記事では、タグ管理アカウントで Taboola Cookie Matching Service タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/taboola-cookie-matching-service-tag/
---

<blockquote>
このタグを `utag` バージョン 4.50 以降で使用する場合は、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を `true` に構成する必要があります。この構成により、Cookie の同期に訪問 ID を使用できるようになります。詳細については、[utag 4.50 リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および [utag 4.50 以降へのアップグレード時の tealium_visitor_id に関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* デフォルトでは、このタグは Taboola ID をサーバーサイド属性 `taboola_id` に送信しますが、これはカスタマイズできます。
* ファーストパーティドメインをサポートします。
* このタグはセッションごとに 1 回配信されます。

Event Streaming での Cookie マッチングの詳細については、[Event Streaming での永続的 Cookie マッチングについて](https://docs.tealium.com/about-persistent-cookie-matching/)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **Tealium アカウント**
    * Tealium Collect エンドポイントで使用するアカウント。
    * Cookie 同期リクエストを別のアカウントに送信する場合に、この値を構成します。
    * デフォルト：このタグがパブリッシュされているアカウント。
* **Tealium プロファイル**
    * Tealium Collect エンドポイントで使用するプロファイル。
    * 複数のクライアントサイドプロファイルから単一のサーバーサイドプロファイルへデータを送信する場合に、この値を構成します。
    * デフォルト：このタグがパブリッシュされているプロファイル。
* **Tealium Collect エンドポイント**
    * Tealium と Cookie を同期するために使用するエンドポイント。
    * デフォルト値を上書きするには、カスタムドメインを入力します。この値には通常、`collect.yourdomain.com/event` などのファーストパーティドメインを構成します。
    * デフォルト：`collect.tealiumiq.com/event`
* **Taboola ID 属性名**
    * Taboola ID を含むサーバーサイド属性のカスタム名を構成します。
    * デフォルト：`taboola_id`。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`| Tealium アカウント|
|`tealium_profile`| Tealium プロファイル|
|`taboola_id`| Taboola ID|