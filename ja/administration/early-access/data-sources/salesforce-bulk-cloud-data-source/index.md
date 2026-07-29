---
title: Salesforce Bulk クラウドデータソース
description: この記事では、Salesforce Bulk クラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/data-sources/salesforce-bulk-cloud-data-source/
---

<blockquote>
Salesforce Bulk クラウドデータソースは現在アーリーアクセス中で、選ばれた顧客のみが利用可能です。Salesforce Bulkを始めるには、Tealiumサポートに連絡してください。
</blockquote>


クラウドデータソースの構成の一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## 動作原理

Salesforce Bulk クラウドデータソースは、[Salesforce Bulk API 2.0](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/bulk_api_2_0.htm)を使用して、Salesforce組織からデータを読み取ります。

Salesforceは、SQLデータベースではなく、オブジェクトとフィールドとしてデータを整理するクラウドデータソースです。Salesforceからデータをインポートするとき、Tealiumは選択したオブジェクトからの各レコードをイベントとして処理します。

Salesforce Bulk データソースは、スケジュールされたバッチモデルを使用します：

* **スケジュール頻度**：時刻、日次、週次のスケジューリングをサポートします。
* **自動データ読み取り**：各スケジュール実行は、前回の実行以降のすべての新しいデータを読み取ります。

## データタイプ

データが正しくインポートされるように、以下のガイドラインに従ってSalesforceフィールドタイプをマッピングしてください：

| Salesforce | Tealium |
|:-----------|:--------|
| 数値、通貨、パーセント | 数値属性 |
| テキスト、メール、電話、URL、選択リスト、テキストエリア、時間 | 文字列属性 |
| チェックボックス | ブール属性 |
| 日付、日時 | 日付属性 |
| 複数選択リスト | 文字列の配列（デフォルト）、数値の配列、ブールの配列 |

Salesforceフィールドタイプの詳細については、[Salesforce: カスタムフィールドタイプ](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5)を参照してください。

## 接続の作成

Salesforceに接続するには、再利用可能な接続構成を作成します。接続構成には、名前と選択した認証方法に依存する認証フィールドが含まれます。

次の OAuth 2.0 認証方法が利用可能です。

### キーペア

サーバー間通信にキーペア方法を使用します。このフローでは、認証リクエストに署名するために証明書を使用し、ユーザーのログインは必要ありませんが、接続されたアプリの事前承認が必要です。Tealiumはキーペアを生成し、認証リクエストにプライベートキーを使用して署名します。対応する証明書をSalesforce Connected Appにアップロードします。アプリは署名されたJWTをSalesforceトークンエンドポイントに送信します。Salesforceは署名を検証し、アプリが事前に承認されている場合、アクセストークンを発行します。詳細については、[Salesforce: OAuth 2.0 JWT bearer flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_jwt_flow.htm&type=5)を参照してください。

キーペアを使用して接続を作成するには：

1. 認証方法として**キーペア**を選択します。
1. **コンシューマーキー**フィールドに、証明書を登録した接続アプリのコンシューマーキーを入力します。
1. **ユーザー名**フィールドに、あなたのSalesforceユーザー名を入力します。
1. **キーペア追加**をクリックし、**キーペア生成**を選択します。既存のキーペアを再利用するか、プライベートキーファイルをアップロードすることもできます。
1. 生成されたキーペア証明書ファイルをダウンロードします。
1. ダウンロードした証明書を接続アプリに適用します。
1. **完了**をクリックして接続を保存します。

### Salesforce OAuth

統合サーバーが秘密を安全に保管できる場合は、Salesforce OAuth方法を使用します。ユーザーがアクセスを承認し、サーバーは認証コードとトークンを交換します。詳細については、[Salesforce: OAuth 2.0 web server flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm&type=5)を参照してください。

Salesforce OAuthを使用して接続を作成するには：

1. 認証方法として**Salesforce OAuth**を選択します。
1. **アカウントタイプ**を選択して、接続に使用するSalesforceエンドポイントを指定します。
1. **接続確立**をクリックします。
1. 開いたSalesforceログイン画面で、ユーザー名とパスワードを入力します。
1. ログインに成功すると、承認ページにリダイレクトされます。Tealiumアプリへのアクセスを許可します。
1. **完了**をクリックして接続を保存します。

### OAuth

ユーザーログインが不要なサーバー間統合には、OAuth方法を使用します。Tealiumは消費者キーと秘密をSalesforce OAuthトークンエンドポイントに送信します。Salesforceは資格情報を検証し、割り当てられた統合ユーザーの代わりにアクセストークンを返します。Tealiumはこのトークンを使用してSalesforce APIを呼び出します。詳細については、[Salesforce: OAuth 2.0 client credentials flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm&type=5)を参照してください。

OAuthを使用して接続を作成するには：

1. 認証方法として**OAuth**を選択します。
1. **ベースURL**フィールドに、SalesforceホストURLを入力します。
1. **コンシューマーキー**フィールドに、外部クライアントアプリのコンシューマーキーを入力します。
1. **コンシューマーシークレット**フィールドに、外部クライアントアプリのコンシューマーシークレットを入力します。
1. **完了**をクリックして接続を保存します。

## クエリ構成

一般的な概要については、を参照してください。

Salesforce Bulkデータソースについては、以下の点に注意してください：

* **インクリメンティング**、**タイムスタンプ + インクリメンティング**、および**タイムスタンプ**クエリモード：これらのクエリモードはサポートされていません。代わりに**オフセットカラム**を指定してください。オフセットカラムは、単調に増加する値を持つ日付または日時フィールド（例：`CreatedDate`または`LastModifiedDate`）でなければなりません。コネクタはこのカラムを使用して進行状況を追跡し、重複読み取りを避けます。
* **高度なクエリモード**：SQLではなく、[Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm)を使用してクエリを記述します。

## 許可するIPアドレス

Salesforce組織がIPアドレスによるAPIアクセスを制限している場合は、[Tealium IPアドレス](https://docs.tealium.com/ip-allow-list/)をSalesforceの信頼できるIP範囲に追加してください。