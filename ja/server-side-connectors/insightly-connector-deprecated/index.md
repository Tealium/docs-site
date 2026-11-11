---
title: Insightlyコネクタ構成ガイド（非推奨）
description: この記事では、Customer Data HubアカウントでInsightlyコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/insightly-connector-deprecated/
---

<blockquote>
このコネクタは非推奨となり、タグマーケットプレイスでは利用できなくなりました。Insightly CRMコネクタについては、[Insightly CRMコネクタ構成ガイド](https://docs.tealium.com/insightly-crm-connector/)を参照してください。
</blockquote>


## コネクタのアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|連絡先を追加| ✓| ✗|
|連絡先を更新| ✓| ✗|
|リードを追加| ✓| ✗|
|リードを更新| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **APIキー**
  * Insightly APIキーの確認場所については、[APIキーの確認またはリセット](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - 連絡先を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|名|  <ul><li>連絡先の名。</li><li>名または姓のいずれかが必要です。</li></ul> |
|姓|  <ul><li>連絡先の姓。</li><li>名または姓のいずれかが必要です。</li></ul> |
|属性|  <ul><li>連絡先の追加属性。</li><li>これらのパラメータはInsightly内に存在している必要があります。</li><li>利用可能な属性のリストについては、[Insightlyのドキュメント](https://api.insight.ly/v2.3/Help#!/Contacts/AddContact)を参照してください。</li></ul> |
|タグ|  <ul><li>連絡先に割り当てるタグ。</li></ul> |

### アクション - 連絡先を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先ID|  <ul><li>更新する連絡先のID。</li></ul> |
|名|  <ul><li>連絡先の名。</li><li>名または姓のいずれかが必要です。</li></ul> |
|姓|  <ul><li>連絡先の姓。</li><li>名または姓のいずれかが必要です。</li></ul> |
|属性|  <ul><li>更新する追加属性。</li><li>利用可能な属性のリストについては、[Insightlyのドキュメント](https://api.insight.ly/v2.3/Help#!/Contacts/UpdateContact)を参照してください。</li></ul> |
|タグ|  <ul><li>更新するタグ。</li></ul> |

### アクション - リードを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|姓|  <ul><li>リードの姓。</li></ul> |
|名|  <ul><li>リードの名。</li></ul> |
|属性|  <ul><li>リードの追加属性。</li><li>利用可能な属性のリストについては、[Insightlyのドキュメント](https://api.insight.ly/v2.3/Help#!/Leads/AddLead)を参照してください。</li></ul> |
|タグ|  <ul><li>リードに割り当てるタグ。</li></ul> |

### アクション - リードを更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リードID|  <ul><li>更新するリードのID。</li></ul> |
|姓|  <ul><li>リードの姓。</li></ul> |
|名|  <ul><li>リードの名。</li></ul> |
|属性|  <ul><li>更新する追加属性。</li><li>利用可能な属性のリストについては、[Insightlyのドキュメント](https://api.insight.ly/v2.3/Help#!/Leads/UpdateLead)を参照してください。</li></ul> |
|タグ|  <ul><li>更新するタグ。</li></ul> |