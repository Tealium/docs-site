---
title: Adobe Campaign Standardコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAdobe Campaign Standardコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-standard-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|トランザクションイベントを送信| ✓| ✗|
|シグナルアクティビティをトリガー| ✓| ✗|
|プロファイルを作成または更新| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **テクニカルアカウントID**
  * テクニカルアカウントIDは、[Adobe I/O Console](https://console.adobe.io/)で確認できます。
  * 詳細については、[Adobe Experience Platform APIの認証とアクセス](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#login-to-adobe-io-console)を参照してください。

* **組織ID**
  * 組織IDは、[Adobe I/O Console](https://console.adobe.io/)で確認できます。

* **テナントID**
  * テナントIDは、Adobe Marketing CloudのURLで確認できます。
  * 例：<https://yourtenantid.experiencecloud.adobe.com/campaign.html>

* **APIキー**
  * APIキー（クライアントID）は、[Adobe I/O Console](https://console.adobe.io/)で確認できます。

* **シークレットキー**
  * クライアントシークレットは、[Adobe I/O Console](https://console.adobe.io/)で確認できます。

* **秘密鍵**
  * 秘密鍵は、Adobe Consoleでインテグレーションを作成する際に生成されます。
  * 詳細については、[Adobe Experience Platform APIの認証とアクセス](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#create-integration)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - トランザクションイベントを送信

トランザクションイベントを送信するには、最初にイベントを作成して構成する必要があります。詳細については、[トランザクションイベントの構成](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/transactional-messaging/event-configuration/configuring-transactional-event.html)および[トランザクションメッセージの管理](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-transactional-messages.html)を参照してください。

トランザクションイベントの送信に使用されるAPIエンドポイントは、構成によって異なります。

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メールアドレス|  <ul><li>（必須）受信者のメールアドレス。</li></ul> |
|イベントID|  <ul><li>（必須）送信するイベントのタイプ。</li><li>このIDは、イベント定義の作成時に生成されます。</li><li>詳細については、[Adobe Campaignドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html)を参照してください。</li></ul> |
|有効期限|  <ul><li>（任意）この日付を過ぎると、トランザクションイベントの送信がキャンセルされます。</li></ul> |
|送信予定日時|  <ul><li>（任意）この日時にトランザクションイベントが処理され、トランザクションメッセージが送信されます。</li></ul> |
|テンプレート名|  <ul><li>テンプレートを使用してデータを渡す場合は、「トランザクションメッセージコンテンツテンプレート」に入力し、メインテンプレートの名前を指定します。</li><li>名前に二重波括弧を含めないでください。たとえば、`{{SomeTemplateName}}`ではなく`SomeTemplateName`を使用します。</li></ul> |
|テンプレート変数|  <ul><li>「トランザクションメッセージコンテンツテンプレート」のデータ入力としてテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット記法で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|トランザクションメッセージコンテンツテンプレート|  <ul><li>拡張されたトランザクションメッセージのコンテンツを記述するテンプレート。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li><li>拡張メッセージコンテンツの使用に関する詳細については、Adobeの[Campaignドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html)を参照してください。</li></ul> |
| トランザクションAPIエンドポイント |  <ul><li>（任意）コネクタ構成のテナントIDの前に「`mc`」を付けたデフォルト値を上書きする場合に指定します。</li><li>これは通常、ステージインスタンスで作業する場合に適用されます。</li><li>例：ステージのテナントIDが「`geometrixx-mkt-stage3`」の場合、トランザクションAPIエンドポイントを「`geometrixx`」に上書きします。</li></ul> |

### アクション - シグナルアクティビティをトリガー

詳細については、Adobeドキュメントの[シグナルアクティビティのトリガー](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-workflows/triggering-a-signal-activity.html)を参照してください。

シグナルアクティビティをトリガーするには、RESTワークフロー／実行APIを使用します。

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ワークフローID|  <ul><li>Adobe Consoleで構成されたワークフローのID。</li></ul> |
|ソース|  <ul><li>トリガーリクエストの送信元を示すために使用します。</li></ul> |
|パラメータマップ|  <ul><li>パラメータを指定してワークフローを呼び出すことができます。</li><li>パラメータの値をその名前にマッピングします。</li><li>文字列、数値、ブール値、および日付／時刻の各タイプがサポートされています。</li></ul> |

### アクション - プロファイルを作成または更新

プロファイルを取得、作成、または更新するため、Adobe ProfileAndServices APIにリクエストが送信されます。

詳細については、[APIを使用したプロファイルの作成](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/creating-profiles-api.html)、[APIを使用したプロファイルの更新](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/updating-profiles.html)、および[APIを使用したプロファイルの取得](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/retrieving-profiles.html?lang=en)を参照してください。
##### パラメーター

|**パラメーター**| **説明**|
|---| ---|
|更新方法| <ul><li>（必須）適用する更新方法を選択します。<ul><li>**作成のみ** — 既存のプロファイルを検索し、見つからない場合は新しいプロファイルを作成します。</li><li>**更新のみ** — 既存のプロファイルを検索して更新します。</li><li>**作成または更新** — 既存のプロファイルを検索し、見つかった場合は更新し、それ以外の場合は新しいプロファイルを作成します。</li></ul></li></ul> |
|フィルター| <ul><li>更新方法が**作成または更新**または**更新のみ**の場合は必須です。</li><li>一意の結果を返すフィルターを選択することを強く推奨します。</li><li>詳細については、[複合識別キー](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en)を参照してください。</li><li>検索結果で複数のプロファイルが返された場合、最初のプロファイルのみが更新されます。</li></ul> |
|カスタムフィルターかどうか| <ul><li>[カスタムフィルターについて](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)を参照してください。</li></ul> |
|テンプレート変数| <ul><li>テンプレート変数をデータ入力として指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット記法で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|テンプレート| <ul><li>本文データで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。</li><li>例：`{{SomeTemplateName}}`</li></ul> |