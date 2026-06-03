---
title: Insightlyコネクタ構成ガイド（廃止）
description: この記事では、Customer Data HubアカウントでInsightlyコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/insightly-connector-deprecated/
---
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。Insightly CRMコネクタについては、[Insightly CRMコネクタ構成ガイド]()を参照してください。

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先を追加| ✓| ✗|
|連絡先を更新| ✓| ✗|
|リードを追加| ✓| ✗|
|リードを更新| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * Insightly APIキーの場所については、次を参照してください：[APIキーの検索またはリセット](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key)

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|名前|  &lt;ul&gt;&lt;li&gt;連絡先の名前。&lt;/li&gt;&lt;li&gt;名前または姓が必要です。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;連絡先の姓。&lt;/li&gt;&lt;li&gt;名前または姓が必要です。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;連絡先の追加属性。&lt;/li&gt;&lt;li&gt;これらのパラメータはInsightly内に存在する必要があります。&lt;/li&gt;&lt;li&gt;利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Contacts/AddContact)。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;連絡先に割り当てるタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先ID|  &lt;ul&gt;&lt;li&gt;更新する連絡先のID。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;連絡先の名前。&lt;/li&gt;&lt;li&gt;名前または姓が必要です。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;連絡先の姓。&lt;/li&gt;&lt;li&gt;名前または姓が必要です。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;更新する追加の属性。&lt;/li&gt;&lt;li&gt;利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Contacts/UpdateContact)。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;更新するタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リードを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|姓|  &lt;ul&gt;&lt;li&gt;リードの姓。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;リードの名前。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;リードの追加属性。&lt;/li&gt;&lt;li&gt;利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Leads/AddLead)。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;リードに割り当てるタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リードを更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リードID|  &lt;ul&gt;&lt;li&gt;更新するリードのID。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;リードの姓。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;リードの名前。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;更新する追加の属性。&lt;/li&gt;&lt;li&gt;利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Leads/UpdateLead)。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;更新するタグ。&lt;/li&gt;&lt;/ul&gt; |
