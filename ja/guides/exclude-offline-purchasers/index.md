---
title: オフライン購入者をリマーケティングから除外する
description: このガイドでは、マーケティング効率と顧客体験を向上させるために、オンラインのリマーケティング施策からオフライン購入者を除外する方法について説明します。
url: https://docs.tealium.com/ja/guides/exclude-offline-purchasers/
---
## オフライン購入者をリターゲティングから除外する理由

オンラインマーケティングキャンペーンからオフライン購入者を除外する理由はいくつかあります。

* **重複する広告を避ける**：商品をオンラインで閲覧し、店舗で購入を完了した購入者に対して、その商品のリマーケティングを行う必要はありません。
* **より関連性の高いオファーを提供する**：店舗での購入を好む購入者は、送料無料などのオンライン限定プロモーションには関心がない可能性があります。

このアプローチは、広告費を削減するだけでなく、購入済みの商品に関する広告が表示されることによる顧客の不満を防ぐためにも役立ちます。

顧客をリマーケティング施策から恒久的に除外しないでください。顧客が商品の閲覧や検索を通じてサイトを再び利用した場合は、除外リストから削除することが重要です。これにより、顧客が再び関心を示した時点でマーケティング施策が再開され、関連性の高いメッセージを提供して機会損失を防ぐことができます。

## オフライン購入者を追跡する方法

オフライン購入者を追跡するには、File Import、Data Connect、またはAPIを使用して、オフライン取引データをTealiumにインポートします。次に、それらの訪問に「Offline Shopper」バッジを付与します。このバッジを使用して除外オーディエンスを作成し、リマーケティングベンダーに送信することで、これらの顧客を不要なリターゲティングから除外できます。

## 要件

#### 必須のEventStream属性

| 属性名 | タイプ | 例 | 
| --- | --- | --- | 
| `customer_email` | UDO変数 | `user@example.com` | 

#### 必須のAudienceStream属性

| 属性名 | タイプ | スコープ | 説明 |
|----------------|--------|---------|----------------|
| Email Address | 文字列 | 訪問 | 顧客のメールアドレス。 |
| Offline Shopper | バッジ | 訪問 | オフラインで購入を完了した訪問。 |
| User Actions | ブール値 | 訪問 | 検索または商品の閲覧によってサイトを再び利用した訪問。 |

次の例では、オフライン顧客とその購入を**Offline Shoppers**バッジによって識別し、そのバッジを持つ訪問でオーディエンスを作成します。次に、リマーケティングベンダーを通じてオーディエンスをアクティベートし、除外リストを更新します。

## ステップ1：属性を作成する

`Email Address`という名前の文字列型訪問属性を、次のエンリッチメントで作成します。

* **ANY EVENT**で`customer_email`に構成します。

