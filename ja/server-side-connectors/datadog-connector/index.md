---
title: Datadogコネクタ構成ガイド
description: この記事では、Datadogコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/datadog-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**  
  DatadogのAPIキー。APIキーを管理するには、[Datadogにログイン](https://app.datadoghq.com/organization-settings/)してください。
* **ホスト**  
  Datadog APIクライアントがAPIを消費するDatadogホストを構成します。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベント送信 | ✗ | ✓ |
| ログ送信 | ✗ | ✓ |
| ログ送信（バッチ処理） | ✗ | ✓ |
| ログイベント送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### イベント送信

#### イベントパラメータ

必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| テキスト | イベントの本文。4000文字に制限されています。イベントテキストにマークダウンを使用する場合は、テキストブロックを `%%%` で始めて `%%%` で終えてください。 |
| タイトル | イベントのタイトル。 |
| 集約キー | 集約に使用する任意の文字列（最大100文字）。キーを指定すると、そのキーを使用するすべてのイベントがEventStreamでグループ化されます。 |
| アラートタイプ | アラートイベントが有効な場合、そのタイプを構成します。許可される値：`error`, `warning`, `info`, `success`, `user_update`, `recommendation`, `snapshot`。 |
| 発生日時 | イベントのPOSIXタイムスタンプ。整数として送信する必要があり、18時間以上前のイベントには制限されます。 |
| デバイス名 | デバイス名。 |
| ホスト | イベントに関連付けるホスト名。ホストに関連付けられたタグもこのイベントに適用されます。 |
| 優先度 | イベントの優先度。許可される値：`normal`または`low`。 |
| 関連イベントID | 親イベントのID。整数として送信する必要があります。 |
| ソースタイプ名 | 投稿されるイベントのタイプ。オプションの例には、`nagios`, `hudson`, `jenkins`, `my_apps`, `chef`, `puppet`, `git`, `bitbucket`が含まれます。完全なリストについては、[Datadog: APIソース属性](https://docs.datadoghq.com/integrations/faq/list-of-api-source-attribute-value/)を参照してください。 |
| タグ | イベントに適用するタグのリスト。 |

### ログ送信

#### ログパラメータ

必須フィールド：

| **パラメータ** | **説明** |
| --- | --- |
| DDソース | ログに関連付けられた統合名。Datadogが統合名に一致すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DDタグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの発信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs`から`APM`に切り替える際に使用されるため、両方の製品を使用する場合は同じ値を定義してください。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |

#### ログメッセージパラメータ

ログの[予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)。デフォルトでは、Datadogはメッセージ属性の値をログエントリの本文として取り込みます。その値はハイライト表示され、ログストリームで表示され、全文検索のためにインデックスが作成されます。

メッセージは次の形式に基づいて構築されます：`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`。この形式を無視するには、**メッセージオーバーライド**パラメータを使用します。

| **パラメータ** | **説明** |
| --- | --- |
| メッセージオーバーライド | この属性をマッピングして、メッセージ全体を渡します。これにより、`message`属性がオーバーライドされます。 |
| タイムスタンプ | ログのタイムスタンプ。このフィールドが入力されていない場合、メッセージで現在のタイムスタンプが使用されます。 |
| 重要度 | メッセージで使用されるログの重要度。 |
| 件名 | メッセージで使用されるログの件名。 |
| 内容 | メッセージ本文の短縮要約。 |

### ログ送信（バッチ処理）

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：1,000
* 最古のリクエストからの最大時間：15分
* リクエストの最大サイズ：5 MB

#### ログパラメータ

必須フィールド：

| **パラメータ** | **説明** |
| --- | --- |
| DDソース | ログに関連付けられた統合名。Datadogが統合名に一致すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DDタグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの発信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs`から`APM`に切り替える際に使用されるため、両方の製品を使用する場合は同じ値を定義してください。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |

#### ログメッセージパラメータ

ログの[予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)。デフォルトでは、Datadogはメッセージ属性の値をログエントリの本文として取り込みます。その値はハイライト表示され、ログストリームで表示され、全文検索のためにインデックスが作成されます。

メッセージは次の形式に基づいて構築されます：`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`。この形式を無視するには、**メッセージオーバーライド**パラメータを使用します。

| **パラメータ** | **説明** |
| --- | --- |
| メッセージオーバーライド | この属性をマッピングして、メッセージ全体を渡します。これにより、`message`属性がオーバーライドされます。 |
| タイムスタンプ | ログのタイムスタンプ。このフィールドが入力されていない場合、メッセージで現在のタイムスタンプが使用されます。 |
| 重要度 | メッセージで使用されるログの重要度。 |
| 件名 | メッセージで使用されるログの件名。 |
| 内容 | メッセージ本文の短縮要約。 |

### ログイベント送信

#### ログパラメータ

必須フィールド：

| **パラメータ** | **説明** |
| --- | --- |
| DDソース | ログに関連付けられた統合名。Datadogが統合名に一致すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DDタグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの発信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs`から`APM`に切り替える際に使用されるため、両方の製品を使用する場合は同じ値を定義してください。詳細については、[Datadog: 予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
#### ログメッセージパラメータ

ログの[予約属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)です。デフォルトでは、Datadogはメッセージ属性の値をログエントリの本文として取り込みます。その値は強調表示され、ログストリームに表示され、全文検索のためにインデックスされます。

メッセージは次の形式に基づいて構築されます：`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`。この形式を無視するには、**Message Override** パラメータを使用します。

| **パラメータ** | **説明** |
| --- | --- |
| Message Override | この属性をマッピングして、メッセージ全体を渡します。これにより `message` 属性が上書きされます。 |
| Timestamp | ログのタイムスタンプ。このフィールドが入力されていない場合、メッセージで現在のタイムスタンプが使用されます。 |
| Severity | メッセージで使用されるログの重要度。 |
| Subject | メッセージで使用されるログの主題。 |
| Content | メッセージ本文の短縮された要約。 |