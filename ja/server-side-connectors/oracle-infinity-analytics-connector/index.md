---
title: Oracle Infinity Analytics コネクタ構成ガイド
description: この記事では、Oracle Infinity Analyticsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/oracle-infinity-analytics-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Oracle Infinity Analytics Data Collection API
* APIバージョン：v3
* APIエンドポイント：`https://dc.oracleinfinity.io`
* ドキュメンテーション：[Oracle Infinity Analytics Data Collection API](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)

### コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| イベント送信      | ✓                  | ✓               |

### 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントGUID**
  * **Oracle Infinity**ユーザーインターフェースに表示されるアカウントGUID。
  * 詳細については、[Oracle Infinity Analytics Data collection API documentation](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)を参照してください。

### アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

#### アクション - イベント送信

##### パラメータ

| **パラメータ**                | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|:-----------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URI Stem                     | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;URLのホストとポートの後、クエリストリングの前に表示されるURIステム。&lt;/li&gt;&lt;li&gt;通常はユーザーがアクセスした要求ファイルやページ。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                              |
| イベントの種類                | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;追跡するイベントの種類を示す数値識別子を指定します。これはイベントレベルのフィルタリングとレポートに使用されます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                           |
| ビジターID                   | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ビジターIDとして使用され、ファーストパーティクッキーに保存されるランダムな値。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                           |
| Unix Time Stamp              | &lt;ul&gt;&lt;li&gt;ビジターIDとして使用され、ファーストパーティクッキーに保存されるランダムな値。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                            |
| 訪問したドメイン               | &lt;ul&gt;&lt;li&gt;ウェブサイトから送信された場合は必須。&lt;/li&gt;&lt;li&gt;訪問したドメイン、例えば `http://www.example.com`。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                   |
| カスタムビジターID            | &lt;ul&gt;&lt;li&gt;他のシステムで訪問に割り当てることができる一意のカスタムビジターIDを識別します。&lt;/li&gt;&lt;li&gt;これはOracle Infinityタグによって送信される自動生成されたビジターIDパラメータとは別のものです。&lt;/li&gt;&lt;li&gt;カスタム値を送信しない場合、このパラメータは&#34;ヒット&#34;に存在しません。&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| カスタムイベントデータ（アドバンス） | &lt;ul&gt;&lt;li&gt;データ収集に渡すことができる可能性のあるパラメータの説明については、[parameter reference](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/parameters/reference.htm)を参照してください。&lt;/li&gt;&lt;li&gt;送信されるイベントに追加するキー値ペアを指定します。&lt;/li&gt;&lt;li&gt;キー値ペアはチェックやフォーマットなしで&#34;そのまま&#34;追加されます。&lt;/li&gt;&lt;li&gt;配列要素はセミコロン(`;`)で結合されます。&lt;/li&gt;&lt;/ul&gt; |