![](https://docs.tealium.com/images/guides/offline_purchases_string_email address.png)

訪問が商品の閲覧や検索によってサイトを再び利用しているかどうかを追跡するには、`User Actions`という名前のブール型訪問属性を、次のエンリッチメントで作成します。

* **NEW VISIT**で`false`に構成します。
* `tealium_event`に`search`が含まれるか、`tealium_event`に`product_view`が含まれる場合、**ANY EVENT**で`true`に構成します。

必要に応じて、監視するその他のイベントをこの属性に追加してください。

![](https://docs.tealium.com/images/guides/user_actions_attribute.png)

属性の追加について詳しくは、[AudienceStream属性の管理](https://docs.tealium.com/manage-as-attributes/)を参照してください。

## ステップ2：データソースの構成

このステップでは、店舗の購入データへの接続を構成します。このデータを収集して処理する方法はいくつかあります。

* [Data Connect](https://docs.tealium.com/about-data-connect/)を使用すると、データワークフローを自動化、スケジュール構成、拡張し、SaaSアプリケーション、CRM、データウェアハウスからTealiumへリアルタイムでデータをインポートできます。
* [HTTP-API Advanced](https://docs.tealium.com/http-api-advanced-incoming-webhook-setup-guide/)データソースでは、受信したリクエスト本文を条件に応じて解析できます。このデータソースは、複雑なオブジェクトのフラット化とイベントのバッチ処理をサポートし、1回のHTTP呼び出しでリアルタイムイベントデータを収集できるHTTPエンドポイントを提供します。
* [File Import](https://docs.tealium.com/about-file-import/)を使用すると、各行が1つのイベントを表すCSVファイルをTealiumにインポートできます。

次の例では、除外リストで使用するオフラインデータをFile Importで処理する方法を示します。

* **サンプルファイルを作成する**：CSVサンプルファイルには、顧客IDやメールアドレスなど、顧客を識別するために必要な取引の詳細を含める必要があります。1行目の列名は自動的に検出され、**Column Mappings**画面の項目を事前構成するために使用されます。![](https://docs.tealium.com/images/guides/offline_purchasers_csv_file.png)
* **ファイルをアップロードして確認する**：サンプルファイルをスクロールし、列とデータが正しいことを確認します。
* **列をイベント属性にマッピングする**：CSVファイルの各行はイベントとして処理されます。マッピングされていない列は無視されます。CSVファイルに存在しないマッピング済みの列はスキップされます。![](https://docs.tealium.com/images/guides/map_columns.png)
* **イベント仕様を選択する**：ファイル内のデータと一致していることを確認するか、イベント属性のカスタムセットを作成します。
* **訪問ID属性を識別してマッピングする**：メールアドレスなどの適切なイベント属性を訪問ID属性にマッピングします。![](https://docs.tealium.com/images/guides/visitor_id_mapping.png)

後で使用するために、必ず**Data Source Key**をコピーしてください。

![](https://docs.tealium.com/images/guides/file_import_summary.png)

変更を保存してパブリッシュします。

File Importの構成方法について詳しくは、[File Import](https://docs.tealium.com/about-file-import/)を参照してください。

## ステップ3：Offline Shopperバッジを作成する

メールアドレスによってオフライン購入者を識別できるようになったため、その属性に基づいてOffline Shopperバッジを作成できます。

「Offline Shopper」という訪問属性をバッジタイプとして、次のエンリッチメントで追加します。先ほど保存したデータソースキーを使用してください。

* `tealium_datasource`がインポートプロファイルのデータソースキーと等しい場合（大文字と小文字を区別しない）、**ANY EVENT**でこのバッジを訪問に割り当てます。
* `User Actions`が`true`の場合、**VISIT ENDED**でこのバッジを訪問から削除します。

![](https://docs.tealium.com/images/guides/offline_shopper_badge.png)

## ステップ4：Offline Shoppersオーディエンスを作成する

次の条件でOffline Shoppersオーディエンスを作成できます。

* `Offline Shopper`バッジが割り当てられている。
* `Email Address`文字列が割り当てられている。

![](https://docs.tealium.com/images/guides/offline_shoppers_audience.png)

詳しくは、を参照してください。
## ステップ 5 - コネクタを構成する

リマーケティングベンダーを通じてオーディエンスをアクティベートし、キャンペーン構成と除外構成を更新します。

割引商品を購入する顧客をターゲティングする際によく使用されるコネクタとアクションには、次のものがあります。

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/)：**ユーザーをリストに登録**、**ユーザーをアップサート**アクション
* [Marketo](https://docs.tealium.com/marketo-connector/)：**リードをリストに追加**アクション
* [SendGrid](https://docs.tealium.com/sendgrid-connector/)：**連絡先をアップサート**アクション

たとえば、訪問のメールアドレスをリマーケティングの除外リストに追加するように、Marketoコネクタを構成できます。訪問が「Offline Shoppers」オーディエンスに参加した場合にのみトリガーされるよう、コネクタアクションをカスタマイズします。

![](https://docs.tealium.com/images/guides/offline_shoppers_marketo1.png)

![](https://docs.tealium.com/images/guides/offline_shoppers_marketo2.png)

次に、訪問がサイトに戻ったときに除外リストから削除するため、Marketoコネクタの別のインスタンスを構成する必要があります。訪問が「Offline Shoppers」オーディエンスから離脱した場合にのみトリガーされるよう、コネクタアクションをカスタマイズします。

![](https://docs.tealium.com/images/guides/offline_shoppers_marketo3.png)

![](https://docs.tealium.com/images/guides/offline_shoppers_marketo4.png)

詳細については、を参照してください。

## ステップ 6 - データをインポートする

属性、バッジ、オーディエンスの構成が完了したら、Tealiumのファイルインポート機能を使用してデータをアップロードします。AudienceStreamは、このデータを訪問プロファイルに統合し、オーディエンスを更新して、リマーケティングコネクタに更新情報を送信します。

アップロード手順の詳細については、[ファイルインポートについて](https://docs.tealium.com/about-file-import/#step-2-upload-your-files-to-a-file-transfer-service)を参照してください。