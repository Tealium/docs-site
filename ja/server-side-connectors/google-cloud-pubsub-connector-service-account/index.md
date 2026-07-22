---
title: Google Cloud Pub/Sub コネクタ構成ガイド
description: この記事では、Google Cloud Pub/Sub コネクタの構成方法について説明します。Tealiumでは、コネクタマーケットプレイスで2種類のPub/Subコネクタを提供しています：Google Cloud Pub/Sub コネクタ（3-legged OAuth）と Google Cloud Pub/Sub（サービスアカウント）コネクタ（2-legged OAuth）。
url: https://docs.tealium.com/ja/server-side-connectors/google-cloud-pubsub-connector-service-account/
---
## 前提条件

### Google Cloud Pub/Sub コネクタ

このコネクタは、クライアントIDとシークレットが必要な三者間OAuthフローを使用して認証を行います。このコネクタを構成する前に、以下の手順を完了してください：

1. Google CloudプロジェクトでウェブアプリケーションタイプのOAuthクライアントIDクレデンシャルを作成します。
1. Google Cloudのウェブアプリケーション構成を更新して、Tealiumサーバーを許可リストに追加し、接続成功時に必要なコールバックを提供します。Google Cloudコンソールで**認証情報**に移動し、OAuthクライアントID構成を以下の値で編集します。各選択について、TealiumインスタンスのURLに使用されるサブドメインに応じて値を追加します。
    * 認可されたJavaScriptの起源：
      * `https://my.tealiumiq.com`
      * `https://my.tealiumiq.com`
      * `https://[privatecloud subdomain].tealiumiq.com`
    * 認可されたリダイレクトURI：
      * `https://my.tealiumiq.com/oauth/google/callback.html`
      * `https://my.tealiumiq.com/oauth/google/callback.html`
      * `https://[private cloud subdomain].tealiumiq.com/oauth/google/callback.html`
1. コネクタ構成に使用する以下の構成情報をメモしておきます：
    * プロジェクトID
    * クライアントID
    * クライアントシークレット

### Google Cloud Pub/Sub（サービスアカウント）コネクタ

