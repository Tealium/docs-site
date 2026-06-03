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

このコネクタは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下の閾値のいずれかが満たされるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：200
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **サーバーホスト**
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * 例：ドメイン &#34;serverURL&#34; の場合、次の例のURLから `serverURL` をコピーして貼り付けます：`&lt;https://serverURL/nl/jsp/soaprouter.jsp&gt;`
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
|SOAPアクション|  &lt;ul&gt;&lt;li&gt;SOAPアクション。&lt;/li&gt;&lt;li&gt;例：`xtk:session#Logon`&lt;/li&gt;&lt;li&gt;この値はSOAPAction HTTPヘッダーに割り当てられます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストテンプレート変数|  &lt;ul&gt;&lt;li&gt;SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力としてテンプレート変数を提供します（参照：[テンプレート変数ガイド]()）。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数にはドット表記を使用して名前を付けます。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から作成されます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディプレフィックス|  &lt;ul&gt;&lt;li&gt;SOAPリクエストの開始部分のテンプレートを提供します。&lt;/li&gt;&lt;li&gt;例：``` &lt;soapenv:Envelope xmlns:soapenv=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34; xmlns:urn=&#34;urn:xtk:session&#34;&gt;&lt;soapenv:Header/&gt;&lt;soapenv:Body&gt;&lt;urn:Logon&gt;&lt;urn:strLogin&gt;USERNAME&lt;/urn:strLogin&gt;&lt;urn:strPassword&gt;PASSWORD&lt;/urn:strPassword&gt;&lt;urn:elemParameters&gt; ``` &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;USERNAMEとPASSWORDの代わりにあなたのAdobeユーザー名とパスワードを使用します。&lt;/li&gt;&lt;li&gt;SOAPリクエストボディプレフィックスにテンプレート変数を使用することができます。&lt;/li&gt;&lt;li&gt;追加情報については：[テンプレートガイド]()&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディデータ|  &lt;ul&gt;&lt;li&gt;送信するSOAPリクエストバッチアイテムのテンプレートを提供します。&lt;/li&gt;&lt;li&gt;SOAPリクエストボディデータにテンプレート変数を使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディジョイナー|  &lt;ul&gt;&lt;li&gt;バッチング時にボディアイテム間で使用する文字または文字列。&lt;/li&gt;&lt;li&gt;指定されていない場合、空の文字列が使用されます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディサフィックス|  &lt;ul&gt;&lt;li&gt;SOAPリクエストの終了部分のテンプレートを提供します。&lt;/li&gt;&lt;li&gt;例：``` &#34;&amp;lt;/urn:customerId&amp;gt;&amp;lt;/urn:sendCampaign&amp;gt;&amp;lt;/soapenv:Body&amp;gt;&amp;lt;/soapenv:Envelope&gt; ``` &lt;/li&gt;&lt;li&gt;SOAPリクエストボディサフィックスにテンプレート変数を使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPレスポンスエラー識別子|  &lt;ul&gt;&lt;li&gt;レスポンスに以下に指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗とマークされます。&lt;/li&gt;&lt;li&gt;デフォルトでは、HTTPレスポンスステータスが200-299の範囲外の場合も失敗とマークされます。&lt;/li&gt;&lt;/ul&gt; |
