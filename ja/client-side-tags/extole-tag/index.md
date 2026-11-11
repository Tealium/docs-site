---
title: Extoleタグ構成ガイド
description: この記事では、Extoleタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/extole-tag/
---
Extoleのプラットフォームは、世界最大級のブランド向けに、豊富な機能を備えたクロスチャネルの紹介プログラムを提供します。大規模な友人紹介施策のマーケティング、測定、最適化に必要な機能をすべて備えたExtoleプラットフォームにより、マーケターは既存顧客のブランドへの愛着を新規顧客の獲得につなげることができます。

## タグに関するヒント

* CTAの配置場所を識別するために使用する方法を選択します。
  * **Element ID**の場合：ハッシュ（`#`）文字を付けずに要素IDを指定します。
  * **HTML Element**の場合：クエリ対象の要素セレクターを指定します。このオプションを使用するには、ページ上でjQueryを読み込む必要があります。
* イベントマッピングを使用して、登録イベントをトリガーします。注文IDが検出されると、コンバージョンイベントが自動的に発生します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **Client Name**：一意のExtoleクライアント名。
* **Target Content Method**：CTAの配置を識別するために使用する方法を選択します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `client_name` | クライアント名 |
| `registration.custom` | 登録カスタムデータ |
| `conversion.custom` | コンバージョンカスタムデータ |


<blockquote>
`custom`を使用する変数名（例：`registration.date`）に置き換えてください。
</blockquote>


### Eコマース

ExtoleタグではEコマースが有効になっているため、デフォルトのEコマース拡張機能のマッピングが自動的に使用されます。通常、次の場合を除き、このカテゴリーで手動マッピングを行う必要はありません。

* 拡張機能のマッピングを上書きする場合。
* ユースケースに必要なEコマース変数が拡張機能で使用できない場合。

| 変数 | 説明 |
|:---------|:------------|
| `order_id`（`_corder`を上書き） | 注文ID |
| `order_total`（`_ctotal`を上書き） | 注文合計 |
| `customer_id`（`_ccustid`を上書き） | 顧客ID |
| `cart_value`（`_ctotal`を上書き） | カートの値 |
| `coupon_code`（`_cpromo`を上書き） | クーポンコード |

### CTA

| 変数 | 説明 |
|:---------|:------------|
| `email` | メールアドレス |
| `first_name` | 名 |
| `last_name` | 姓 |
| `locale` | ロケール |
| `cta.global_header.id` | グローバルヘッダー |
| `cta.global_footer.id` | グローバルフッター |
| `cta.product.id` | 製品 |
| `cta.product.data.content.custom` | 製品カスタムデータ |
| `cta.confirmation.id` | 確認 |
| `cta.referral_page.id` | 紹介ページ |
| `cta.my_account.id` | アカウントページ |
| `cta.custom.id` | カスタムCTA名 |
| `cta.CTAname.data.first_name` | CTAの名を追加 |
| `cta.CTAname.data.last_name` | CTAの姓を追加 |
| `cta.CTAname.data.partner_user_id` | CTAのパートナーユーザーIDを追加 |
| `cta.CTAname.data.email` | CTAのメールアドレスを追加 |
| `cta.CTAname.data.locale` | CTAのロケールを追加 |
| `cta.CTAname.data.custom` | CTAのカスタムデータを追加 |
| `cta.overlay` | オーバーレイ |
| `cta.mobile_menu` | モバイルメニュー |


<blockquote>
要素IDまたはセレクターをマッピングしない場合は、文字列`n/a`をマッピングしてください。
</blockquote>


#### 標準CTA名

|**CTA名**| **値**|
|---| ---|
|グローバルヘッダー | `global_header` |
|グローバルフッター | `global_footer` |
|確認 | `confirmation` |
|紹介ページ | `referral_page` |
|アカウントページ | `my_account` |

紹介CTAの日付を送信する場合は、**Referral Page**の送信先にマッピングします。次に、**Add CTA custom data**の送信先に`cta.referral_page.data.date`としてマッピングします。

### イベントトリガー

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

ページ上で特定のイベントをトリガーするには、以下の送信先にマッピングします。イベントをトリガーするには、次の手順を実行します。

1. **Trigger**ドロップダウンからイベントを選択します。
1. **Mapped Value**フィールドに、マッピングする変数の値を入力します。
1. **Add**をクリックします。

| 変数 | 説明 |
|:---------|:------------|
| Registration | 登録イベントを発生させます。 |
| Conversion | コンバージョンイベントを発生させます。 |
| Confirmation | 要素IDなしで確認イベントを発生させます。 |

## ベンダーのドキュメント

[Extole Asycドキュメント](https://dev.extole.com/docs/tealium)