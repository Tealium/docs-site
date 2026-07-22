---
title: Adobe Campaign Classic Batch コネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAdobe Campaign Classic Batchコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-classic-batch-connector/
---

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|カスタムSOAPリクエストを送信| ✓| ✗|

## バッチの制限

このコネクタは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、以下の閾値のいずれかが満たされるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：200
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **サーバーホスト**
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * 例：ドメイン "serverURL" の場合、次の例のURLから `serverURL` をコピーして貼り付けます：`<https://serverURL/nl/jsp/soaprouter.jsp>`
  * 認証のために、SOAPリクエストボディプレフィックスの一部としてユーザー名とパスワードを提供します。
  * 追加情報については、Adobe Campaign Classicアクセス管理ヘルプドキュメンテーションの[アクセス管理](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en#connectivity)を参照してください。

* **サーバーアドレス**
  * Adobe Campaignサーバーへの完全なURLを指定します。
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * アドレスが提供されている場合、ホストは無視されます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - カスタムSOAPリクエストを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|SOAPアクション|  <ul><li>SOAPアクション。</li><li>例：`xtk:session#Logon`</li><li>この値はSOAPAction HTTPヘッダーに割り当てられます。</li></ul> |
|SOAPリクエストテンプレート変数|  <ul><li>SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力としてテンプレート変数を提供します（参照：[テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)）。</li><li>ネストされたテンプレート変数にはドット表記を使用して名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から作成されます。</li></ul> |
|SOAPリクエストボディプレフィックス|  <ul><li>SOAPリクエストの開始部分のテンプレートを提供します。</li><li>例：``` <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:session"><soapenv:Header/><soapenv:Body><urn:Logon><urn:strLogin>USERNAME</urn:strLogin><urn:strPassword>PASSWORD</urn:strPassword><urn:elemParameters> ``` </li></ul> <ul><li>USERNAMEとPASSWORDの代わりにあなたのAdobeユーザー名とパスワードを使用します。</li><li>SOAPリクエストボディプレフィックスにテンプレート変数を使用することができます。</li><li>追加情報については：[テンプレートガイド](https://docs.tealium.com/about-connector-templates/)</li></ul> |
|SOAPリクエストボディデータ|  <ul><li>送信するSOAPリクエストバッチアイテムのテンプレートを提供します。</li><li>SOAPリクエストボディデータにテンプレート変数を使用することができます。</li></ul> |
|SOAPリクエストボディジョイナー|  <ul><li>バッチング時にボディアイテム間で使用する文字または文字列。</li><li>指定されていない場合、空の文字列が使用されます。</li></ul> |
|SOAPリクエストボディサフィックス|  <ul><li>SOAPリクエストの終了部分のテンプレートを提供します。</li><li>例：``` "&lt;/urn:customerId&gt;&lt;/urn:sendCampaign&gt;&lt;/soapenv:Body&gt;&lt;/soapenv:Envelope> ``` </li><li>SOAPリクエストボディサフィックスにテンプレート変数を使用することができます。</li></ul> |
|SOAPレスポンスエラー識別子|  <ul><li>レスポンスに以下に指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗とマークされます。</li><li>デフォルトでは、HTTPレスポンスステータスが200-299の範囲外の場合も失敗とマークされます。</li></ul> |
