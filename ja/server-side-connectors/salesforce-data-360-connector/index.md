---
title: Salesforce Data 360 コネクタ構成ガイド
description: この記事では、Salesforce Data 360 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-data-360-connector/
---


## 要件

このコネクタには、以下のSalesforce Data 360リソースが必要です：

* Tealiumから受信したいオブジェクトとフィールドで構成された[Ingestion API ソース](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-connect-an-ingestion-source.html)
* Ingestion API ソースのデータストリーム
* Data 360 Ingestion APIへのアクセス権を持つConnected AppまたはExternal Client App

詳細については、[Salesforce: Connect an ingestion source](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-connect-an-ingestion-source.html)を参照してください。

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Salesforce Data 360 Ingestion API
* APIバージョン：v1
* APIエンドポイント：[Salesforce Data Cloud Ingestion API](https://developer.salesforce.com/docs/data/data-cloud-int/references/data-cloud-ingestionapi-ref/c360-a-api-get-started.html)

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[About Connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **Salesforceドメイン**
  * （必須）Salesforce組織のMy Domain URL。例：`https://company.my.salesforce.com`。クライアント資格情報フローにはMy Domain URLが必要です。他のSalesforceホストでは`request not supported on this domain`エラーが返されます。
* **クライアントID**
  * （必須）Salesforce Connected AppまたはExternal Client AppからのConsumer Key。
  * アプリはクライアント資格情報フローを有効にし、Run Asユーザーを構成し、`cdp_ingest_api`および`api` OAuthスコープを持っている必要があります。
  * Connected AppまたはExternal Client AppのコールバックURLを`https://my.tealiumiq.com/oauth/salesforce/callback.html`に構成します。
  * Salesforceが`no client credentials user enabled`を返した場合、Run Asユーザーが構成されているか確認してください。このエラーはクライアントシークレットが間違っていることを示すものではありません。
* **クライアントシークレット**
  * （必須）Salesforce Connected AppまたはExternal Client AppからのConsumer Secret。
* **ソースAPI名**
  * （必須）Salesforce Data 360のIngestion APIソースのソースAPI名。

## アクション

| アクション名 | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Ingestion API Records | ✓ | ✓ |

### Send Ingestion API Records

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントがベンダーに順不同で到達する可能性があります。イベントの順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。

リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：200
* 最古のリクエストからの最大時間：10分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| Object API Name | （必須）レコードを送信するSalesforce Data 360オブジェクト。利用可能なオブジェクトは選択したIngestion APIソースから取得されます。オブジェクトがリストにない場合は、そのObject API Nameを入力してEnterキーを押してください。名前は大文字と小文字が区別され、Salesforceスキーマと正確に一致する必要があります。 |
| Record Data | （必須）Tealiumの属性をSalesforce Data 360オブジェクトスキーマの宛先フィールドにマッピングします。マッピング要件については、[Record Data](#record-data)を参照してください。 |

#### Record Data

選択したSalesforce Data 360オブジェクトの宛先フィールドにTealiumの属性をマッピングします。マッピングを構成する際には、以下の要件に従ってください：

* フィールドがネストされたオブジェクトまたは配列を必要とする場合は、**Templates**タブでテンプレートを定義し、マップされた値としてテンプレート名を入力します。
* Data Streamの主キーおよびSalesforce摂取スキーマで必須とされている他のフィールドを含めます。
* 部分更新の場合は、構成された**Record Modified**フィールドを含めます。エンゲージメントオブジェクトの場合は、構成された**Event Time**フィールドも含めます。
* マップされた値がSalesforceによって期待されるデータタイプとフォーマット、例えばISO 8601タイムスタンプ、数字、およびブール値と一致することを確認します。
* ソースに複数のオブジェクトが含まれている場合、例えば`SalesCustomer`と`Order`の場合、各Object API Nameに対して別のアクションを作成し、各**Record Data**マッピングが単一のオブジェクトスキーマに対応するようにします。


<blockquote>
Salesforceは摂取リクエストを非同期で処理します。成功したレスポンスはSalesforceが処理のためにリクエストを受け入れたことを確認しますが、すべてのレコードが摂取されたことを確認するものではありません。必要な値が欠けている、データタイプが無効である、または他のスキーマの不一致が原因で、下流の処理中にレコードが失敗する可能性がありますが、Tealiumにエラーが返されることはありません。
</blockquote>


#### Templates

| パラメータ | 説明 |
| --- | --- |
| Templates | （オプション）ネストされたオブジェクトや配列、条件付きフィールド、フォーマットされたタイムスタンプ、派生値または静的値、またはスキーマ固有の変換が必要なフィールドのためにテンプレートを作成します。左側にテンプレート名を入力し、右側に有効なJSONをレンダリングするテンプレートを入力します。テンプレートを使用するには、その名前を**Record Data**の宛先フィールドにマッピングします。テンプレートは、マップされたフィールドによって参照される場合にのみ送信されます。トップレベルの`data`ラッパーは含めないでください。Tealiumが自動的に追加します。 |
| Template Variables | （オプション）Tealiumの属性をテンプレートで使用される変数名にマッピングします。 |