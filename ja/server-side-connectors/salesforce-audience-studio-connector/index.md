---
title: Salesforce Audience Studio コネクタ構成ガイド
description: この記事では、Salesforce Audience Studioコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-audience-studio-connector/
---
## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ピクセルを送信| ✓| ✓|
|イベントを送信| ✓| ✓|
|トランザクションを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ピクセルを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ドメイン|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。&lt;/li&gt;&lt;/ul&gt; |
|パブリッシャーUUID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。&lt;/li&gt;&lt;/ul&gt; |
|サイト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。&lt;/li&gt;&lt;/ul&gt; |
|ユニークユーザーID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;/ul&gt; |
|セクション|  &lt;ul&gt;&lt;li&gt;データを送信したいアプリケーションのセクションです。&lt;/li&gt;&lt;li&gt;例えば、`open_app`や`home_page`など&lt;/li&gt;&lt;/ul&gt; |
|ブラウザ属性|  &lt;ul&gt;&lt;li&gt;ユーザーエージェントデータを補完するために送信する必要があるすべてのブラウザ属性データ。&lt;/li&gt;&lt;/ul&gt; |
|追加情報|  &lt;ul&gt;&lt;li&gt;追加情報については、[Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews)のドキュメンテーションを参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントURLエンドポイント|  &lt;ul&gt;&lt;li&gt;イベントURLは[Salesforce Audience Studio UI](https://console.krux.com/events/list)で作成されます。&lt;/li&gt;&lt;/ul&gt; |
|ユニークユーザーID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トランザクションを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユニークユーザーID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;/ul&gt; |
|トランザクションURLエンドポイント|  &lt;ul&gt;&lt;li&gt;トランザクションデータを送信するためにSalesforce Audience Studioの担当者から提供されるURL。&lt;/li&gt;&lt;/ul&gt; |
|パブリッシャーUUID|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;この値を取得するには、Salesforce Audience Studioの担当者に連絡してください。&lt;/li&gt;&lt;/ul&gt; |
|注文合計|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;/ul&gt; |
|数量|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;/ul&gt; |
|トランザクション日|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;/ul&gt; |
|追加情報|  &lt;ul&gt;&lt;li&gt;追加情報については、[Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews)のドキュメンテーションを参照してください。&lt;/li&gt;&lt;/ul&gt; |
