---
title: Adjust Events APIコネクタ構成ガイド
description: この記事では、Adjust Events APIコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adjust-events-api-connector/
---
## コネクタアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|イベントを送信| ✗| ✓|
|セッションを送信| ✗| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

* **認証トークン**
  * AdjustのS2S Security機能を使用すると、S2Sイベントのセキュリティを確保し、偽装リクエストから保護できます。
  * S2S認証を構成すると、受信する各リクエストにAdjustダッシュボードで生成されたトークンを含める必要があります。
  * 詳細については、[サーバー間（S2S）セキュリティ](https://dev.adjust.com/en/api/s2s-api/security/)を参照してください。
  * S2S認証を構成していない場合は、このフィールドを空のままにします。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントトークン|  <ul><li>ダッシュボードに表示されるAdjustイベントトークン。</li></ul> |
|アプリトークン|  <ul><li>ダッシュボードに表示されるAdjustアプリトークン。</li></ul> |
|Android ID|  <ul><li>Android ID。</li><li>`android_id`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|ハッシュ化されたAndroid ID（小文字、MD5）|  <ul><li>小文字のAndroid IDのMD5ハッシュ。</li><li>`android_id_lower_md5`としてAdjustに送信されます。</li><li>コネクタは指定された値をそのまま渡し、ハッシュ化しません。</li></ul> |
|ハッシュ化されたAndroid ID（小文字、SHA1）|  <ul><li>小文字のAndroid IDのSHA1ハッシュ。</li><li>`android_id_lower_sha1`としてAdjustに送信されます。</li><li>コネクタは指定された値をそのまま渡し、ハッシュ化しません。</li></ul> |
|ハッシュ化されたAndroid ID（大文字、MD5）|  <ul><li>大文字のAndroid IDのMD5ハッシュ。</li><li>`android_id_upper_md5`としてAdjustに送信されます。</li><li>コネクタは指定された値をそのまま渡し、ハッシュ化しません。</li></ul> |
|ハッシュ化されたAndroid ID（大文字、SHA1）|  <ul><li>大文字のAndroid IDのSHA1ハッシュ。</li><li>`android_id_upper_sha1`としてAdjustに送信されます。</li><li>コネクタは指定された値をそのまま渡し、ハッシュ化しません。</li></ul> |
|Open Advertising ID|  <ul><li>プラットフォーム依存のOpen Advertising ID。</li><li>`oaid`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Raw Amazon Fire Advertising ID|  <ul><li>プラットフォーム依存の未加工のAmazon Fire Advertising ID。</li><li>`fire_adid`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Raw IDFA|  <ul><li>iOSのみ。</li><li>未加工のIDFA識別子。</li><li>`idfa`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Raw IDFV|  <ul><li>未加工のIDFV識別子。</li><li>`idfv`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Raw Google Advertising ID|  <ul><li>未加工のGoogle Advertising ID識別子。</li><li>`gps_adid`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Roku Advertising ID|  <ul><li>Rokuデバイスの広告ID。</li><li>`rida`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Vizio Advertising ID|  <ul><li>Vizioデバイスの広告ID。</li><li>`vida`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Tizen Advertising ID|  <ul><li>Samsung Tizenデバイスの広告ID。</li><li>`tifa`としてAdjustに送信されます。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|Adjust Device ID|  <ul><li>IDFA情報を使用せずにiOS上のLATユーザーを識別します。</li></ul> |
|作成日時のタイムスタンプ（フォーマット済み）|  <ul><li>イベントが発生した正確な時点を指定します。</li><li>コネクタは値をエンコードします。</li><li>例：__ `2017-01-02T15:04:05.000+0000`は`2017-01-02T15%3A04%3A05.000%2B0000`になります。</li></ul> |
|作成日時のタイムスタンプ（Unix）|  <ul><li>イベントが発生した正確な時点を指定します。</li><li>秒またはミリ秒のいずれかで指定できます。</li></ul> |
|IPアドレス|  <ul><li>Googleなどのサードパーティーへのイベントの関連付けや、コールバックに`city`や`postal_code`などの位置情報を含めるために使用します。</li><li>`ip_address`パラメータはIPv4のみを受け付けます。</li><li>IPv6はまだサポートされていません。</li></ul> |
|通貨|  <ul><li>収益イベント</li><li>[通貨コード](https://help.adjust.com/en/article/supported-currencies)を参照してください。</li></ul> |
|環境|  <ul><li>データの送信先となる環境。</li><li>例：`environment=sandbox`または`environment=production`</li><li>このパラメータを指定しない場合、イベントは本番環境に送信されます。</li></ul> |
|収益|  <ul><li>通貨単位で表した収益イベントの値（149.99 = $149.99）。</li><li>Adjustでは、このパラメータに指定できる最小値は0.001です。</li></ul> |
|テンプレート変数|  <ul><li>テンプレート変数をデータ入力として指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数はドット表記で参照します。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。</li></ul> |
|テンプレート|  <ul><li>本文データで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。=.</li><li>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |

### セッションを送信

イベントを送信する前にAdjustとのセッションを確立するには、セッションを送信アクションを使用します。Adjustは、セッションが記録されていないデバイスからのイベントを破棄します。Roku、Vizio、Tizenデバイスへのサーバーサイドデプロイメントなど、ソースがAdjust SDKを介してセッションを開始できない場合に、このアクションを使用します。

動作：

* Adjustは、同じデバイスについて前回のセッションから30分以内に送信されたセッションを無視します。このアクションは、すべてのイベントではなく、セッション開始イベントでトリガーしてください。
* このアクションを使用するには、事前にAdjust側でアプリのサーバー間（S2S）セッションを有効にする必要があります。この機能を有効にするには、Adjustのアカウントマネージャーにお問い合わせください。
#### パラメーター

|**パラメーター**| **説明**|
|---| ---|
|アプリトークン|  <ul><li>ダッシュボードで確認できるAdjustアプリトークン。</li></ul> |
|デバイス識別子|  <ul><li>プラットフォーム固有のデバイスIDまたは広告ID。</li><li>サポートされている各識別子に値をマッピングします。コネクターは、空でない最初の識別子を送信します。</li><li>[デバイス識別子](https://help.adjust.com/en/article/device-identifiers)を参照してください。</li></ul> |
|推奨される追加パラメーター|  <ul><li>セッションを正確にアトリビューションするため、Adjustではセッションに以下のパラメーターを含めることを推奨しています。<ul><li>**AdjustデバイスID**：IDFA情報なしでiOSのLATユーザーを識別します。</li><li>**作成日時のタイムスタンプ（フォーマット済み）**：セッションが発生した正確な時刻を示します。コネクターによって値がエンコードされます。たとえば、`2017-01-02T15:04:05.000+0000`は`2017-01-02T15%3A04%3A05.000%2B0000`になります。</li><li>**作成日時のタイムスタンプ（Unix）**：セッションが発生した正確な時刻を示します。秒またはミリ秒のいずれかで指定できます。</li><li>**IPアドレス**：セッションをサードパーティに関連付け、コールバックに位置情報を含めます。`ip_address`パラメーターはIPv4のみを受け付けます。IPv6はまだサポートされていません。</li></ul></li></ul> |
|セッションパラメーター|  <ul><li>**アプリバージョン**：アプリのバージョン。</li><li>**アプリの短縮バージョン**：アプリの短縮バージョン。</li><li>**OS名**：オペレーティングシステム名。</li><li>**OSバージョン**：オペレーティングシステムのバージョン。</li><li>**デバイスタイプ**：デバイスの種類。</li><li>**デバイス名**：デバイスの名前。</li><li>**国**：国コード。</li><li>**言語**：言語コード。</li><li>**環境**：データの送信先環境（`sandbox`または`production`）。このパラメーターを含めない場合、セッションは本番環境に送信されます。</li><li>**EEA**、**広告のパーソナライズ**、**広告ユーザーデータ**、**NPA**：デジタル市場法（DMA）の同意パラメーター。</li><li>カスタムキー（ドロップダウンにないもの）は、そのまま渡されます。</li></ul> |