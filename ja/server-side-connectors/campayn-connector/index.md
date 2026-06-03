---
title: Campaynコネクタ構成ガイド
description: この記事では、Campaynコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/campayn-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|基本的なサインアップ| ✓| ✗|
|連絡先の退会| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIキー**
  * あなたのAPIキーはCampaynアカウントで見つけることができます。
  * 詳細については、GitHubの[Campayn API](https://github.com/nebojsac/Campayn-API)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 基本的なサインアップ

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;追加するリストのID。&lt;/li&gt;&lt;li&gt;詳細については、GitHubの[Campayn API Contacts ](https://github.com/nebojsac/Campayn-API/blob/master/endpoints/contacts.md)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;サインアップするユーザーのメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|重複時に失敗|  &lt;ul&gt;&lt;li&gt;値は `true` または `false` です。&lt;/li&gt;&lt;li&gt;`true` の場合、ユーザーが既に存在するときに呼び出しが失敗します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先の退会

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;連絡先が退会するリストのID。&lt;/li&gt;&lt;li&gt;詳細については、GitHubの[ Campayn API Lists](https://github.com/nebojsac/Campayn-API/blob/master/endpoints/lists.md)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;退会する連絡先のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
