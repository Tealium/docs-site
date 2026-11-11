---
title: Yahoo! JAPAN サイトジェネラルタグ構成ガイド
description: この記事では、タグ管理アカウントで Yahoo! JAPAN サイトジェネラルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yahoo-japan-site-general-tag/
---

## タグに関するヒント

* **重要:** 特定のタグをトリガーするには、マッピングツールボックスの **Tag Types** タブでトリガー条件を構成します。構成しない場合、タグはトリガーされません。
* 標準構成を上書きするには、マッピングを使用します。
* ID またはラベルは、カンマ区切りのリストとして複数入力できます。1 つの ID と複数のラベルを入力すると、同じ ID を使用して、ラベルごとに 1 回ずつ呼び出しがトリガーされます。複数の ID と 1 つのラベルを入力すると、同じラベルを使用して、ID ごとに 1 回ずつ呼び出しがトリガーされます。1 つのタグタイプに対して複数の ID とラベルを入力する場合は、ID とラベルの数が一致していることを確認してください。
* 次の E コマース拡張値をサポートしています。
  * 注文 ID（`_corder`）
  * 注文小計（`_csubtotal`）
  * 商品 ID のリスト（`_cprod`）
  * 商品カテゴリーのリスト（`_ccat`）
  * 商品数量のリスト（`_cquan`）
  * 商品価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **Auto Tagging**: 自動タグ付けを有効または無効にします。この構成を有効にすると、タグの読み込み後に `ytag({"type":"ycl_cookie"});` が呼び出されます。
* **Display Network Conversion IO**: Yahoo! JAPAN ディスプレイ広告（YDN）のコンバージョン IO を入力します。
* **Display Network Conversion Label**: Yahoo! JAPAN ディスプレイ広告（YDN）のコンバージョンラベルを入力します。
* **Display Network Retargeting ID**: Yahoo! JAPAN ディスプレイ広告（YDN）のリターゲティング ID を入力します。
* **Display Network Retargeting Label**: Yahoo! JAPAN ディスプレイ広告（YDN）のリターゲティングラベルを入力します。
* **Sponsored Search Conversion ID**: Yahoo! JAPAN 検索広告（YSS）のコンバージョン ID を入力します。
* **Sponsored Search Conversion Label**: Yahoo! JAPAN 検索広告（YSS）のコンバージョンラベルを入力します。
* **Sponsored Search Retargeting ID**: Yahoo! JAPAN 検索広告（YSS）のリターゲティング ID を入力します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。


<blockquote>
タグを配信するには、**Tag Type** カテゴリーでトリガー条件を構成する必要があります。
</blockquote>


使用可能なカテゴリーは次のとおりです。

### ディスプレイ広告（YDN）コンバージョン

|変数|説明|
|---|---|
|コンバージョン IO（`yahoo_ydn_conv_io`）|［文字列］|
|コンバージョンラベル（`yahoo_ydn_conv_label`）|［文字列］|
|コンバージョントランザクション ID（`yahoo_ydn_conv_transaction_id`）|［文字列］|
|コンバージョン値（`yahoo_ydn_conv_value`）|［文字列］|

### ディスプレイ広告（YDN）リターゲティング

|変数|説明|
|---|---|
|リターゲティング ID（`yahoo_retargeting_id`）|［文字列］|
|リターゲティングラベル（`yahoo_retargeting_label`）|［文字列］|
|リターゲティングページタイプ（`yahoo_retargeting_page_type`）|［文字列］|
|リターゲティングアイテム（`yahoo_retargeting_items`）|［配列］|
|カテゴリー ID（`category_id`）（`_ccat` を上書き）|［配列］|
|アイテム ID（`item_id`）（`_cprod` を上書き）|［配列］|
|価格（`price`）（`_cprice` を上書き）|［配列］|
|数量（`quantity`）（`_cquan` を上書き）|［配列］|

### 検索広告（YSS）コンバージョン

