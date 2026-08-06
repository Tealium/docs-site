---
title: ログストリーミングについて
description: この記事では、Tealiumシステムログを外部の監視、保存、およびアラートプラットフォームにルーティングするためのログストリーミングの使用方法について説明します。
url: https://docs.tealium.com/ja/administration/log-streaming/about/
---
## 概要

ログストリーミングは、Tealiumのログを既存の監視、保存、およびアラートプラットフォームにルーティングし、既に使用しているツールでシステムの動作を監視できます。

ログストリーミングを使用して：

* 中央の場所でコネクタの信頼性を監視します。
* 詳細なログレコードで障害を調査します。
* 目的地プラットフォームでダッシュボードとアラートを構築します。
* 保持またはコンプライアンスのニーズのために自分のシステムにログを保存します。

## 要件

**サーバーサイド構成**でログストリーミングが有効になっています。詳細については、[ログストリーミングを有効にする](https://docs.tealium.com/manage-log-streaming/#enable-log-streaming)を参照してください。

## 動作原理

ログストリーミングは、主に以下の2つのコンポーネントを使用します：

### 宛先

宛先はログエントリが送信される場所を定義します。各宛先はコネクタによってバックアップされ、専用のログストリーミングアクションを使用してログデータを外部システムに配信します。

ログストリーミング宛先はログストリーミングUIで構成され、標準コネクタ画面で構成されたコネクタとは別です。

例としては、DatadogやNew Relicのような監視プラットフォーム、Amazon S3のような保存システム、Confluent Kafkaのようなストリーミングプラットフォームがあります。さらに多くの例については、を参照してください。

### ログソース

ログソースは、どのログが収集され、配信前にどのようにグループ化されるかを定義します。各ログソースはログタイプを指定し、どのコネクタまたはアクションが監視されるかを制御します。ログソースインスタンスは単一の宛先に紐づけられています。同じログを複数の宛先に送信するには、別々のログソースインスタンスを作成します。

ログソースがログエントリを生成すると、次のプロセスが発生します：

1. ログソースがイベントをキャプチャします。
1. ログソースは、コネクタタイプ、HTTPレスポンスステータス、エラーコード、実行時間などのフィールドを含む構造化されたレコードを組み立てます。
1. レコードは関連する宛先に転送されます。
1. 宛先コネクタはログエントリを外部プラットフォームに配信します。
1. 外部プラットフォームはログを監視、分析、アラート、または長期保持のために取り込みます。

たとえば、優先度の高いキャンペーンのコネクタエラーを監視し、それらのログをDatadogに送信して、チームが障害を確認し、エラー数が増加したときにアラートをトリガーすることができます。

ログストリーミングはコネクタを通じてログを配信し、Tealium内でログを保存または分析しません。

## 利点

* **コネクタエラーに関する外部からの可視性**  
コネクタエラー情報はデフォルトでTealium UI内でのみ利用可能です。ログストリーミングはそれらのエラーを監視スタックにルーティングするため、Tealiumにログインせずにチームがそれらを監視できます。
* **プログラムによる分析のための構造化データ**  
各ログレコードには、HTTPステータスコード、エラータイプ、実行時間などのフィールドが含まれています。これらのフィールドを使用してエラーを分類し、ノイズをフィルタリングし、目的地プラットフォームでターゲットを絞ったアラートを構築します。
* **相関監視**  
インフラの残りの部分を監視している同じプラットフォームにコネクタエラーを送信し、Tealiumの障害をより広範なシステムイベントと相関させます。
* **長期的なエラー履歴**  
Tealiumは歴史的なエラーデータを保持しません。ログを自分のシステムに保存することで、監査、コンプライアンス、またはトレンド分析のための永続的な記録を提供します。
* **選択的なフィールド配信**  
Send Log Eventアクションを使用して、宛先に到達するフィールドを制御し、使用ケースに関連するものだけを転送します。

## 利用可能な宛先コネクタ

ログエントリを送信するために以下のコネクタを使用します：

| コネクタ | Send Log Event | Send Entire Log Event |
|---| :---: | :---: |
| [Amazon Redshift](https://docs.tealium.com/amazon-redshift-connector/) | ✓ | ✓ |
| [Amazon S3](https://docs.tealium.com/amazon-s3-connector/) | ✓ | ✓ |
| [AWS Firehose](https://docs.tealium.com/aws-firehose-connector/) | ✓ | ✗ |
| [AWS Firehose (Tealium Provided Credentials)](https://docs.tealium.com/aws-firehose-tealium-provided-credentials-connector/) | ✓ | ✗ |
| [Confluent Kafka Connect](https://docs.tealium.com/confluent-kafka-connect-connector/) | ✓ | ✓ |
| [Datadog](https://docs.tealium.com/datadog-connector/) | ✓ | ✗ |
| [File Transfer Protocol (SFTP, FTPS)](https://docs.tealium.com/ftp-connector/) | ✓ | ✓ |
| [Google BigQuery](https://docs.tealium.com/google-bigquery-connector/) | ✓ | ✓ |
| [Google Cloud Pub/Sub](https://docs.tealium.com/google-cloud-pubsub-connector-service-account/) | ✓ | ✗ |
| [Google Cloud Storage](https://docs.tealium.com/google-cloud-storage-connector/) | ✓ | ✓ |
| [Microsoft Fabric Eventhouse](https://docs.tealium.com/microsoft-fabric-eventhouse-connector/) | ✓ | ✓ |
| [New Relic](https://docs.tealium.com/new-relic-connector/) | ✓ | ✓ |
| [Splunk](https://docs.tealium.com/splunk-connector/) | ✓ | ✓ |
| [Webhook JDBC](https://docs.tealium.com/webhook-jdbc/) | ✓ | ✓ |

各宛先は、2つのログストリーミングアクションのいずれかを使用します：

* **Send Entire Log Event**  
利用可能なすべてのログ属性を単一のペイロードで宛先に送信します。初期構成中に完全なデータ構造を確認し、使用ケースに関連するフィールドを特定するためにこのアクションを使用します。
* **Send Log Event**  
コネクタアクション構成で明示的にマッピングした属性のみを送信します。ペイロードにはマッピングされた属性のみが含まれます。宛先に到達するフィールドを制御するために、本番環境でこのアクションを使用します。詳細については、[イベント属性をベンダーパラメータにマッピングする](https://docs.tealium.com/manage-log-streaming/#map-event-attributes-to-vendor-parameters)を参照してください。

## 利用可能なログソース

以下のログソースタイプがサポートされています：

* [Connector Errors](https://docs.tealium.com/connector-error-logging/)  
コネクタアクションによって生成されるエラーログ。これらのログには、エラーコード、実行ステータス、タイムスタンプ、トラブルシューティングに使用される識別子などの詳細が含まれています。

## ワークフロー

始める前に、監視するコネクタとアクション、ログを受け取る外部プラットフォームを決定します。


<blockquote>
ログストリーミングは、アウトバウンドイベントコネクタの呼び出しにカウントされます。使用ケースに必要なコネクタとアクションのみを監視してください。
</blockquote>


1. [宛先を作成する](https://docs.tealium.com/manage-log-streaming/#create-a-destination)ログを受け取る各外部システム用。
1. [ログソースを作成する](https://docs.tealium.com/manage-log-streaming/#create-a-log-source)監視するコネクタとアクションを定義します。
1. [イベント属性をベンダーパラメータにマッピングする](https://docs.tealium.com/manage-log-streaming/#map-event-attributes-to-vendor-parameters)ログフィールド値を抽出するためのエンリッチメントを作成し、それらの属性を宛先固有のパラメータにマッピングします。
1. 宛先システムに正しくマッピングされたフィールドでログレコードが到着することを確認します。
1. **ログストリーミングの管理**ページを使用してログストリーミング活動を監視します。配信メトリックは、監視されているコネクタ操作の健全性ではなく、ログ配信パイプラインの健全性を反映します。

ログでキャプチャされたコネクタエラーのトラブルシューティングについては、[コネクタエラーログ](https://docs.tealium.com/connector-error-logging/#use-logs-to-troubleshoot-connector-errors)を参照してください。

## 次のステップ

* [ログストリーミングを管理する](https://docs.tealium.com/manage-log-streaming/)
* [コネクタエラーログ](https://docs.tealium.com/connector-error-logging/)