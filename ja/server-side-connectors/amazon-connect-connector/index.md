---
title: AWS Amazon Connect コネクタ構成ガイド
description: この記事では、Amazon Connectコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-connect-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Amazon Connect
* APIバージョン：v1.0
* APIエンドポイント：`https://connect.{REGION}.amazonaws.com`
* ドキュメント：[Amazon Connect: StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html)

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **認証タイプ**：（必須）使用する認証のタイプ。
    * **アクセスキー**
        * **アクセスキー**：（必須）IAMユーザーのアクセスキーを提供してください。関連するIAMポリシー（IAMユーザーまたは仮定されたロール用）は、データを送信したいストリームに対して`kinesis:PutRecord`権限を付与する必要があります。
        * **シークレットキー**：（必須）IAMユーザーのシークレットキーを提供してください。
        * **リージョン**：（必須）使用しているAWS Connectのリージョンを選択してください。
    * **STS**
        * **STS - Assume Role: ARN**：（必須）仮定するロールに割り当てられたAmazonリソースネーム。詳細については、[IAMロールの切り替え](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
        * **STS - Assume Role: Session Name**：（必須）仮定されたロールセッションの一意の識別子。
        * **STS - Assume Role: External ID**：（オプション）第三者が顧客のアカウントでロールを仮定する際に使用する一意の識別子。詳細については、[AWS: 第三者が所有するAWSアカウントへのアクセス](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)を参照してください。
        * **リージョン**：（必須）使用しているAWS Connectのリージョンを選択してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Start Outbound Voice Contact | ✓ | ✓ |
| Update Profile Attributes | ✓ | ✓ |
| Update Profile Attributes (Batch) | ✓ | ✓ |

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### Start Outbound Voice Contact

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| Instance ID | （必須）Amazon Connectインスタンス識別子。 |
| Queue ID | 通話のキュー。キューを指定すると、発信者IDに表示される電話番号はキューで指定された電話番号です。キューを指定しない場合は、フローで定義されたキューが使用されます。**Queue ID**または**Source Phone Number**のいずれかが必要です。 |
| Source Phone Number | Amazon Connectインスタンスに関連付けられた電話番号（E.164形式）。**Queue ID**または**Source Phone Number**のいずれかが必要です。 |
| Contact Flow ID | （必須）発信通話のフローの識別子。 |

#### ベンダーパラメータ

| パラメータ | 説明 |
| --- | --- |
| Destination Phone Number | （必須）顧客の電話番号（E.164形式）。 |
| Campaign ID | 発信通信のキャンペーン識別子。値は1から100文字の長さである必要があります。 |
| Client Token | 重複したリクエストを防ぐための一意で大文字小文字を区別する識別子。提供されていない場合、AWS SDKがこのフィールドを埋めます。最大長は500文字です。 |
| Description | エージェントパネルの音声連絡説明。値は0から4096文字の長さである必要があります。 |
| Name | （必須）CCPに表示される音声連絡名。値は0から1024文字の長さである必要があります。 |
| Related Contact ID | タスク/チャットをリンクする関連`contactId`。値は1から256文字の長さである必要があります。 |
| Traffic Type | トラフィッククラス。可能な値：`GENERAL`または`CAMPAIGN`。 |

#### 留守番電話検出構成

| パラメータ | 説明 |
| --- | --- |
| Await Answer Machine Prompt | 留守番電話のプロンプトを待つかどうかを示すブール値。 |
| Enable Answer Machine Detection | 留守番電話検出が必要かどうかを示すブール値。`true`の場合、**Traffic Type**は`CAMPAIGN`でなければなりません。 |
| Attributes | 属性マップを使用したカスタムキーバリューペア。属性は標準のAmazon Connect属性であり、他の連絡先属性と同様にフローでアクセスできます。連絡先ごとにキーバリューペア全体で最大32,768 UTF-8バイトが可能です。属性キーには、英数字、ダッシュ、アンダースコアのみを含めることができます。 |

#### 参照

| パラメータ | 説明 |
| --- | --- |
| Type | 参照のタイプ。可能な値：`URL`, `NUMBER`, `STRING`, `DATE`, `EMAIL`。 |
| Value | 参照の有効な値。たとえば、Contact Control Panel (CCP)でエージェントに表示されるフォーマットされたURL。タイプが`DATE`の場合、値はUnix Epoch時間形式でなければなりません。 |

### Update Profile Attributes (Standard and Batched)

#### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするために、バッチリクエストを使用できます。リクエストは、次のいずれかの閾値が満たされるまでキューに入れられます：

* 最大リクエスト数：500
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：5 MB

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| Stream Name | （必須）データを送信するストリームを選択します。IAMポリシーが`kinesis:ListStreams`権限を付与していない場合は、カスタム値を手動で入力してください。 |
| Region Override | KinesisリージョンとConnectリージョンが異なる場合は、使用しているAWS Kinesisリージョンを選択します。 |

#### メッセージオプション

| パラメータ | 説明 |
| --- | --- |
| Partition Key | （必須）ストリーム内のどのシャードにデータレコードが割り当てられるかを決定します。 |
| Explicit Hash Key | （必須）データレコードが割り当てられるシャードを明示的に決定するために使用します。 |
| Sequence Number For Ordering | （必須）同じクライアントから同じパーティションキーへのメッセージに対して、厳密に増加するシーケンス番号を保証します。 |

#### メッセージデータ

| パラメータ | 説明 |
| --- | --- |
| Template Variables | （必須）テンプレートにデータ入力としてテンプレート変数を提供します。たとえば、`items.name`のようにドット表記でネストされたテンプレート変数を名前付けします。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。詳細および使用例については、を参照してください。|
| Templates | （必須）データセクションで参照されるテンプレートを提供します。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。たとえば、`{{SomeTemplateName}}`。詳細および使用例については、を参照してください。|