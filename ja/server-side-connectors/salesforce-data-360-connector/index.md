---
title: Salesforce Data 360コネクタ構成ガイド
description: この記事では、Salesforce Data 360コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-data-360-connector/
---


## 要件

このコネクタには、次のSalesforce Data 360リソースが必要です。

* Tealiumから受信するオブジェクトとフィールドを構成した[取り込みAPIソース](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-connect-an-ingestion-source.html)
* 取り込みAPIソース用のデータストリーム
* Data 360 Ingestion APIへのアクセス権を持つConnected AppまたはExternal Client App

詳細については、[Salesforce：取り込みソースの接続](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-connect-an-ingestion-source.html)を参照してください。

## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Salesforce Data 360 Ingestion API
* APIバージョン：v1
* APIエンドポイント：[Salesforce Data Cloud Ingestion API](https://developer.salesforce.com/docs/data/data-cloud-int/references/data-cloud-ingestionapi-ref/c360-a-api-get-started.html)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **Salesforceドメイン**
  * （必須）Salesforce組織のMy Domain URL（例：`https://company.my.salesforce.com`）。クライアント資格情報フローには、My Domain URLが必要です。その他のSalesforceホストでは、`request not supported on this domain`エラーが返されます。
* **クライアントID**
  * （必須）Salesforce Connected AppまたはExternal Client AppのConsumer Key。
  * アプリでクライアント資格情報フローを有効にし、実行ユーザーを構成したうえで、`cdp_ingest_api`および`api` OAuthスコープを付与する必要があります。
  * Connected AppまたはExternal Client AppのコールバックURLを`https://my.tealiumiq.com/oauth/salesforce/callback.html`に構成します。
  * Salesforceから`no client credentials user enabled`が返された場合は、実行ユーザーが構成されていることを確認してください。このエラーは、Client Secretが正しくないことを示すものではありません。
* **クライアントシークレット**
  * （必須）Salesforce Connected AppまたはExternal Client AppのConsumer Secret。
* **ソースAPI名**
  * （必須）Salesforce Data 360の取り込みAPIソースのSource API Name。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| ----------- | :------------: | :---------: |
| 取り込みAPIレコードを送信 | ✓ | ✓ |

### 取り込みAPIレコードを送信

#### バッチ制限

このアクションは、ベンダーへの大容量データ転送に対応するため、バッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達することがあります。イベントの順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。

次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに入れられます。

* リクエストの最大数：200
* 最も古いリクエストからの最大経過時間：10分

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| オブジェクトAPI名 | （必須）レコードの送信先となるSalesforce Data 360オブジェクト。使用可能なオブジェクトは、選択した取り込みAPIソースから取得されます。オブジェクトが一覧にない場合は、そのObject API Nameを入力してEnterキーを押します。名前では大文字と小文字が区別されるため、Salesforceスキーマと完全に一致させる必要があります。 |
| レコードデータ | （必須）Tealium属性をSalesforce Data 360オブジェクトスキーマの宛先フィールドにマッピングします。マッピング要件については、[レコードデータ](#record-data)を参照してください。 |

#### レコードデータ

Tealium属性を、選択したSalesforce Data 360オブジェクトの宛先フィールドにマッピングします。マッピングを構成する際は、次の要件に従ってください。

* フィールドにネストされたオブジェクトまたは配列が必要な場合は、**テンプレート**タブでテンプレートを定義し、そのテンプレート名をマッピング値として入力します。
* データストリームの主キーと、Salesforce取り込みスキーマで必須としてマークされているその他のフィールドを含めます。
* 部分更新の場合は、構成済みの**レコード更新日時**フィールドを含めます。エンゲージメントオブジェクトの場合は、構成済みの**イベント時刻**フィールドも含めます。
* マッピングされた値が、ISO 8601形式のタイムスタンプ、数値、ブール値など、Salesforceで想定されるデータ型および形式と一致していることを確認します。
* ソースに`SalesCustomer`や`Order`など複数のオブジェクトが含まれている場合は、各**レコードデータ**マッピングが単一のオブジェクトスキーマに対応するように、Object API Nameごとに個別のアクションを作成します。


<blockquote>
Salesforceは取り込みリクエストを非同期で処理します。成功レスポンスは、Salesforceが処理対象としてリクエストを受け付けたことを示しますが、すべてのレコードが取り込まれたことを保証するものではありません。必須値の欠落、無効なデータ型、その他のスキーマ不一致があると、Tealiumにエラーが返されることなく、後続の処理中にレコードの取り込みが失敗する可能性があります。
</blockquote>


#### テンプレート

| パラメータ | 説明 |
| --- | --- |
| テンプレート | （任意）ネストされたオブジェクトや配列、条件付きフィールド、書式構成されたタイムスタンプ、派生値や静的な値、またはスキーマ固有の変換が必要なフィールド用のテンプレートを作成します。左側にテンプレート名を入力し、右側に有効なJSONを生成するテンプレートを入力します。テンプレートを使用するには、**レコードデータ**でその名前を宛先フィールドにマッピングします。テンプレートは、マッピングされたフィールドから参照されている場合にのみ送信されます。最上位の`data`ラッパーは含めないでください。Tealiumによって自動的に追加されます。 |
| テンプレート変数 | （任意）Tealium属性を、テンプレートで使用する変数名にマッピングします。 |