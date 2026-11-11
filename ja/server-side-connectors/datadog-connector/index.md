---
title: Datadog コネクター構成ガイド
description: この記事では、Datadog コネクターの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/datadog-connector/
---
## 構成

コネクターマーケットプレイスに移動し、新しいコネクターを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクターを追加したら、次の構成を行います。

* **API キー**  
  Datadog API キー。API キーを管理するには、[Datadog にログイン](https://app.datadoghq.com/organization-settings/)します。
* **ホスト**  
  Datadog API クライアントが API を利用する Datadog ホストを構成します。

コネクターを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントを送信 | ✗ | ✓ |
| ログを送信 | ✗ | ✓ |
| ログを送信（バッチ） | ✗ | ✓ |
| ログイベントを送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### イベントを送信

#### イベントパラメーター

必須パラメーター：

| **パラメーター** | **説明** |
| --- | --- |
| テキスト | イベントの本文。4000 文字までに制限されています。イベントテキストで Markdown を使用するには、テキストブロックを `%%%` で開始し、`%%%.` で終了します。 |
| タイトル | イベントのタイトル。 |
| 集約キー | 集約に使用する最大 100 文字の任意の文字列。キーを指定すると、そのキーを使用するすべてのイベントが EventStream でグループ化されます。 |
| アラートタイプ | アラートイベントが有効になっている場合は、そのタイプを構成します。使用できる値：`error`、`warning`、`info`、`success`、`user_update`、`recommendation`、`snapshot`。 |
| 発生日時 | イベントの POSIX タイムスタンプ。整数として送信する必要があり、18 時間以内に発生したイベントに限られます。 |
| デバイス名 | デバイス名。 |
| ホスト | イベントに関連付けるホスト名。ホストに関連付けられているタグも、このイベントに適用されます。 |
| 優先度 | イベントの優先度。使用できる値：`normal` または `low`。 |
| 関連イベント ID | 親イベントの ID。整数として送信する必要があります。 |
| ソースタイプ名 | 投稿するイベントのタイプ。オプションの例：`nagios`、`hudson`、`jenkins`、`my_apps`、`chef`、`puppet`、`git`、`bitbucket`。完全なリストについては、[Datadog：API ソース属性](https://docs.datadoghq.com/integrations/faq/list-of-api-source-attribute-value/)を参照してください。 |
| タグ | イベントに適用するタグのリスト。 |

### ログを送信

#### ログパラメーター

必須フィールド：

| **パラメーター** | **説明** |
| --- | --- |
| DD ソース | ログに関連付けられたインテグレーション名。Datadog がインテグレーション名を照合すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DD タグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの送信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs` から `APM` への切り替えに使用されるため、両方の製品を使用する場合は、必ず同じ値を定義してください。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |

#### ログメッセージパラメーター

ログのメッセージ[予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)。デフォルトでは、Datadog はメッセージ属性の値をログエントリーの本文として取り込みます。その後、その値はログストリーム内で強調表示され、全文検索用にインデックスが作成されます。

メッセージは、`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]` の形式に基づいて構築されます。この形式を無視するには、**メッセージの上書き**パラメーターを使用します。

| **パラメーター** | **説明** |
| --- | --- |
| メッセージの上書き | メッセージ全体を渡すには、この属性をマッピングします。これにより、`message` 属性が上書きされます。 |
| タイムスタンプ | ログのタイムスタンプ。このフィールドに値が入力されていない場合、メッセージでは現在のタイムスタンプが使用されます。 |
| 重大度 | メッセージで使用されるログの重大度。 |
| 件名 | メッセージで使用されるログの件名。 |
| コンテンツ | メッセージ本文を短くまとめた概要。 |

### ログを送信（バッチ）

#### バッチ制限

このアクションでは、ベンダーへの大容量データ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルが公開されるまで、リクエストはキューに格納されます。

* リクエストの最大数：1,000
* 最も古いリクエストからの最大経過時間：15 分
* リクエストの最大サイズ：5 MB

#### ログパラメーター

必須フィールド：

| **パラメーター** | **説明** |
| --- | --- |
| DD ソース | ログに関連付けられたインテグレーション名。Datadog がインテグレーション名を照合すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DD タグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの送信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs` から `APM` への切り替えに使用されるため、両方の製品を使用する場合は、必ず同じ値を定義してください。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |

#### ログメッセージパラメーター

ログのメッセージ[予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)。デフォルトでは、Datadog はメッセージ属性の値をログエントリーの本文として取り込みます。その後、その値はログストリーム内で強調表示され、全文検索用にインデックスが作成されます。

メッセージは、`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]` の形式に基づいて構築されます。この形式を無視するには、**メッセージの上書き**パラメーターを使用します。

| **パラメーター** | **説明** |
| --- | --- |
| メッセージの上書き | メッセージ全体を渡すには、この属性をマッピングします。これにより、`message` 属性が上書きされます。 |
| タイムスタンプ | ログのタイムスタンプ。このフィールドに値が入力されていない場合、メッセージでは現在のタイムスタンプが使用されます。 |
| 重大度 | メッセージで使用されるログの重大度。 |
| 件名 | メッセージで使用されるログの件名。 |
| コンテンツ | メッセージ本文を短くまとめた概要。 |

### ログイベントを送信

#### ログパラメーター

必須フィールド：

| **パラメーター** | **説明** |
| --- | --- |
| DD ソース | ログに関連付けられたインテグレーション名。Datadog がインテグレーション名を照合すると、対応するパーサーとファセットが自動的にインストールされます。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
| DD タグ | ログに関連付けられたタグ。 |
| ホスト名 | ログの送信元ホスト名。 |
| サービス | ログイベントを生成するアプリケーションまたはサービスの名前。`Logs` から `APM` への切り替えに使用されるため、両方の製品を使用する場合は、必ず同じ値を定義してください。詳細については、[Datadog：予約済み属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)を参照してください。 |
#### ログメッセージのパラメーター

ログの message [予約属性](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes)。デフォルトでは、Datadog は message 属性の値をログエントリの本文として取り込みます。この値はログストリームで強調表示され、全文検索用にインデックス化されます。

メッセージは、`[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]` という形式に基づいて構成されます。この形式を無視するには、**Message Override** パラメーターを使用します。

| **パラメーター** | **説明** |
| --- | --- |
| Message Override | メッセージ全体を渡すには、この属性をマッピングします。これにより、`message` 属性が上書きされます。 |
| Timestamp | ログのタイムスタンプ。このフィールドに値が入力されていない場合は、メッセージに現在のタイムスタンプが使用されます。 |
| Severity | メッセージで使用されるログの重大度。 |
| Subject | メッセージで使用されるログの件名。 |
| Content | メッセージ本文の短い要約。 |