このコネクタは、Google Cloudのサービスアカウントを使用した二者間OAuthフローを使用します。コネクタを構成する前に、Google CloudプロジェクトでPub/Subパブリッシャーの役割を持つサービスアカウントを作成します。サービスアカウントの作成についての詳細は、Google Cloudのドキュメント[アクセス制御に関するIAM](https://cloud.google.com/pubsub/docs/access-control)を参照してください。サービスアカウントを作成した後、コネクタ構成に使用する以下の構成情報をメモしておきます：

* プロジェクトID
* サービスアカウントのメール
* サービスアカウントキー

## 構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、追加したコネクタに基づいて以下の構成を構成します：

### Google Cloud Pub/Sub コネクタ

* **Google Cloud Platform プロジェクトID**  
(必須) あなたのGoogle Cloud PlatformプロジェクトID。
* **クライアントID**  
(必須) あなたのGoogle CloudプロジェクトにあるウェブアプリケーションタイプのOAuthクライアントID。
* **クライアントシークレット**  
(必須) あなたのGoogle Cloudプロジェクトで割り当てられたクライアントシークレットを入力します。

### Google Cloud Pub/Sub（サービスアカウント）コネクタ

* **Google Cloud Platform プロジェクトID**  
(必須) あなたのGoogle Cloud PlatformプロジェクトID。
* **クライアントメール**  
(必須) あなたのGoogle Cloudプロジェクトで使用されるサービスアカウントのメールアドレス。
* **プライベートキー**  
(必須) あなたのGoogle Cloudプロジェクトのサービスアカウントに生成されたプライベートキー。

## アクション

### Google Cloud Pub/Sub コネクタ

| アクション名 | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| トピックへのイベントデータ送信 | ✗ | ✓ |
| トピックへの訪問データ送信 | ✓ | ✗ |
| トピックへのカスタマイズデータ送信（高度） | ✓ | ✓ |
| トピックへのログイベント送信 | ✓ | ✓ |

### Google Cloud Pub/Sub（サービスアカウント）コネクタ

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| トピックへのイベントデータ送信 | ✗ | ✓ |
| カスタムURLでのイベントデータ送信 | ✗ | ✓ |
| トピックへの訪問データ送信 | ✓ | ✗ |
| トピックへのカスタマイズデータ送信（高度） | ✓ | ✓ |
| トピックへのログイベント送信 | ✓ | ✓ |


<blockquote>
パブリッシュするPub/Subトピックにスキーマが添付されている場合は、**トピックへのカスタマイズデータ送信**アクションを使用して、スキーマに一致する厳格なJSON定義を指定してください。
</blockquote>


### トピックへのイベントデータ送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|プロジェクトトピック| (必須) メッセージを公開するPub/Subプロジェクトのトピックを選択します。 |
|メッセージ属性| カスタムPub/Subメッセージ属性に属性値をマッピングします。**To**ドロップダウンリストでメッセージ属性キーを入力します。 |
|属性名の印刷| 属性名が更新された場合、ペイロードの名前は公開されたメッセージで更新された名前を自動的に反映します。|
|オーダリングキー|オーダリングキー値をマッピングまたは入力して、Pub/Subトピックのサブスクライバーが公開された順序でメッセージを受信できるようにします。詳細については、[Google: メッセージの順序](https://cloud.google.com/pubsub/docs/ordering)を参照してください。|

### トピックへの訪問データ送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|プロジェクトトピック|(必須) メッセージを公開するPub/Subプロジェクトのトピックを選択します。 |
|メッセージ属性|カスタムPub/Subメッセージ属性に属性値をマッピングします。**To**ドロップダウンリストでメッセージ属性キーを入力します。 |
|現在の訪問データを含む| このボックスをチェックすると、公開されたメッセージに訪問データと現在の訪問データの両方が含まれます。 |
|属性名の印刷| 属性名が更新された場合、ペイロードの名前は公開されたメッセージで更新された名前を自動的に反映します。 |
|オーダリングキー|オーダリングキー値をマッピングまたは入力して、Pub/Subトピックのサブスクライバーが公開された順序でメッセージを受信できるようにします。詳細については、[Google: メッセージの順序](https://cloud.google.com/pubsub/docs/ordering)を参照してください。|

### トピックへのカスタマイズデータ送信（高度）

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|プロジェクトトピック|(必須) メッセージを公開するPub/Subプロジェクトのトピックを選択します。 |
| メッセージデータ|(必須) メッセージデータを構築するための値を提供します。テンプレートサポートの場合は、テンプレート名を参照してメッセージデータを生成します。値を単純な1レベルのJSON形式の名前にマッピングするか、テンプレート名を参照して**カスタムメッセージ定義**オプションのみを選択します。|
|メッセージ属性| カスタムPub/Subメッセージ属性に属性値をマッピングします。**To**ドロップダウンリストでメッセージ属性キーを入力します。|
|テンプレート変数|テンプレートにデータ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。例えば、`items.name`のようにドット表記でネストされたテンプレート変数を名前付けします。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。|
|テンプレート| メッセージ属性またはデータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。例えば、`{{SomeTemplateName}}`。
|オーダリングキー|オーダリングキー値をマッピングまたは入力して、Pub/Subトピックのサブスクライバーが公開された順序でメッセージを受信できるようにします。詳細については、[Google: メッセージの順序](https://cloud.google.com/pubsub/docs/ordering)を参照してください。|

### トピックへのログイベント送信

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| プロジェクトトピック | (必須) ログイベントを送信するトピックを選択します。 |
| メッセージ属性 | (オプション) メッセージ属性に値をマッピングします。 |

### カスタムURLでのイベントデータ送信

| **パラメータ** | **説明** |
| --- | --- |
| URLオーバーライド | (必須) データを送信するカスタム`URL`を入力します。 |
| メッセージ属性 | メッセージ属性に値をマッピングします |
| 属性名の印刷 | 属性名が更新された場合、ペイロードは更新を反映します。 |
|オーダリングキー|オーダリングキー値をマッピングまたは入力して、Pub/Subトピックのサブスクライバーが公開された順序でメッセージを受信できるようにします。詳細については、[Google: メッセージの順序](https://cloud.google.com/pubsub/docs/ordering)を参照してください。|


## ベンダー文書

* [Pub/Sub: Pub/Subとは何ですか？](https://cloud.google.com/pubsub/docs/overview)
* [サーバー間の本番アプリケーションの認証構成](https://cloud.google.com/docs/authentication/production#obtaining_and_providing_service_account_credentials_manually)