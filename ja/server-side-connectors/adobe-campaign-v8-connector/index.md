---
title: Adobe Campaign v8 コネクタ構成ガイド
description: この記事では、Adobe Campaign v8 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-v8-connector/
---
## 構成

TealiumでAdobe Campaign v8コネクタを構成するには、まずAdobeでOAuthサーバー間認証のためのクレデンシャルを生成する必要があります。詳細については、[Adobe: OAuthサーバー間認証を使用してプロジェクトにAPIを追加する](https://developer.adobe.com/developer-console/docs/guides/services/services-add-api-oauth-s2s/)を参照してください。

Adobeのクレデンシャルを生成し、コネクタを構成するには、以下の手順を完了してください：

1. 新しいAdobe Developer Consoleプロジェクトを作成するか、既存のプロジェクトを使用します。詳細については、[Adobe: プロジェクト概要](https://developer.adobe.com/developer-console/docs/guides/projects/)を参照してください。
1. プロジェクトのクレデンシャルに関連付けたいAdobeサービスをプロジェクトに追加します。詳細については、[Adobe: サービス概要](https://developer.adobe.com/developer-console/docs/guides/services/)を参照してください。このコネクタには以下のサービスが必要です：
    * Adobe Campaign API
    * I/O Management API
1. これらのクレデンシャルで管理したいAdobe Campaign API製品プロファイルを選択します。
1. サービスをプロジェクトに追加した後、プロジェクトのクレデンシャルにアクセスできます。詳細については、[Adobe: クレデンシャル](https://developer.adobe.com/developer-console/docs/guides/credentials/)を参照してください。
プロジェクト概要に移動し、**クレデンシャル**セクションで**OAuthサーバー間**を選択します。このコネクタに必要なクレデンシャルは以下の通りです：
    * クライアントID（APIキー）
    * クライアントシークレット
    * テクニカルアカウントのメール
1. クレデンシャルをメモして、コネクタの構成を完了するためにTealiumに戻ります。
1. Tealiumでコネクタマーケットプレイスに移動し、新しいAdobe Campaign v8コネクタを追加します。コネクタの追加方法についての一般的な説明については、[コネクタについて]()を参照してください。
1. コネクタを追加した後、次の構成を構成します：
    * **クライアントID**  
        * （必須）クライアントID（APIキー）。
    * **クライアントシークレット**  
        * （必須）クライアントシークレット。
    * **サーバーホスト**  
        * （必須）サーバーホストを提供します。  
        例えば、API URL `https://example.campaign.adobe.com/nl/jsp/soaprouter.jsp`のホストは`example.campaign.adobe.com`です。
1. Adobeで、**Adobe Admin**コンソールの**開発者**セクションに移動します。詳細については、[Adobe: 開発者の管理](https://helpx.adobe.com/enterprise/using/manage-developers.html#add-developers)を参照してください。
1. Adobeプロジェクトのクレデンシャルからテクニカルアカウントのメールを使用して新しい開発者を追加します。
1. 追加した開発者にAdobe Campaign v8へのアクセスを許可します。
    1. **Adobe Admin**コンソールからユーザーを追加します。
    1. 追加した開発者のメールを追加します。
    1. Adobe Campaign Managed Cloudサービスを追加し、クレデンシャルを作成する際に選択した製品プロファイルを含めます。
    詳細については、[Adobe: ユーザー権限の管理](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/admin/permissions/manage-permissions)を参照してください。
1. Adobe Campaignクライアントコンソールで新しく作成された技術オペレータを更新します。詳細については、[Adobe: Campaignクライアントコンソール内の技術アカウントオペレータを更新する](https://experienceleague.adobe.com/en/docs/campaign/technotes-ac/tn-new/ims-migration#ims-migration-step-9)を参照してください。

## 移行

Adobe Campaign ClassicコネクタをAdobe Campaign V8コネクタに移行するには、Adobe Campaign Classicからv8 Migratorツールを使用します。

Tealium Toolsを使用してAdobe Analyticsタグを移行するには、次の手順を完了してください：

1. 次のURLでJSON定義を使用してTealium ToolsにAdobe Campaign Classicからv8 Migratorを追加します：`https://solutions.tealium.net/hosted/tealiumTools/acc_to_v8/acc_to_v8.json`。カスタムツールの追加方法については、[カスタムツールの管理]()を参照してください。
1. **イベントコネクタ**または**オーディエンスコネクタ**に移動し、Tealium ToolsからAdobe Campaign Classicからv8 Migratorツールを起動します。
1. アクションの移行方法を選択します。既存のAdobe Campaign Classicアクションを無効にするには、**既存のアクションを無効にする**を選択します。アクティブなアクションのみを移行するには、**アクティブなアクションのみを移行する**を選択します。
1. ドロップダウンリストから移行の範囲を選択します：
    * すべてのAdobe Campaign Classicアクション
    * 特定のAdobe Campaign Classicアクション
    * 特定のAdobe Campaign Classicコネクタ
1. プロジェクトのAdobe CampaignクライアントIDとクライアントシークレットを入力します。サーバーホストは既存のAdobe Campaign Classic構成から自動的に抽出されます。
1. **開始**をクリックします。  
Migratorツールは自動的に既存のAdobe Campaign Classicコネクタを新しいAdobe Campaign v8コネクタに移行します。コネクタの名前は同じで、接尾辞は`V8 (Migrated)`になります。
1. 新しいコネクタの構成とアクションを確認します。
1. プロファイルを保存して公開します。

## 許可するIPアドレス

[Tealium IPアドレス]()を[Adobe Campaign許可リスト](https://experience.adobe.com/#/controlpanel/instances)（**Adobe Experience Platform** &gt; **Control Panel** &gt; **Instances**）に追加する必要があります。

詳細については、[Adobe Campaign: IPアドレスの許可リスト](https://experienceleague.adobe.com/en/docs/control-panel-learn/tutorials/instance-settings/allowlist-ip-adresses)を参照してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Custom SOAP Request (Batched) | ✓ | ✓ |
| Send Custom SOAP Request | ✓ | ✓ |

アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### Send Custom SOAP Request (Batched)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。以下のいずれかの閾値に達するまでリクエストがキューに入れられます：

* 最大リクエスト数：200
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| SOAPアクションヘッダー値 | 例：`nms:rtEvent#PushEvent`の`SOAP`アクション。&lt;br&gt;この値は`SOAPAction` `HTTP`ヘッダーに割り当てられます。 |
| SOAPリクエストボディプレフィックス | `SOAP`リクエストの開始部分のテンプレートを提供します。例：&lt;br&gt;`&lt;?xml version=&#34;`1`.0&#34; encoding=&#34;utf-`8`&#34;?&gt;&lt;soapenv:Envelope xmlns:soapenv=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34; xmlns:urn=&#34;urn:nms:rtEvent&#34;&gt;&lt;soapenv:Header/&gt;&lt;soapenv:Body&gt;&lt;urn:PushEvent&gt;&lt;urn:domEvent&gt;`。&lt;br&gt;`SOAP`リクエストボディプレフィックスでテンプレート変数を使用できます。詳細については、を参照してください。 |
| SOAPリクエストボディデータ | `SOAP`リクエストバッチアイテムを送信するためのテンプレートを提供します。&lt;br&gt;`SOAP`リクエストボディデータでテンプレート変数を使用できます。 |
| SOAPリクエストボディサフィックス | `SOAP`リクエストの終了部分のテンプレートを提供します。例：&lt;br&gt;`&lt;/urn:domEvent&gt;&lt;/urn:PushEvent&gt;&lt;/soapenv:Body&gt;&lt;/soapenv:Envelope&gt;`。&lt;br&gt;`SOAP`リクエストボディサフィックスでテンプレート変数を使用できます。 |
| SOAPリクエストボディジョイナー | バッチ処理時にボディアイテム間に使用する文字または文字列。指定されていない場合は空文字列が使用されます。 |
| SOAPリクエストテンプレート変数 | `SOAPリクエストボディプレフィックス`、`SOAPリクエストボディデータ`、`SOAPリクエストボディサフィックス`のデータ入力用のテンプレート変数を提供します。詳細については、を参照してください。&lt;br&gt;例えば、`items.name`のようにドット表記でネストされたテンプレート変数を名前付けします。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| SOAPレスポンスエラー識別子 | レスポンスにエラー文字列が含まれている場合、それは失敗としてマークされます。デフォルトでは、`200`-`299`範囲外の`HTTP`レスポンスステータスも失敗としてマークされます。 |

### Send Custom SOAP Request


#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| SOAP アクションヘッダー値 | 例：`nms:rtEvent#PushEvent`の`SOAP`アクション。この値は`SOAPAction` `HTTP`ヘッダーに割り当てられます。 |
| SOAP リクエストボディテンプレート | 送信する`SOAP`リクエストボディテンプレートを提供します。詳細については、を参照してください。テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例えば、`{{SomeTemplateName}}`。 |
| SOAP リクエストボディテンプレート変数 | `SOAP リクエストボディテンプレート`のデータ入力としてテンプレート変数を提供します。詳細については、を参照してください。ドット表記を使用してネストされたテンプレート変数を名前付けします。例えば`items.name`。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| SOAP レスポンスエラー識別子 | レスポンスにエラー文字列が含まれている場合、それは失敗としてマークされます。デフォルトでは、`200`-`299`範囲外の`HTTP`レスポンスステータスも失敗としてマークされます。 |