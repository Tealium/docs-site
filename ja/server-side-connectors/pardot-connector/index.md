---
title: 顧客データプラットフォーム（CDP）向けSalesforce Pardotコネクタ構成ガイド
description: この記事では、Customer Data HubプロファイルでSalesforce Pardotコネクタサービスを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pardot-connector/
---
Salesforce Pardotコネクタを使用すると、オーディエンスに基づいて1対1のメールを送信できます。

## 要件

* PardotビジネスユニットID
* Salesforce SSO

## サポートされるアクション

|**アクション名**| **オーディエンスによるトリガー**| **ストリームによるトリガー**|
|---| ---| ---|
|プロスペクトにメールを送信| ✓| x|
|プロスペクトを作成または更新| ✓| x|
|プロスペクトをリストに追加| ✓| x|
|プロスペクトをリストからオプトアウト| ✓| x|
|プロスペクトをリストから削除| ✓| x|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

1. **Configuration**タブで、**Add Connector**をクリックします。
1. コネクタの名前と実装に関するメモを入力します。
1. **Account Type**で、接続先のアカウントタイプ（**Developer**、**Sandbox**、または**Production**）を選択します。
1. **Pardot Business Unit ID**を入力します。
    * この値を確認するには、Salesforceで**Setup**に移動し、**Quick Find**ボックスに**Business Unit Setup**と入力します。
    * **Pardot Business Unit ID**は`OUv`で始まる18文字の値です。
1. **Establish Connection**をクリックします。
    * Salesforceのログインウィンドウが表示されます。Salesforce SSOの認証情報を入力し、**Log In**をクリックします。
    * MFAが有効になっている場合は、Salesforceへのログインを確認する必要があります。

## アクション構成 - パラメータとオプション

**Continue**をクリックしてコネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - プロスペクトにメールを送信

#### パラメータ

* **Campaign**：（必須）使用するキャンペーンを選択します。目的のキャンペーンが表示されない場合は、キャンペーンIDをカスタム値として入力できます。

