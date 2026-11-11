---
title: Microsoft Azure Event Hubs コネクタ構成ガイド
description: Microsoft Azure Event Hubs は、大量のイベントを受信および処理するためのクラウドサービスです。この記事では、Customer Data Hub プロファイルでこのサービスを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/microsoft-azure-event-hubs-connector/
---## コネクタアクション

|**アクション名**| **オーディエンスでトリガー**| **ストリームでトリガー**|
|---| ---| ---|
|イベントデータを Event Hub に送信| ✗| ✓|
|訪問データを Event Hub に送信| ✓| ✗|
|カスタマイズしたデータを Event Hub に送信| ✓| ✓|

## 要件

* Microsoft Azure アカウント
* Service Bus 共有アクセスポリシーの認証情報
* データの送信先となる Event Hub の名前

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

1. **Configure** タブで、コネクタインスタンスのタイトルを入力します。

1. Azure Portal にサインインし、Event Hubs 名前空間、共有アクセスポリシー名、およびキーを作成します。次に、Event Hub を作成します。詳細については、[Azure Portal を使用して Event Hubs 名前空間と Event Hub を作成する](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create)を参照してください。

1. Event Hub 名前空間、共有アクセスポリシー、および共有アクセスキーを使用してコネクタを構成します。

1. **Test Connection** をクリックし、指定した認証情報を使用して API に接続できることを確認します。


<blockquote>
共有アクセスポリシーには、`Send`、`Listen`、`Manage` の3種類の権限を付与できます。指定するポリシーには、少なくとも `Send` 権限が必要です。
</blockquote>


## アクション構成 — パラメータとオプション

**Continue** をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — イベントデータを Event Hub に送信

#### パラメータ

| パラメータ | 説明 |
|---|---|
| Event Hub | （必須）このリストから Event Hub を選択します。構成したポリシーに **Manage** 権限が付与されている場合にのみ、これらのオプションを使用できます。権限が付与されていない場合は、カスタム値として Event Hub を手動で入力する必要があります。 |
| ユーザープロパティ | 属性を、**To** ドロップダウンでメッセージのユーザープロパティにマッピングします（カスタム値として入力）。 |
| ブローカープロパティ | 属性を、**To** ドロップダウンで任意のメッセージブローカープロパティにマッピングします。使用可能なオプションについては、以下を参照してください。 |
| 属性名を出力 | このチェックボックスをオンにすると、メッセージペイロード内の各イベントデータ属性の名前が表示されます。 |


<blockquote>
すべてのアクションで、メッセージのユーザープロパティとブローカープロパティがサポートされています。これらのプロパティは、キーと値のペアを使用して、メッセージに関する有用な情報を簡単に提供します。ただし、これらは HTTP ヘッダーとして構成され、メッセージ本文には含まれません。詳細については、[メッセージのユーザープロパティとブローカープロパティ](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties)を参照してください。
</blockquote>


#### オプション — ブローカープロパティ

|**オプション**| **説明**|
|---| ---|
|コンテンツタイプ|メッセージコンシューマー向けの HTTP ヘッダー `Content-Type` を構成します|
|相関 ID|相関を一意に識別する ID です|
|セッション ID|メッセージを分割し、特定のコンシューマーにルーティングするために使用できます|
|メッセージ ID|自動生成されるデフォルトのメッセージ ID を上書きします|
|ラベル|アプリケーションラベルです|
|返信先|メッセージコンシューマーの応答の送信先を指定するために使用できます|
|有効期間（秒）|指定した秒数が経過した後にメッセージを期限切れにします（Event Hub レベルの構成を上書きします）|
|送信先|送信先アドレスです|
|スケジュールされたエンキュー時刻|メッセージをエンキューする予定の日時です|
|返信先セッション ID|返信先と同様ですが、応答先としてセッションを指定します|
|パーティションキー|パーティション分割された Event Hub の一意の識別子です|

### アクション – 訪問データを Event Hub に送信

#### パラメータ

| パラメータ | 説明 |
|---|---|
| Event Hub | （必須）このリストから Event Hub を選択します。構成したポリシーに **Manage** 権限が付与されている場合にのみ、これらのオプションを使用できます。権限が付与されていない場合は、カスタム値として Event Hub を手動で入力する必要があります。 |
| ユーザープロパティ | 属性を、**To** ドロップダウンでメッセージのユーザープロパティにマッピングします（カスタム値として入力）。 |
| ブローカープロパティ | 属性を、**To** ドロップダウンで任意のメッセージブローカープロパティにマッピングします。使用可能な[ブローカープロパティ](#options---broker-properties)のオプションを参照してください。 |
| 訪問データに現在の訪問データを含める | 現在の訪問データをペイロードに追加します。「現在の訪問イベントデータを除外」が選択されていない場合は、イベントの訪問データも含まれます。 |
| 現在の訪問イベントデータを除外 | 現在の訪問データからイベントデータを除外します。 |
| 属性名を出力 | このチェックボックスをオンにすると、メッセージペイロード内の各訪問データ属性の名前が表示されます。 |

### アクション — カスタマイズしたデータを Event Hub に送信（詳細構成）

#### パラメータ

| パラメータ | 説明 |
|---|---|
| Event Hub |（必須）このリストから Event Hub を選択します。構成したポリシーに **Manage** 権限が付与されている場合にのみ、これらのオプションを使用できます。権限が付与されていない場合は、カスタム値として Event Hub を手動で入力する必要があります。 |
| ユーザープロパティ | 属性を、**To** ドロップダウンでメッセージのユーザープロパティにマッピングします（カスタム値として入力）。 |
| ブローカープロパティ | 属性を、**To** ドロップダウンで任意のメッセージブローカープロパティにマッピングします。使用可能な[ブローカープロパティ](#options---broker-properties)のオプションを参照してください。 |
| メッセージデータ | （必須）カスタムメッセージ本文を作成します。単純な1階層の JSON 形式では属性を名前にマッピングします。または、二重中括弧で囲んだテンプレート名を参照し、**Custom Message Definition** オプションを選択します。 |
| テンプレート変数 | 属性をテンプレート変数名にマッピングします。テンプレート変数は、すべてのテンプレートの置換とレンダリングに使用できます。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| テンプレート | レンダリングする1つ以上のテンプレートを指定します。通常、メッセージデータの作成には単一のテンプレートを使用します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。|


<blockquote>
必要に応じて、ユーザープロパティやブローカープロパティ内でテンプレートを参照し、挿入することもできます。
</blockquote>


## ベンダーのドキュメント

* [Azure Event Hubs とは](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-what-is-event-hubs)
* [Azure Portal を使用して Event Hubs 名前空間と Event Hub を作成する](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create)
* [SAS トークンを生成する](https://docs.microsoft.com/en-us/rest/api/eventhub/generate-sas-token)
* [共通のパラメータとヘッダー](https://docs.microsoft.com/en-us/rest/api/eventhub/event-hubs-runtime-rest)
* [メッセージのユーザープロパティとブローカープロパティ](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties)
* [Event Hub の一覧を取得する](https://docs.microsoft.com/en-us/rest/api/eventhub/list-event-hubs)
* [Event Hubs にイベントを送信する](https://docs.microsoft.com/en-us/rest/api/eventhub/send-event)