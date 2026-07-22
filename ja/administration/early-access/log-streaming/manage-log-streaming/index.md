---
title: ログストリーミングの管理
description: この記事では、ログストリーミングの送信先とログソースを構成、確認、管理する方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/log-streaming/manage-log-streaming/
---

<blockquote>
ログストリーミングはEarly Access中で、選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、Tealiumサポート担当者に連絡してください。
</blockquote>


## ログストリーミングを有効にする

1. **Server-Side Settings > Log Streaming**に移動します。
1. **Enable Log Streaming**をオンにします。
1. プロファイルを保存して公開します。

## 送信先を作成する

ログを受け取る各外部システムに対して一つの送信先を作成します。

例えば：
* モニタリングとアラート用にDatadog送信先を作成します。
* 長期保存と監査用にAmazon S3送信先を作成します。

送信先を作成するには：

1. 管理メニューで**Manage Log Streaming**をクリックします。
1. **+ New Destination**をクリックします。
1. コネクタを選択して**Next**をクリックします。
1. **Status**をオンにして送信先を有効にします。
1. 送信先の**Name**を入力します。
1. （オプション）送信先の説明として**Notes**を入力します。
1. 認証と接続構成を構成します。必要なフィールドは選択したコネクタによって異なります。
1. **Test Connection**をクリックして接続を確認します。
1. **Done**をクリックします。

