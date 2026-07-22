---
title: Agillic Recipientsコネクタ構成ガイド
description: この記事では、Agillic Recipientsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/agillic-recipients-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|受信者の追加または更新| ✓| ✓|
|受信者テーブルレコードの更新| ✓| ✓|
|イベントの達成| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントID**
  * 必須。
  * あなたのウェブアプリケーションクライアントIDを提供します。
  * 詳細については、[APIを始める：認証](https://developers.agillic.com/apis/getting-started#authentication)を参照してください。

* **クライアントシークレット**
  * 必須。
  * あなたのウェブアプリケーションクライアントシークレットを提供します。

* **日付形式**
  * コネクタの日付形式を構成します。
  * 指定されていない場合、デフォルトの形式`dd.MM.yyyy`が使用されます。
  * 日付とタイムスタンプの形式は、各Agillicアカウントインスタンスに固有です。
  * 形式はAgillic管理インターフェースで定義されます。
  * 詳細については、[APIを始める：日付と時間](https://developers.agillic.com/apis/getting-started#dates-and-time)を参照してください。

* **タイムスタンプ形式**
  * コネクタのタイムスタンプ形式を構成します。
  * 指定されていない場合、デフォルトの形式`dd.MM.yyyy`が使用されます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 受信者の追加または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>必須。</li><li>EMAILやMOBILEなどのユニークなPerson Dataをマップします。</li><li>一般的な目的には受信者IDを使用します。</li><li>詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|受信者データ|  <ul><li>必須。</li><li>Person Dataフィールドに値をマップします。</li></ul> |

#### アクション - 受信者テーブルレコードの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>必須。</li><li>EMAILやMOBILEなどのユニークなPerson Dataをマップします。</li><li>一般的な目的には受信者IDを使用します。</li><li>詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|テーブル|  <ul><li>必須。</li><li>バッチ更新されるレコードのテーブルID。</li></ul> |
|テーブルレコード|  <ul><li>必須。</li><li>各テーブルレコードフィールドに1つ以上の値をマップします。</li><li>IDまたはプライマリキーを指定する必要があります。</li></ul> |

### アクション - イベントの達成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  <ul><li>必須。</li><li>EMAILやMOBILEなどのユニークなPerson Dataをマップします。</li><li>一般的な目的には受信者IDを使用します。</li><li>詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。</li></ul> |
|イベントID|  <ul><li>必須。</li><li>達成するイベントID。</li></ul> |

