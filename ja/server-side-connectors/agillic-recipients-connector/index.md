---
title: Agillic Recipientsコネクタ構成ガイド
description: この記事では、Agillic Recipientsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/agillic-recipients-connector/
---
## コネクタアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|受信者の追加または更新| ✓| ✓|
|受信者の追加または更新（バッチ）| ✓| ✓|
|受信者テーブルレコードの更新| ✓| ✓|
|イベントの達成| ✓| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

* **クライアントID**
  * （必須）WebアプリケーションのクライアントIDを指定します。
  * 詳細については、[API入門：認証](https://developers.agillic.com/apis/getting-started#authentication)を参照してください。

* **クライアントシークレット**
  * （必須）Webアプリケーションのクライアントシークレットを指定します。

* **日付形式**
  * コネクタの日付形式を構成します。
  * 指定しない場合、デフォルト形式の`dd.MM.yyyy`が使用されます。
  * 日付およびタイムスタンプの形式は、Agillicアカウントのインスタンスごとに異なります。
  * 形式はAgillic Administrationインターフェイスで定義します。
  * 詳細については、[API入門：日付と時刻](https://developers.agillic.com/apis/getting-started#dates-and-time)を参照してください。

* **タイムスタンプ形式**
  * コネクタのタイムスタンプ形式を構成します。
  * 指定しない場合、デフォルト形式の`dd.MM.yyyy`が使用されます。

## アクション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### 受信者の追加または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>（必須）EMAILやMOBILEなど、一意の個人データをマッピングします。</li><li>汎用的な用途には受信者IDを使用します。</li><li>詳細については、[API：Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|受信者データ|  <ul><li>（必須）個人データフィールドに値をマッピングします。</li></ul> |

### 受信者の追加または更新（バッチ）

### バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。以下のいずれかのしきい値に達するか、プロファイルが公開されるまで、リクエストはキューに保持されます。

* リクエストの最大数：1000
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：5 MB

### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>（必須）EMAILやMOBILEなど、一意の個人データをマッピングします。</li><li>汎用的な用途には受信者IDを使用します。</li><li>詳細については、[API：Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|受信者データ|  <ul><li>（必須）個人データフィールドに値をマッピングします。</li></ul> |
| 受信者ID属性名 |<ul><li>（任意）既存の受信者との照合に使用する個人データ値を上書きします。</li><li>EMAILやMOBILEなど、一意の個人データをマッピングします。</li><li>詳細については、[API：Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |

### 受信者テーブルレコードの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>（必須）EMAILやMOBILEなど、一意の個人データをマッピングします。</li><li>汎用的な用途には受信者IDを使用します。</li><li>詳細については、[API：Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|テーブル|  <ul><li>（必須）バッチ更新するレコードのテーブルIDです。</li></ul> |
|テーブルレコード|  <ul><li>（必須）各テーブルレコードフィールドに1つ以上の値をマッピングします。</li><li>IDまたは主キーを指定する必要があります。</li></ul> |

### イベントの達成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>（必須）EMAILやMOBILEなど、一意の個人データをマッピングします。</li><li>汎用的な用途には受信者IDを使用します。</li><li>詳細については、[API：Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|イベントID|  <ul><li>（必須）達成するイベントのIDです。</li></ul> |