<blockquote>
キャンペーンIDを確認するには、Pardotで対象のキャンペーンを開き、URLの末尾にある数値を確認します。たとえば、URLが`https://pi.pardot.com/campaign/read/id/123`の場合、IDは`123`です。キャンペーンIDの詳細については、[1対1のメールの送信](http://developer.pardot.com/kb/api-version-4/emails/#sending-one-to-one-emails)および[サポートされるパラメータ](http://developer.pardot.com/kb/api-version-4/emails/#supported-parameters_1)の記事を参照してください。
</blockquote>

* **Email Template**：（必須）使用するメールテンプレートを選択します。目的のメールテンプレートがこのリストに表示されない場合は、テンプレートIDをカスタム値として入力できます。


<blockquote>
キャンペーンIDと同様に、メールテンプレートIDはPardotのメールテンプレートURLの末尾にある数値です。テンプレートURLは`https://pi.pardot.com/emailTemplate/read/id/XXXX`のようになり、`XXXX`が数値IDです。
</blockquote>


* **Prospect Identifier**：（必須）プロスペクトの検索に使用する識別子を選択します。
  * **prospect_email:** プロスペクトに関連付けられたメールアドレス
  * **id:** プロスペクトに関連付けられたPardot ID

#### オプション（任意）

##### 追加のメールオプション

「Email Template」の属性を上書きするには、このセクションを構成します。テンプレートのサポート：`subject`、`text_content`、`html_content`オプションはテンプレート機能をサポートしています。これらのオプションでは、テンプレート名を参照してテンプレートからメッセージデータを生成します。

|オプション| 説明|
|---| ---|
|`subject`| メールの件名。構成する場合、値には**Templates**セクションのテンプレートキーを指定します|
|`text_content`| メールのテキスト本文。構成する場合、値には**Templates**セクションのテンプレートキーを指定します。テンプレートには`%%unsubscribe%%`または`%%email_preference_center%%`のいずれかを含める必要があります|
|`html_content`| メールのHTML本文。構成する場合、値には**Templates**セクションのテンプレートキーを指定します。テンプレートには`%%unsubscribe%%`または`%%email_preference_center%%`のいずれかを含める必要があります|
|`tags[]`| 1つまたは複数のタグに対して「array/set」属性タイプを構成します。これは、このメールに作成または関連付けるタグの名前です|
|`list_ids[]`| 1つまたは複数のリストに対して「array/set」属性タイプを構成します。これは、メールの送信先となるリストのIDです|
|`suppression_list_ids[]`| 1つまたは複数のリストに対して「array/set」属性タイプを構成します。これは、メール送信の対象外とするリストのIDです|

* `email_template_id`が指定されていない場合は、`(from_email & from_name)`または`from_user_id`のいずれかが必要です
* **Email Template**セクションが構成されていない場合は、`name`、`subject`、および`text_content`または`html_content`のいずれかが必要です
* **Email Template**セクションが構成されている場合は、メールテンプレートが最初に使用されます。`name`、`replyto_email`、`subject`、`text_content`、`html_content`が指定されている場合は、テンプレートの内容が上書きされます

##### テンプレート変数

* テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。
* ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`
* ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます

##### テンプレート

* メッセージデータ内で参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。
* サポートされているフィールドでは、二重波かっこを使用してテンプレートを名前で挿入します。例：`{{SomeTemplateName}}`

### アクション - プロスペクトを作成または更新

#### パラメータ

* **Prospect Lookup Identifier:**（必須）プロスペクトの検索に使用する識別子を選択します。
  * 詳細については、[プロスペクトの作成と更新](http://developer.pardot.com/kb/api-version-4/prospects/)を参照してください。
  * プロスペクトの検索には、次のいずれかのオプションを選択してください。
    * Prospect Email (email)：メールアドレス
    * Prospect ID (id)：プロスペクトの一意のID
    * Prospect FID (fid)：プロスペクトのCRM ID

*. **Campaign:**（必須）使用するキャンペーンを選択します。目的のキャンペーンが表示されない場合は、キャンペーンIDをカスタム値として入力できます。

<blockquote>
キャンペーンIDを確認するには、Pardotで対象のキャンペーンを開き、URLの末尾にある数値を確認します。たとえば、URLが`https://pi.pardot.com/campaign/read/id/123`の場合、IDは`123`です。
</blockquote>


* **Create If Not Exists:**（任意）プロスペクトの作成を許可する場合は選択します。

* **Create Prospect Data**
  * （必須）メールアドレス
  * プロスペクトを作成する際は、このセクションのフィールド構成が使用されます

* **Update Prospect Data**
  * （必須）プロスペクトを更新する際は、このセクションのフィールド構成が使用されます

### アクション - プロスペクトをリストに追加

#### パラメータ

* **Target List:**（必須）プロスペクトの追加先となるリスト。
[「Supported Parameters」の「create」オプション](http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)を参照してください。
  

<blockquote>
ドロップダウンに表示されないリストを追加する必要がある場合は、URL `https://pi.pardot.com/list/read/id/XXXX`でリストIDを確認できます。
</blockquote>


* **Prospect Identifier:**（必須）プロスペクトの検索に使用する識別子を選択します。
  * **prospect\_email:** プロスペクトに関連付けられたメールアドレス
  * **id:** プロスペクトを識別するPardot ID

### アクション - プロスペクトをリストからオプトアウト
#### パラメーター

* **対象リスト：**（必須）プロスペクトを追加するリスト。
参照：［サポートされているパラメーターの「create」オプション］(http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)
  

<blockquote>
If you need to add a list that you don't see in the dropdown, you can find the list ID at the URL: `https://pi.pardot.com/list/read/id/XXXX`
</blockquote>


* **プロスペクト識別子：**（必須）プロスペクトの検索に使用する識別子を選択します。
  * **prospect_email：** プロスペクトに関連付けられたメールアドレス
  * **id：** プロスペクトを識別する Pardot ID

### アクション - リストからプロスペクトを削除

#### パラメーター

* **対象リスト**（必須）プロスペクトを追加するリスト。
参照：［サポートされているパラメーターの「delete」オプション］(http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)
  

<blockquote>
If you need to add a list that you don't see in the dropdown, you can find the list ID at the URL: `https://pi.pardot.com/list/read/id/XXXX`
</blockquote>


* **プロスペクト検索識別子：**（必須）プロスペクトの検索に使用する識別子を選択します。
  * **prospect_email：** プロスペクトに関連付けられたメールアドレス
  * **id：** プロスペクトを識別する Pardot ID

## ベンダーのドキュメント

* [プロスペクトはキャンペーンにどのように関連付けられますか？](http://help.pardot.com/customer/en/portal/articles/2128387-how-are-prospects-associated-with-campaigns-#setting-campaigns-with-the-api)
* [1 対 1 のメールの送信](http://developer.pardot.com/kb/api-version-4/emails/#sending-one-to-one-emails)
* [サポートされているパラメーター](http://developer.pardot.com/kb/api-version-4/emails/#supported-parameters_1)