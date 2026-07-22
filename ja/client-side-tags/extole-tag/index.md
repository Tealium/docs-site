---
title: Extoleタグ構成ガイド
description: この記事では、Extoleタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/extole-tag/
---
Extoleのプラットフォームは、世界最大のブランドのためのエンリッチされた、クロスチャネルの紹介プログラムを提供します。大規模な友人紹介をマーケティング、測定、最適化するすべての機能を備えたExtoleプラットフォームは、マーケターが既存の顧客がブランドに対して持っている愛情を新たな顧客に変えるのを助けます。

## タグのヒント

* CTAが配置される場所を識別するための方法を選択します。
  * **要素ID**の場合：ハッシュ (`#`) 文字なしで要素IDを提供します。
  * **HTML要素**の場合：クエリするための要素セレクタを提供します。このオプションは、ページ上でjQueryをロードする必要があります。
* イベントマッピングを使用して登録イベントをトリガーします。注文IDが検出されると、コンバージョンイベントは自動的に発火します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアント名**：あなたのユニークなExtoleクライアント名。
* **ターゲットコンテンツ方法**：CTA配置を識別するために使用される方法を選択します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `client_name` | クライアント名  |
| `registration.custom` | 登録カスタムデータ  |
| `conversion.custom` | コンバージョンカスタムデータ  | 


<blockquote>
`custom`をあなたの変数名に置き換えてください、例えば`registration.date`。
</blockquote>


### E-コマース

Extoleタグはeコマース対応しているため、デフォルトのE-Commerce Extensionマッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、以下の場合は必要です：

* Extensionマッピングを上書きしたい場合。
* あなたのユースケースに必要なeコマース変数がextensionに存在しない場合。

| 変数 | 説明 |
|:---------|:------------|
| `order_id` (`_corder`を上書き) |注文ID  |
| `order_total` (`_ctotal`を上書き) | 注文合計  |
| `customer_id` (`_ccustid`を上書き) | 顧客ID  |
| `cart_value` (`_ctotal`を上書き) | カートの価値  | 
| `coupon_code` (`_cpromo`を上書き) | クーポンコード  | 

### Calls-To-Action

| 変数 | 説明 |
|:---------|:------------|
|  `email` | メール  |
|  `first_name` | 名前  |
|  `last_name` | 姓  |
|  `locale` | ロケール  |
|  `cta.global_header.id` | グローバルヘッダー  |
|  `cta.global_footer.id` | グローバルフッター  |
|  `cta.product.id` | 商品  |
|  `cta.product.data.content.custom` | 商品カスタムデータ  |
|  `cta.confirmation.id` | 確認  |
|  `cta.referral_page.id` | 紹介ページ  |
|  `cta.my_account.id` | アカウントページ  |
|  `cta.custom.id` | カスタムCTA名 |
|  `cta.CTAname.data.first_name` | CTA名を追加  |
|  `cta.CTAname.data.last_name` | CTA姓を追加  |
|  `cta.CTAname.data.partner_user_id` | CTAパートナーユーザーIDを追加  |
|  `cta.CTAname.data.email` | CTAメールを追加  |
|  `cta.CTAname.data.locale` | CTAロケールを追加  |
|  `cta.CTAname.data.custom` | CTAカスタムデータを追加  |
|  `cta.overlay` | オーバーレイ  |
|  `cta.mobile_menu` | モバイルメニュー  |


<blockquote>
要素IDまたはセレクタをマッピングしていない場合、文字列`n/a`をマッピングします。
</blockquote>


#### スタンダードCTA名

|**CTA名**| **値**|
|---| ---|
|グローバルヘッダー | `global_header` |
|グローバルフッター | `global_footer` |
|確認 | `confirmation` |
|紹介ページ | `referral_page` |
|アカウントページ | `my_account` |

紹介CTAの日付を送信したい場合は、**紹介ページ**宛先にマッピングします。次に、**CTAカスタムデータを追加**宛先に次のようにマッピングします：`cta.referral_page.data.date`。

### イベントトリガー

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

ページ上で特定のイベントをトリガーするために、以下の宛先にマッピングします。イベントをトリガーするには：

1. **トリガー**ドロップダウンからイベントを選択します。
1. **マッピング値**フィールドに、マッピングする変数の値を入力します。
1. **追加**をクリックします。

| 変数 | 説明 |
|:---------|:------------|
| 登録 | 登録イベントを発火します。 |
| コンバージョン | コンバージョンイベントを発火します。 |
| 確認 | 要素IDなしで確認イベントを発火します。 |

## ベンダー文書

[Extole Asyc文書](https://dev.extole.com/docs/tealium)

