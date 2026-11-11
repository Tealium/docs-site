---
title: The Trade Desk Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでThe Trade Desk Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/the-trade-desk-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期にビジターIDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## 要件

* タグ管理
* 顧客データプラットフォーム（CDP）

## 仕組み

The Trade Desk Cookie Matching Serviceタグは、`ttd_uuid`という名前の新しい変数を構成します。この変数は、セッションCookieおよび標準のデータレイヤー変数として保存されます。デフォルトでは、タグはセッションごとに一度だけトリガーされます。

The Trade Desk Cookie Matching Serviceタグは、The Trade Deskサーバーと通信して、現在のユーザーの識別子をリクエストします。この値がタグに返されると、同期されたユーザーIDを含むビジター属性への入力に使用できるよう、CDPに渡されます。この属性は、The Trade Deskコネクタアクションで「Trade Desk ID (TDID)」へのマッピングとして使用できます。

## データレイヤー変数

タグを追加する前に、次のデータレイヤー変数を作成します。

* `ttd_uuid`：UDO変数
* `utag_main_ttd_uuid`：ファーストパーティCookie

これらの変数は、Cookie Matchingタグによって自動的に構成されます。

![](https://docs.tealium.com/images/client-side-tags/the-trade-desk-cookie.png)

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を構成します。

* **Tealiumアカウント**：The Trade DeskのユーザーIDを別のアカウントに送信する場合を除き、空白のままにします。
* **Tealiumプロファイル**：The Trade DeskのユーザーIDを別のプロファイルに送信する場合を除き、空白のままにします。

### ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを決定します。

このタグは、Cookieの照合がまだ行われていない場合にのみ実行する必要があります。次のようなロードルール条件で、Cookie変数`utag_main_ttd_uuid`を使用して判定できます。

`utag_main_ttd_uuid`が定義されていない

このタグには、Cookieが定義されていない場合にのみ発火するロジックも組み込まれています。ただし、ロードルールを使用すると、現在のセッションですでに実行済みの場合に、そのページでタグが読み込まれないようにできます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

|**宛先名**| **タイプ** | **説明**|
|---| ---| ---|
|`tealium_account`| 文字列 | ユーザーIDの同期先となるTealiumアカウント。デフォルトは現在のアカウントです。 |
|`tealium_profile`| 文字列 | ユーザーIDの同期先となるTealiumプロファイル。デフォルトは現在のプロファイルです。 |
|`gdpr`| ブール値 | 現在のユーザーが欧州連合（EU）に居住し、GDPRの対象であるかどうかを示す値を渡します。<ul><li>ユーザーがGDPRの対象でない場合は、`0`（デフォルト）に構成します。<br>ユーザーがGDPRの対象である場合は、`1`に構成します。</li><li>この値を`0`に構成し、ビジターがEUに所在する場合、Cookie Sync Serviceは空の配列を返します。</li></ul> |
|`gdpr_consent_string`| 文字列 | Base64 URLエンコードされたGDPR同意文字列。|
| `domain` | 文字列 | Cookieの同期を開始するドメイン。<br>注：このドメインをThe Trade Desk構成の**許可リスト**に追加する必要があります。 |
|`order_id`| 文字列 | `_corder` Eコマース拡張機能の値を上書きします。|

## CDPの構成

変更を保存して本番環境にパブリッシュすると、新しい変数がCDPで使用できるようになります。`ttd_uuid`変数はイベント属性として表示されますが、The Trade Deskコネクタアクションで使用するには、ビジター属性として作成する必要があります。

`ttd_uuid`値を保存するビジター属性を追加するには、次の手順を実行します。

1. **変換 > ビジター／訪問属性**に移動します。
1. **属性を追加**をクリックし、スコープに**ビジター**、データタイプに**文字列**を選択します。
1. 名前として`Trade Desk User ID`を入力します。
1. **エンリッチメントを追加**をクリックし、**文字列を構成**を選択します。
1. **文字列の構成先**ドロップダウンメニューから`ttd_uuid`を選択します。
1. **完了**をクリックします。

これで、Trade Desk User IDが構成されているビジターのオーディエンスを作成できます。これらのオーディエンスは、The Trade Deskのコネクタアクションで使用されます。The Trade Deskのコネクタアクションで、この属性を「Trade Desk ID (TDID)」パラメータにマッピングします。