|変数|説明|
|---|---|
|コンバージョン ID（`yahoo_conversion_id`）|［文字列］|
|コンバージョンラベル（`yahoo_conversion_label`）|［文字列］|
|コンバージョン値（`yahoo_conversion_value`）|［文字列］|

### 検索広告（YSS）リターゲティング

|変数|説明|
|---|---|
|リターゲティング ID（`yahoo_ss_retargeting_id`）|［文字列］|
|カスタムパラメーター|（`yahoo_sstag_custom_params`）|

### E コマース

|変数|説明|
|---|---|
|注文 ID（`order_id`）（`_corder` を上書き）|［文字列］|
|小計（`order_subtotal`）（`_csubtotal` を上書き）|［文字列］|
|商品カテゴリーのリスト（`product_category`）（`_ccat` を上書き）|［配列］|
|商品 ID のリスト（`product_id`）（`_cprod` を上書き）|［配列］|
|商品数量のリスト（`product_quantity`）（`_cquan` を上書き）|［配列］|
|商品価格のリスト（`product_unit_price`）（`_cprice` を上書き）|［配列］|

### タグタイプ

|変数|説明|
|---|---|
|ディスプレイ広告コンバージョン|`yjad_conversion`|
|ディスプレイ広告リターゲティング|`yjad_retargeting`|
|検索広告コンバージョン|`yss_conversion`|
|検索広告リターゲティング|`yss_retargeting`|
|カスタム|カスタム|

### タイプ固有のパラメーター

|変数|説明|
|---|---|
|コンバージョン IO（`yahoo_ydn_conv_io`）|`yahoo_ydn_conv_io`|
|コンバージョンラベル（`yahoo_ydn_conv_label`）|`yahoo_ydn_conv_label`|
|コンバージョントランザクション ID（`yahoo_ydn_conv_transaction_id`）|`yahoo_ydn_conv_transaction_id`|
|コンバージョン値（`yahoo_ydn_conv_value`）|`yahoo_ydn_conv_value`|
|リターゲティング ID（`yahoo_retargeting_id`）|`yahoo_retargeting_id`|
|リターゲティングラベル（`yahoo_retargeting_label`）|`yahoo_retargeting_label`|
|リターゲティングページタイプ（`yahoo_retargeting_page_type`）|`yahoo_retargeting_page_type`|
|リターゲティングアイテム（`yahoo_retargeting_items`）|`yahoo_retargeting_items`|
|アイテム ID（`item_id`）|`item_id`|
|カテゴリー ID（`category_id`）|`category_id`|
|価格（`price`）|`price`|
|数量（`quantity`）|`quantity`|
|コンバージョン ID（`yahoo_conversion_id`）|`yahoo_conversion_id`|
|コンバージョンラベル（`yahoo_conversion_label`）|`yahoo_conversion_label`|
|コンバージョン値（`yahoo_conversion_value`）|`yahoo_conversion_value`|
|リターゲティング ID（`yahoo_ss_retargeting_id`）|`yahoo_ss_retargeting_id`|
|カスタムパラメーター（`yahoo_sstag_custom_params`）|`yahoo_sstag_custom_params`|
|カスタムパラメーター|`Custom_Parameter`|
|ディスプレイ広告（YDN）コンバージョン|`yjad_conversion`|
|ディスプレイ広告（YDN）リターゲティング|`yjad_retargeting`|
|検索広告（YSS）コンバージョン|`yss_conversion`|
|検索広告（YSS）リターゲティング|`yss_retargeting`|
|カスタムタグタイプ|`Custom_Type`|

## ユースケース

### 読み込みルールに一致するすべてのページで YDN リターゲティングをトリガーする

読み込みルールに従ってすべてのページで配信されるタグを構成するには、次の手順を実行します。