各送信先には独自の構成要件があります。必要なフィールドとサポートされているパラメータについては、コネクタのドキュメントを参照してください。利用可能なコネクタのリストについては、[Available destination connectors](https://docs.tealium.com/about-log-streaming/#available-destination-connectors)を参照してください。

## ログソースを作成する


<blockquote>
ログストリーミングは、アウトバウンドイベントコネクタコールにカウントされます。使用事例に必要なコネクタとアクションのみを監視してください。
</blockquote>


ログソースを作成するには：

1. 次のいずれかを使用してログソースダイアログを開きます：
   * **Manage Log Streaming**テーブルから、送信先行で**+ New Source**をクリックします。
   * 送信先を選択し、**+ New Source**をクリックします。

1. **New Log Source**ダイアログで：
   1. **Log Source Name**を入力します。
   1. **Log Streaming Scope**を選択します：
      * **Send Entire Log Event**：ペイロードのすべてのログ属性を送信します。
      * **Send Log Event**：ペイロードのマップされた属性のみを送信します。
      
      利用可能なオプションが一つのみの場合、それがデフォルトで選択されます。詳細については、[Available destination connectors](https://docs.tealium.com/about-log-streaming/#available-destination-connectors)を参照してください。
   1. **Log Source Type**は**Connector Errors**に構成されます。
   1. 右側のサンプルペイロードを確認して、利用可能なフィールドを理解します。
   1. **Continue**をクリックします。

1. 監視するコネクタを選択します：
   1. リストから一つ以上のコネクタを選択します。
   1. ログに記録する内容を絞り込むには、コネクタで**Select Action Logs**をクリックします。

1. アクションレベルのログ記録を構成します（オプション）：
   1. **Select Actions to Log**ダイアログで、**Log Streaming Mode**を選択します：
      * **Send All**（コネクタレベルのログ記録）
        コネクタのすべてのアクションのエラーログを送信します。後で追加されたアクションも含まれます。
      * **Send Selected Actions**（アクションレベルのログ記録）
        選択したアクションのみのログを送信します。
   1. **Send Selected Actions**を使用する場合、監視するアクションを選択します。
   1. **Done**をクリックします。

1. コネクタの選択を保存するために**Done**をクリックします。

## イベント属性をベンダーパラメータにマッピングする

ログソースを構成した後、Tealiumのログ属性を送信先システムの必要なパラメータにマッピングします。ログソースの**Settings**タブで行います。

利用可能なベンダーパラメータについての情報は、[destination connector and action](https://docs.tealium.com/about-log-streaming/#available-destination-connectors)および[connector log parameters](https://docs.tealium.com/connector-error-logging/#connector-log-parameters)のドキュメントを参照してください。

### マッピングの仕組み

ログストリーミングは標準のイベント処理とは別のパイプラインで実行されます。訪問やイベントデータからの通常のイベント属性はログストリーミングアクションで利用できません。このため、ログパラメータの値はイベント属性に明示的に昇格させる必要があります。その後、それらを送信先のフィールドにマッピングできます。

マッピングには二つのステップがあります：

1. **イベント属性をエンリッチメントを使用して作成する**

   送信先に送りたい各ログフィールドに対して文字列イベント属性を作成します。その属性にログパラメータを値として持つ文字列構成エンリッチメントを追加します。二重中括弧を使用します。

   例えば、重大度レベルをマッピング可能にするために：
   
   * `dd_severity`という名前の文字列イベント属性を作成します。
   * 値として`{{severityText}}`を持つ文字列構成エンリッチメントを追加します。

   配信時に、エンリッチメントはログレコードから値を抽出してイベント属性に書き込みます。

   利用可能なログパラメータの完全なリストについては、[Connector log parameters](https://docs.tealium.com/connector-error-logging/#connector-log-parameters)を参照してください。

1. **イベント属性をベンダーパラメータにマッピングする**

   ログソースの構成で、イベント属性を適切なベンダーパラメータにマッピングします。利用可能なパラメータは使用している送信先コネクタに依存します。

   例えば、Datadogの**Send Log Event**ログソース構成で、イベント属性`dd_severity`をDatadogの**Severity**パラメータにマッピングします。

### マッピング例（Datadog）

以下の例は、Datadog送信先の属性構造を示しています：

| イベント属性 | 文字列構成エンリッチメント |
| --- | --- |
| `dd_tags` | `account:{{account}},profile:{{profile}},connector:{{connectorType}},action_id:{{customId}},status:{{result.status}},error_code:{{result.failure.code.name}},http_status:{{http.0.response.statusCode}},group_id:{{groupId}}` |
| `dd_subject` | `{{result.failure.code.name}}` |
| `dd_content` | `{{result.failure.error.0.message}}` |
| `dd_severity` | `{{severityText}}` |

その後、これらのイベント属性をログソースの**Settings**タブでベンダーパラメータにマッピングします：

| イベント属性 | ベンダーパラメータ |
| --- | --- |
| `tealium_connector_errors` | DD Source |
| `dd_tags` | DD Tags |
| `tealium_server_side` | Hostname |
| `tealium_connectors` | Service |
| `tealium_timestamp_epoch` | Timestamp |
| `dd_subject` | Subject |
| `dd_content` | Content |
| `dd_severity` | Severity |

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-mapping-attributes.png)

ログソースビューのサンプルペイロードを使用して、参照しているフィールドが存在し、期待される値を含んでいることを確認します。

完全なパラメータ定義については、[Connector log parameters](https://docs.tealium.com/connector-error-logging/#connector-log-parameters)を参照してください。

## 配信を確認する

送信先とログソースを構成した後：

* ログが送信先システムに到着していることを確認します。
* フィールドが正しくマッピングされているかを検証します。
* フィールドが欠落している場合や誤ってフォーマットされている場合は、マッピングを調整します。

Tealiumでは、ログストリーミングダッシュボードを使用して、ログが正常に送信されていることを確認します。

## ログストリーミング活動を監視する

**Manage Log Streaming**ページを使用して、配信パフォーマンスを監視し、送信先を管理します。

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-manage-table.png)

### 概要メトリック

概要セクションでは、選択した時間範囲の配信メトリックを表示します。

* **Total Volume**：送信されたログイベントの数
* **Retries**：再試行の回数
* **Total Success**：正常に配信されたイベント
* **Success after Retry**：一回以上の再試行後に配信されたイベント
* **Total Errors**：配信に失敗したイベント

これらのメトリックは、コネクタの実行ではなく、ログ配信パイプラインの健全性を反映しています。

エラーの数が多い場合は、通常、以下のような問題を示しています：

* 認証の失敗
* 接続問題
* 送信先の構成エラー


### 宛先テーブル

**ログストリーミング宛先**テーブルは、構成されたすべての宛先とその配信パフォーマンスを一覧表示します。

各行には以下が表示されます：

* **ソース**: 宛先に接続されたログソースの数
* **総ボリューム / 成功 / エラー**: 宛先の配信メトリクス
* **更新日**: 宛先が最後に更新された日時
* **ラベル**: 宛先に適用されたラベル
* **ステータス**: 宛先がアクティブかどうか

このテーブルを使用して、ボリュームやエラーに異常なパターンを特定し、さらに調査するための宛先を選択します。

### 宛先の詳細を表示

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-destination-details-overview.png)

宛先を選択してその詳細を開きます。以下のタブを使用します：

* **概要**: 配信トレンドチャート、要約統計、および基本情報（名前、メモ、UID、ラベル）。統計とトレンドチャートをフィルタリングするための期間を選択します。
* **ログソース**: この宛先に接続されたログソース、タイプ、ステータス、および各ソースの統計（総ボリューム、成功、エラー）。個々のソースを複製または削除するオプションが含まれます。
* **構成**: コネクタ構成（認証フィールド、ID、接続パラメータ）

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-destination-log-sources-table.png)

### ログソースの詳細を表示

ログソースを選択してその詳細を開きます。以下のタブを使用します：

* **概要**: 配信トレンドチャートと要約統計。統計をフィルタリングするための期間を選択します。
* **コネクタ**: このログソースによって監視されるコネクタとアクション。
* **構成**: 属性マッピングとサンプルペイロード。ログソース間でマッピングを再利用するには、[マッピングのコピー](#copy-mappings)を参照してください。

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-log-source-details-payload.png)

サンプルペイロードを使用して、マッピングで参照するフィールドが存在し、期待される値を含んでいることを確認します。

## マッピングのコピー

**マッピングのコピー**を使用して、ログソース間で構成を再利用します。

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-copy-mappings.png)

1. ログソースを開きます。
1. **構成**タブに移動します。
1. **マッピングのコピー**をクリックします。
1. 次のいずれかを選択します：
   * **アクションからマッピングを挿入**: 選択したアクションから現在のアクションにマッピングをコピーします。
   * **アクションへマッピングをコピー**: 現在のアクションから選択したアクションにマッピングをコピーします。
1. 競合の取り扱い方法を選択します：
   * **元のマッピングを保持**: ソースからの新しいマッピングを追加し、宛先の既存のマッピングを変更しません。
   * **すべてのマッピングを上書き**: 宛先のすべての既存のマッピングをソースアクションのもので置き換えます。
1. アクションのリストを絞り込むためにフィルターを適用するか、検索を行い、アクションを選択します。
1. **完了**をクリックします。


<blockquote>
同じログソースを複数の宛先に送信したい場合は、追加の宛先を作成し、ログソースを追加してから、マッピングのコピー機能を使用して、あるログソースから他のログソースへマッピングを複製します。
</blockquote>


## 関連リソース

* [コネクタエラーロギング](https://docs.tealium.com/connector-error-logging/)
* [エンリッチメントについて](https://docs.tealium.com/about-enrichments/)
* [ログストリーミングについて](https://docs.tealium.com/about-log-streaming/)