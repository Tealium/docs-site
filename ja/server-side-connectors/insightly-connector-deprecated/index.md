---
title: Insightlyコネクタ構成ガイド（廃止）
description: この記事では、Customer Data HubアカウントでInsightlyコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/insightly-connector-deprecated/
---

<blockquote>
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。Insightly CRMコネクタについては、[Insightly CRMコネクタ構成ガイド](https://docs.tealium.com/insightly-crm-connector/)を参照してください。
</blockquote>


## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先を追加| ✓| ✗|
|連絡先を更新| ✓| ✗|
|リードを追加| ✓| ✗|
|リードを更新| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|名前|  <ul><li>連絡先の名前。</li><li>名前または姓が必要です。</li></ul> |
|姓|  <ul><li>連絡先の姓。</li><li>名前または姓が必要です。</li></ul> |
|属性|  <ul><li>連絡先の追加属性。</li><li>これらのパラメータはInsightly内に存在する必要があります。</li><li>利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Contacts/AddContact)。</li></ul> |
|タグ|  <ul><li>連絡先に割り当てるタグ。</li></ul> |

### アクション - 連絡先を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先ID|  <ul><li>更新する連絡先のID。</li></ul> |
|名前|  <ul><li>連絡先の名前。</li><li>名前または姓が必要です。</li></ul> |
|姓|  <ul><li>連絡先の姓。</li><li>名前または姓が必要です。</li></ul> |
|属性|  <ul><li>更新する追加の属性。</li><li>利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Contacts/UpdateContact)。</li></ul> |
|タグ|  <ul><li>更新するタグ。</li></ul> |

### アクション - リードを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|姓|  <ul><li>リードの姓。</li></ul> |
|名前|  <ul><li>リードの名前。</li></ul> |
|属性|  <ul><li>リードの追加属性。</li><li>利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Leads/AddLead)。</li></ul> |
|タグ|  <ul><li>リードに割り当てるタグ。</li></ul> |

### アクション - リードを更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リードID|  <ul><li>更新するリードのID。</li></ul> |
|姓|  <ul><li>リードの姓。</li></ul> |
|名前|  <ul><li>リードの名前。</li></ul> |
|属性|  <ul><li>更新する追加の属性。</li><li>利用可能な属性のリストについては、次を参照してください：[Insightlyのドキュメンテーション](https://api.insight.ly/v2.3/Help#!/Leads/UpdateLead)。</li></ul> |
|タグ|  <ul><li>更新するタグ。</li></ul> |