1. **Tag Configuration** タブで、**Display Network Retargeting ID** ボックスに適切な値を入力します。
1. **Auto Tagging** を **True** に構成します。これにより、`ytag({"type":"ycl_cookie"});` の呼び出しがトリガーされます。
1. 必要に応じて読み込みルールを構成します。
1. **Data Mappings** タブの **Variables** ドロップダウンで、**Use Custom Value** をクリックします。
1. ダイアログの左上のセクションにあるボックスに **true** と入力します。
1. **Category** セクションで、**Tag Types** を選択します。
1. **When mapped variables equals** ボックスに **true** と入力します。
1. **Trigger tag type** ドロップダウンで、**Display Network Retargeting** を選択します。
1. **+Add** をクリックします。
1. **Done** をクリックします。
1. **Apply** をクリックします。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2022-07-06-at-13.35.19.png)
### 購入イベントで YDB コンバージョンをトリガーし、その他のページでリターゲティングを実行する

`tealium_event` 変数の値が `purchase` であるページで配信される YDN コンバージョンタグと、ロードルールに従ってその他のすべてのページで配信されるリターゲティングタグを構成するには、次の手順を実行します。

1. 上記の「ロードルールに一致するすべてのページで YDN リターゲティングをトリガーする」セクションの説明に従って、リターゲティングタグを構成します。
1. **タグ構成**タブで、**ディスプレイネットワークコンバージョン IO** と **コンバージョンラベル**の各ボックスに適切な値を入力します。
1. **データマッピング**タブの**変数**ドロップダウンで、`tealium_event` を選択します。
1. **+宛先を選択**をクリックします。
1. **カテゴリ**セクションで、**タグタイプ**を選択します。
1. **マッピングされた変数が次と等しい場合**ボックスに、`purchase` と入力します。
1. **トリガーするタグタイプ**ドロップダウンで、**ディスプレイネットワークコンバージョン**を選択します。
1. **+追加**をクリックします。
1. **カテゴリ**セクションで**ディスプレイネットワーク（YDN）コンバージョン**を選択し、**コンバージョントランザクション ID**や**コンバージョン値**などの同様のマッピングについて、手順3～8を繰り返します。
1. 複数のページでコンバージョンを配信するには、これらの手順を繰り返すか、拡張機能によって動的に値を割り当てられるベンダー固有の変数（例：`yahoo_conversion_value`）を作成します。
1. **完了**をクリックします。
1. **適用**をクリックします。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2022-07-06-at-13.42.31.png)

特定ページの URL で YDB コンバージョンをトリガーし、その他のページでリターゲティングを実行する

特定ページの URL（例：`/cart/thankyou`）で配信される YDN コンバージョンタグと、ロードルールに従ってその他のすべてのページで配信されるリターゲティングタグを構成するには、次の手順を実行します。

1. 上記の「ロードルールに一致するすべてのページで YDN リターゲティングをトリガーする」セクションの説明に従って、リターゲティングタグを構成します。
1. **タグ構成**タブで、**ディスプレイネットワークコンバージョン IO** と **コンバージョンラベル**の各ボックスに適切な値を入力します。
1. **データマッピング**タブの**変数**ドロップダウンで、**カスタム値**を選択します。
1. **+宛先を選択**をクリックします。
1. **カテゴリ**セクションで、**タグタイプ**を選択します。
1. **マッピングされた変数が次と等しい場合**ボックスに、コンバージョンをトリガーするページへのパス（例：`/cart/thankyou`）を入力します。
1. **トリガーするタグタイプ**ドロップダウンで、**ディスプレイネットワークコンバージョン**を選択します。
1. **+追加**をクリックします。
1. **カテゴリ**セクションで**ディスプレイネットワーク（YDN）コンバージョン**を選択し、**コンバージョントランザクション ID**や**コンバージョン値**などの同様のマッピングについて、手順3～8を繰り返します。
1. 複数のページでコンバージョンを配信するには、これらの手順を繰り返すか、拡張機能によって動的に値を割り当てられるベンダー固有の変数（例：`yahoo_conversion_value`）を作成します。
1. **完了**をクリックします。
1. **適用**をクリックします。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2022-07-06-at-13.43.38.png)