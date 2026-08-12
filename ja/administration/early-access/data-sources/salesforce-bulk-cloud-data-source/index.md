---
title: Salesforce Bulk クラウドデータソース
description: Salesforce Bulk クラウドデータソースを構成して、Salesforce 組織から Tealium へのイベントとしてレコードをインポートします。
url: https://docs.tealium.com/ja/administration/early-access/data-sources/salesforce-bulk-cloud-data-source/
--- 

<blockquote>
Salesforce Bulk クラウドデータソースは現在アーリーアクセス中で、選ばれた顧客のみが利用可能です。Salesforce Bulk を始めるには Tealium サポートに連絡してください。
</blockquote>


クラウドデータソースの構成の一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## 動作原理

Salesforce Bulk クラウドデータソースは、[Salesforce Bulk API 2.0](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/bulk_api_2_0.htm) を使用して Salesforce 組織からデータを読み取ります。

Salesforce は SQL データベースではなく、オブジェクトとフィールドとしてデータを整理するクラウドデータソースです。Salesforce からデータをインポートするとき、Tealium は選択したオブジェクトからの各レコードをイベントとして処理します。

Salesforce Bulk データソースはスケジュールされたバッチモデルを使用します：

* **スケジュール頻度**：時刻、日次、週次のスケジューリングをサポートします。
* **自動データ読み取り**：各スケジュール実行は、前回の実行以降のすべての新しいデータを読み取ります。

## データタイプ

Tealium がデータを正しくインポートするために、以下のガイドラインに従って Salesforce フィールドタイプをマッピングしてください：

| Salesforce | Tealium |
|:-----------|:--------|
| 数値、通貨、パーセント | 数値属性 |
| テキスト、メール、電話、URL、選択リスト、テキストエリア、時間 | 文字列属性 |
| チェックボックス | ブール属性 |
| 日付、日付/時刻 | 日付属性 |
| マルチセレクト選択リスト | 文字列の配列（デフォルト）、数値の配列、ブールの配列 |

Salesforce フィールドタイプの詳細については、[Salesforce: カスタムフィールドタイプ](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5)を参照してください。

## 接続の作成

Salesforce に接続するには、再利用可能な接続構成を作成します。接続構成には名前と、選択した認証方法に依存する認証フィールドが含まれます。

次の OAuth 2.0 認証方法が利用可能です。

### JWT トークン

サーバー間通信に JWT トークン方法を使用します。このフローは、認証リクエストに署名するために証明書を使用し、ユーザーのログインを必要としませんが、接続されたアプリの事前承認が必要です。Tealium はキーペアを生成し、認証リクエストにプライベートキーで署名します。対応する証明書を Salesforce Connected App にアップロードします。アプリは署名された JWT を Salesforce トークンエンドポイントに送信します。Salesforce は署名を検証し、アプリが事前に承認されていると仮定して、アクセストークンを発行します。詳細については、[Salesforce: OAuth 2.0 JWT ベアラーフロー](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_jwt_flow.htm&type=5)を参照してください。

JWT トークンを使用して接続を作成するには：

1. 認証方法として **JWT トークン** を選択します。
1. **コンシューマーキー** フィールドに、証明書を登録した接続アプリのコンシューマーキーを入力します。
1. **ユーザー名** フィールドに、あなたの Salesforce ユーザー名を入力します。
1. **キーペア追加** をクリックし、**キーペア生成** を選択します。既存のキーペアを再利用するか、プライベートキーファイルをアップロードすることもできます。
1. 生成されたキーペア証明書ファイルをダウンロードします。
1. ダウンロードした証明書を接続アプリに適用します。
1. **完了** をクリックして接続を保存します。

### Web サーバー

統合サーバーが秘密を安全に保管できる場合は、Web サーバー方法を使用します。アクセスを承認し、サーバーは認証コードをトークンと交換します。詳細については、[Salesforce: OAuth 2.0 Web サーバーフロー](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm&type=5)を参照してください。

Web サーバーを使用して接続を作成するには：

1. 認証方法として **Web サーバー** を選択します。
1. 接続に使用する Salesforce エンドポイントを指定するために **アカウントタイプ** を選択します。
1. **接続の確立** をクリックします。
1. 開いた Salesforce ログイン画面で、ユーザー名とパスワードを入力します。
1. ログインに成功すると、承認ページにリダイレクトされます。Tealium アプリへのアクセスを許可します。
1. **完了** をクリックして接続を保存します。

### クライアント資格情報

ユーザーログインが不要なサーバー間統合には、クライアント資格情報方法を使用します。Tealium はコンシューマーキーとシークレットを Salesforce OAuth トークンエンドポイントに送信します。Salesforce は資格情報を検証し、割り当てられた統合ユーザーの代わりにアクセストークンを返します。Tealium はこのトークンを使用して Salesforce API を呼び出します。詳細については、[Salesforce: OAuth 2.0 クライアント資格情報フロー](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm&type=5)を参照してください。

クライアント資格情報を使用して接続を作成するには：

1. 認証方法として **クライアント資格情報** を選択します。
1. **ベース URL** フィールドに、あなたの Salesforce ホスト URL を入力します。
1. **コンシューマーキー** フィールドに、外部クライアントアプリのコンシューマーキーを入力します。
1. **コンシューマーシークレット** フィールドに、外部クライアントアプリのコンシューマーシークレットを入力します。
1. **完了** をクリックして接続を保存します。

## クエリ構成

一般的な概要については、を参照してください。

Salesforce Bulk データソースについては、以下の点に注意してください：

* **インクリメンティング**、**タイムスタンプ + インクリメンティング**、および **タイムスタンプ** クエリモード：Salesforce Bulk データソースはこれらのクエリモードをサポートしていません。代わりに **オフセットカラム** を指定してください。オフセットカラムは、単調に増加する値を持つ Date または Date/Time フィールド（例：`CreatedDate` または `LastModifiedDate`）でなければなりません。コネクタはこのカラムを使用して進行状況を追跡し、重複読み取りを避けます。
* **高度なクエリモード**：SQL ではなく、[Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) を使用してクエリを記述します。

## 許可する IP アドレス

あなたの Salesforce 組織が IP アドレスによる API アクセスを制限している場合は、[Tealium IP アドレス](https://docs.tealium.com/ip-allow-list/)を Salesforce の信頼できる IP 範囲に追加してください。
