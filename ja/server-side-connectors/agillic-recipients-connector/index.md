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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()の記事を参照してください。

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
|受信者ID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;EMAILやMOBILEなどのユニークなPerson Dataをマップします。&lt;/li&gt;&lt;li&gt;一般的な目的には受信者IDを使用します。&lt;/li&gt;&lt;li&gt;詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|受信者データ|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;Person Dataフィールドに値をマップします。&lt;/li&gt;&lt;/ul&gt; |

#### アクション - 受信者テーブルレコードの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;EMAILやMOBILEなどのユニークなPerson Dataをマップします。&lt;/li&gt;&lt;li&gt;一般的な目的には受信者IDを使用します。&lt;/li&gt;&lt;li&gt;詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|テーブル|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;バッチ更新されるレコードのテーブルID。&lt;/li&gt;&lt;/ul&gt; |
|テーブルレコード|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;各テーブルレコードフィールドに1つ以上の値をマップします。&lt;/li&gt;&lt;li&gt;IDまたはプライマリキーを指定する必要があります。&lt;/li&gt;&lt;/ul&gt; |

### アクション - イベントの達成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|受信者ID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;EMAILやMOBILEなどのユニークなPerson Dataをマップします。&lt;/li&gt;&lt;li&gt;一般的な目的には受信者IDを使用します。&lt;/li&gt;&lt;li&gt;詳細については、[APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|イベントID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;達成するイベントID。&lt;/li&gt;&lt;/ul&gt; |

