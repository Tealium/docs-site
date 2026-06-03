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

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]() の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **テクニカルアカウントID**
  * テクニカルアカウントIDは [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。
  * 詳細については、[Adobe Experience Platform API への認証とアクセス](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#login-to-adobe-io-console) を参照してください。

* **組織ID**
  * 組織IDは [Adobe I/O コンソール](https://console.adobe.io/) で見つけることができます。

* **テナントID**
  * テナントIDは、Adobe Marketing Cloud URL で見つけることができます。
  * 例：&lt;https://yourtenantid.experiencecloud.adobe.com/campaign.html&gt;

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
|Email|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;受信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|Event ID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;送信したいイベントのタイプ。&lt;/li&gt;&lt;li&gt;このIDはイベント定義を作成する際に生成されます。&lt;/li&gt;&lt;li&gt;追加情報については、[Adobe Campaign ドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html) を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Expiration Date|  &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;この日付後にトランザクショナルイベントの送信がキャンセルされます。&lt;/li&gt;&lt;/ul&gt; |
|Scheduled Send Date|  &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;この日付にトランザクショナルイベントが処理され、トランザクショナルメッセージが送信されます。&lt;/li&gt;&lt;/ul&gt; |
|Template Name|  &lt;ul&gt;&lt;li&gt;データを渡すためにテンプレートを使用する場合、「Transactional Message Content Template」と入力し、メインテンプレートの名前を入力します。&lt;/li&gt;&lt;li&gt;名前に二重中括弧を含めないでください。例えば、`SomeTemplateName` を使用し、`{{SomeTemplateName}}` は使用しないでください。&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;「Transactional Message Content Template」のデータ入力用にテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、 を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数の名前を付けます。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|Transactional Message Content Template|  &lt;ul&gt;&lt;li&gt;エンリッチされたトランザクショナルメッセージコンテンツを記述するテンプレート。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされているフィールドに名前で二重中括弧を使用して挿入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;li&gt;エンリッチされたメッセージコンテンツの使用についての追加情報は、Adobeの [Campaign ドキュメント](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html) を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Transactional API Endpoint |  &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;デフォルト値 &#34;`mc`&#34; に続くコネクタ構成からのテナントIDを上書きするために指定します。&lt;/li&gt;&lt;li&gt;これは通常、ステージインスタンスで作業する場合に適用されます。&lt;/li&gt;&lt;li&gt;例：ステージテナントIDが &#34;`geometrixx-mkt-stage3`&#34; の場合、Transactional API Endpoint を &#34;`geometrixx`&#34; に上書きします。&lt;/li&gt;&lt;/ul&gt; |

### アクション - シグナルアクティビティをトリガー

詳細については、Adobeのドキュメントの [シグナルアクティビティのトリガー](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-workflows/triggering-a-signal-activity.html) を参照してください。

シグナルアクティビティをトリガーするには、RESTワークフロー/実行APIが使用されます。

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Workflow ID|  &lt;ul&gt;&lt;li&gt;Adobeコンソールで構成されたワークフローのID。&lt;/li&gt;&lt;/ul&gt; |
|Source|  &lt;ul&gt;&lt;li&gt;トリガーリクエストのソースを示すために使用されます。&lt;/li&gt;&lt;/ul&gt; |
|Parameter Map|  &lt;ul&gt;&lt;li&gt;パラメータを使用してワークフローを呼び出すことが可能です。&lt;/li&gt;&lt;li&gt;パラメータの値をその名前にマップします。&lt;/li&gt;&lt;li&gt;String、Number、Boolean、および Date/Time タイプがサポートされています。&lt;/li&gt;&lt;/ul&gt; |

### アクション - プロファイルの作成または更新

プロファイルを取得、作成、または更新するためには、Adobe ProfileAndServices APIにリクエストが送信されます。

詳細については、[APIを使用したプロファイルの作成](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/creating-profiles-api.html)、[APIを使用したプロファイルの更新](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/updating-profiles.html)、および [APIを使用したプロファイルの取得](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/retrieving-profiles.html?lang=en) を参照してください。
##### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新戦略|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;適用可能な更新戦略を選択します。&lt;ul&gt;&lt;li&gt;**新規作成のみ** — 既存のプロファイルを検索し、見つからない場合は新しいプロファイルを作成します。&lt;/li&gt;&lt;li&gt;**更新のみ** — 既存のプロファイルを検索して更新します。&lt;/li&gt;&lt;li&gt;**新規作成または更新** — 既存のプロファイルを検索し、見つかった場合は更新し、そうでない場合は新しいプロファイルを作成します。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|フィルタ|  &lt;ul&gt;&lt;li&gt;更新戦略が **新規作成または更新** または **更新のみ** の場合は必須です。&lt;/li&gt;&lt;li&gt;一意の結果を返すフィルタを選択することを強く推奨します。&lt;/li&gt;&lt;li&gt;詳細については、こちらを参照してください：[複合識別キー](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en)。&lt;/li&gt;&lt;li&gt;検索結果が複数のプロファイルを返した場合、最初のプロファイルのみが更新されます。&lt;/li&gt;&lt;/ul&gt; |
|カスタムフィルタ|  &lt;ul&gt;&lt;li&gt;[カスタムフィルタについて](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;データ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数に名前を付けます。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;本文データで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で指定され、サポートされるフィールドに二重波括弧で注入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |
