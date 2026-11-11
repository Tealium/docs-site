---
title: Adobe Campaign v8 コネクタ構成ガイド
description: この記事では、Adobe Campaign v8 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-v8-connector/
---
## 構成

Tealium で Adobe Campaign v8 コネクタを構成するには、まず Adobe で接続用の OAuth サーバー間資格情報を生成する必要があります。詳細については、[Adobe：OAuth サーバー間資格情報を使用したプロジェクトへの API の追加](https://developer.adobe.com/developer-console/docs/guides/services/services-add-api-oauth-s2s/)を参照してください。

Adobe の資格情報を生成してコネクタを構成するには、次の手順を実行します。

1. 新しい Adobe Developer Console プロジェクトを作成するか、既存のプロジェクトを使用します。詳細については、[Adobe：プロジェクトの概要](https://developer.adobe.com/developer-console/docs/guides/projects/)を参照してください。
1. プロジェクトの資格情報に関連付ける Adobe サービスをプロジェクトに追加します。詳細については、[Adobe：サービスの概要](https://developer.adobe.com/developer-console/docs/guides/services/)を参照してください。このコネクタには、次のサービスが必要です。
    * Adobe Campaign API
    * I/O Management API
1. これらの資格情報を使用して管理する Adobe Campaign API 製品プロファイルを選択します。
1. プロジェクトにサービスを追加すると、プロジェクトの資格情報にアクセスできるようになります。詳細については、[Adobe：資格情報](https://developer.adobe.com/developer-console/docs/guides/credentials/)を参照してください。  
プロジェクトの概要に移動し、**資格情報**セクションで**OAuth サーバー間**を選択します。このコネクタには、次の資格情報が必要です。
    * クライアント ID（API キー）
    * クライアントシークレット
    * テクニカルアカウントのメールアドレス
1. 資格情報を記録し、Tealium に戻ってコネクタの構成を完了します。
1. Tealium でコネクタマーケットプレイスに移動し、新しい Adobe Campaign v8 コネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。
1. コネクタを追加したら、次の構成を行います。
    * **クライアント ID**  
        * （必須）クライアント ID（API キー）。
    * **クライアントシークレット**  
        * （必須）クライアントシークレット。
    * **サーバーホスト**  
        * （必須）サーバーホストを指定します。  
        たとえば、API URL が `https://example.campaign.adobe.com/nl/jsp/soaprouter.jsp` の場合、ホストは `example.campaign.adobe.com` です。
1. Adobe で、**Adobe Admin** コンソールの**開発者**セクションに移動します。詳細については、[Adobe：開発者の管理](https://helpx.adobe.com/enterprise/using/manage-developers.html#add-developers)を参照してください。
1. Adobe プロジェクトの資格情報に含まれるテクニカルアカウントのメールアドレスを使用して、新しい開発者を追加します。
1. 追加した開発者に Adobe Campaign v8 へのアクセス権を付与します。
    1. **Adobe Admin** コンソールからユーザーを追加します。
    1. 先ほど追加した開発者のメールアドレスを追加します。
    1. 資格情報を作成する際に、Adobe Campaign Managed Cloud サービスを追加し、選択した製品プロファイルを含めます。
    詳細については、[Adobe：ユーザー権限の管理](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/admin/permissions/manage-permissions)を参照してください。
1. Adobe Campaign クライアントコンソールで、新しく作成されたテクニカル演算子を更新します。詳細については、[Adobe：Campaign クライアントコンソール内でのテクニカルアカウント演算子の更新](https://experienceleague.adobe.com/en/docs/campaign/technotes-ac/tn-new/ims-migration#ims-migration-step-9)を参照してください。

## 移行

Adobe Campaign Classic to v8 Migrator ツールを使用して、既存の Adobe Campaign Classic コネクタを Adobe Campaign v8 コネクタに移行します。

Tealium Tools を使用して Adobe Analytics タグを移行するには、次の手順を実行します。

1. 次の URL にある JSON 定義を使用して、Adobe Campaign Classic to v8 Migrator を Tealium Tools に追加します：`https://solutions.tealium.net/hosted/tealiumTools/acc_to_v8/acc_to_v8.json`。カスタムツールの追加について詳しくは、[カスタムツールの管理](https://docs.tealium.com/tealium-tools-browser-extension/#add-a-custom-tool)を参照してください。
1. **イベントコネクタ**または**オーディエンスコネクタ**に移動し、Tealium Tools から Adobe Campaign Classic to v8 Migrator ツールを起動します。
1. アクションの移行方法を選択します。移行の一環として既存の Adobe Campaign Classic アクションを無効にするには、**既存のアクションを無効化**を選択します。アクティブなアクションのみを移行するには、**アクティブなアクションのみを移行**を選択します。
1. ドロップダウンリストから移行範囲を選択します。
    * すべての Adobe Campaign Classic アクション
    * 特定の Adobe Campaign Classic アクション
    * 特定の Adobe Campaign Classic コネクタ
1. プロジェクトの Adobe Campaign クライアント ID とクライアントシークレットを入力します。サーバーホストは、既存の Adobe Campaign Classic 構成から自動的に抽出されます。
1. **開始**をクリックします。  
Migrator ツールによって、既存の Adobe Campaign Classic コネクタが新しい Adobe Campaign v8 コネクタに自動的に移行されます。コネクタ名は同じですが、接尾辞として `V8 (Migrated)` がエンリッチメントされます。
1. 新しいコネクタの構成とアクションを確認します。
1. プロファイルを保存してパブリッシュします。

## 許可する IP アドレス

[Tealium の IP アドレス](https://docs.tealium.com/ip-allow-list/)を [Adobe Campaign の許可リスト](https://experience.adobe.com/#/controlpanel/instances)（**Adobe Experience Platform** > **コントロールパネル** > **インスタンス**）に追加する必要があります。

詳細については、[Adobe Campaign：IP アドレスの許可リスト登録](https://experienceleague.adobe.com/en/docs/control-panel-learn/tutorials/instance-settings/allowlist-ip-adresses)を参照してください。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| カスタム SOAP リクエストを送信（バッチ処理） | ✓ | ✓ |
| カスタム SOAP リクエストを送信 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### カスタム SOAP リクエストを送信（バッチ処理）

#### バッチ制限

このアクションでは、ベンダーへの大量のデータ転送をサポートするために、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに格納されます。

* リクエストの最大数：200
* 最も古いリクエストからの最大経過時間：10 分
* リクエストの最大サイズ：1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| SOAP アクションヘッダー値 | `SOAP` アクション（例：`nms:rtEvent#PushEvent`）。<br>この値は `SOAPAction` `HTTP` ヘッダーに割り当てられます。 |
| SOAP リクエスト本文のプレフィックス | `SOAP` リクエストの開始部分のテンプレートを指定します。例：<br>`<?xml version="`1`.0" encoding="utf-`8`"?><soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:nms:rtEvent"><soapenv:Header/><soapenv:Body><urn:PushEvent><urn:domEvent>`。<br>`SOAP` リクエスト本文のプレフィックスでは、テンプレート変数を使用できます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |
| SOAP リクエスト本文データ | 送信する `SOAP` リクエストのバッチ項目用テンプレートを指定します。<br>`SOAP` リクエスト本文データでは、テンプレート変数を使用できます。 |
| SOAP リクエスト本文のサフィックス | `SOAP` リクエストの終了部分のテンプレートを指定します。例：<br>`</urn:domEvent></urn:PushEvent></soapenv:Body></soapenv:Envelope>`。<br>`SOAP` リクエスト本文のサフィックスでは、テンプレート変数を使用できます。 |
| SOAP リクエスト本文の結合文字列 | バッチ処理時に本文の項目間で使用する文字または文字列。指定しない場合は、空の文字列が使用されます。 |
| SOAP リクエストテンプレート変数 | `SOAP Request Body Prefix`、`SOAP Request Body Data`、`SOAP Request Body Suffix` のデータ入力として使用するテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。 |
| SOAP レスポンスエラー識別子 | レスポンスにエラー文字列が含まれている場合、失敗としてマークされます。デフォルトでは、`200`～`299` の範囲外の `HTTP` レスポンスステータスも失敗としてマークされます。 |

### カスタム SOAP リクエストを送信
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| SOAPアクションヘッダー値 | `SOAP`アクション（例：`nms:rtEvent#PushEvent`）。<br>この値は`SOAPAction` `HTTP`ヘッダーに構成されます。 |
| SOAPリクエストボディテンプレート | 送信する`SOAP`リクエストボディテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされているフィールドに二重波括弧で名前を指定して挿入します。例：`{{SomeTemplateName}}`。 |
| SOAPリクエストボディテンプレート変数 | `SOAP Request Body Template`へのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。ネストされたテンプレート変数には、`items.name`のようにドット記法で名前を付けます。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。 |
| SOAPレスポンスエラー識別子 | レスポンスにエラー文字列が含まれている場合、失敗としてマークされます。デフォルトでは、`200`～`299`の範囲外の`HTTP`レスポンスステータスも失敗としてマークされます。 |