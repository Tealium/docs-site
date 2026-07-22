---
title: Adobe Campaign Standard コネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Adobe Campaign Standard コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-standard-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|トランザクショナルイベントを送信| ✓| ✗|
|シグナルアクティビティをトリガー| ✓| ✗|
|プロファイルの作成または更新| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/) の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **テクニカルアカウントID**
  * テクニカルアカウントIDは [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。
  * 詳細については、[Adobe Experience Platform API への認証とアクセス](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#login-to-adobe-io-console) を参照してください。

* **組織ID**
  * 組織IDは [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。

* **テナントID**
  * テナントIDは、Adobe Marketing Cloud URL で見つけることができます。
  * 例：<https://yourtenantid.experiencecloud.adobe.com/campaign.html>

* **APIキー**
  * APIキー（クライアントID）は [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。

* **シークレットキー**
  * クライアントシークレットは [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。

* **プライベートキー**
  * プライベートキーは、Adobe コンソールでインテグレーションを作成する際に生成されます。
  * 詳細については、[Adobe Experience Platform API への認証とアクセス](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#create-integration) を参照してください。

## アクション構成 - パラメータとオプション

**次へ** をクリックするか、**アクション** タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - トランザクショナルイベントを送信

トランザクショナルイベントを送信するには、まずイベントを作成して構成する必要があります。詳細については、[トランザクショナルイベントの構成](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/transactional-messaging/event-configuration/configuring-transactional-event.html) および [トランザクショナルメッセージの管理](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-transactional-messages.html) を参照してください。

トランザクショナルイベントを送信するために使用する API エンドポイントは、構成によって異なります。

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email|  <ul><li>必須。</li><li>受信者のメールアドレス。</li></ul> |
|Event ID|  <ul><li>必須。</li><li>送信したいイベントのタイプ。</li><li>このIDはイベント定義を作成する際に生成されます。</li><li>追加情報については、[Adobe Campaign ドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html) を参照してください。</li></ul> |
|Expiration Date|  <ul><li>オプション。</li><li>この日付後にトランザクショナルイベントの送信がキャンセルされます。</li></ul> |
|Scheduled Send Date|  <ul><li>オプション。</li><li>この日付にトランザクショナルイベントが処理され、トランザクショナルメッセージが送信されます。</li></ul> |
|Template Name|  <ul><li>データを渡すためにテンプレートを使用する場合、「Transactional Message Content Template」と入力し、メインテンプレートの名前を入力します。</li><li>名前に二重中括弧を含めないでください。例えば、`SomeTemplateName` を使用し、`{{SomeTemplateName}}` は使用しないでください。</li></ul> |
|Template Variables|  <ul><li>「Transactional Message Content Template」のデータ入力用にテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数の名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|Transactional Message Content Template|  <ul><li>エンリッチされたトランザクショナルメッセージコンテンツを記述するテンプレート。</li><li>テンプレートは、サポートされているフィールドに名前で二重中括弧を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li><li>エンリッチされたメッセージコンテンツの使用についての追加情報は、Adobeの [Campaign ドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html) を参照してください。</li></ul> |
| Transactional API Endpoint |  <ul><li>オプション。</li><li>デフォルト値 "`mc`" に続くコネクタ構成からのテナントIDを上書きするために指定します。</li><li>これは通常、ステージインスタンスで作業する場合に適用されます。</li><li>例：ステージテナントIDが "`geometrixx-mkt-stage3`" の場合、Transactional API Endpoint を "`geometrixx`" に上書きします。</li></ul> |

### アクション - シグナルアクティビティをトリガー

詳細については、Adobeのドキュメントの [シグナルアクティビティのトリガー](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-workflows/triggering-a-signal-activity.html) を参照してください。

シグナルアクティビティをトリガーするには、RESTワークフロー/実行APIが使用されます。

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Workflow ID|  <ul><li>Adobeコンソールで構成されたワークフローのID。</li></ul> |
|Source|  <ul><li>トリガーリクエストのソースを示すために使用されます。</li></ul> |
|Parameter Map|  <ul><li>パラメータを使用してワークフローを呼び出すことが可能です。</li><li>パラメータの値をその名前にマップします。</li><li>String、Number、Boolean、および Date/Time タイプがサポートされています。</li></ul> |

### アクション - プロファイルの作成または更新

プロファイルを取得、作成、または更新するためには、Adobe ProfileAndServices APIにリクエストが送信されます。

詳細については、[APIを使用したプロファイルの作成](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/creating-profiles-api.html)、[APIを使用したプロファイルの更新](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/updating-profiles.html)、および [APIを使用したプロファイルの取得](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/retrieving-profiles.html?lang=en) を参照してください。
##### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新戦略|  <ul><li>必須</li><li>適用可能な更新戦略を選択します。<ul><li>**新規作成のみ** — 既存のプロファイルを検索し、見つからない場合は新しいプロファイルを作成します。</li><li>**更新のみ** — 既存のプロファイルを検索して更新します。</li><li>**新規作成または更新** — 既存のプロファイルを検索し、見つかった場合は更新し、そうでない場合は新しいプロファイルを作成します。</li></ul> </li></ul> |
|フィルタ|  <ul><li>更新戦略が **新規作成または更新** または **更新のみ** の場合は必須です。</li><li>一意の結果を返すフィルタを選択することを強く推奨します。</li><li>詳細については、こちらを参照してください：[複合識別キー](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en)。</li><li>検索結果が複数のプロファイルを返した場合、最初のプロファイルのみが更新されます。</li></ul> |
|カスタムフィルタ|  <ul><li>[カスタムフィルタについて](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)を参照してください。</li></ul> |
|テンプレート変数|  <ul><li>データ入力としてテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数に名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。</li></ul> |
|テンプレート|  <ul><li>本文データで参照されるテンプレートを提供します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で指定され、サポートされるフィールドに二重波括弧で注入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |
