---
title: PersistIQコネクタ構成ガイド
description: PersistIQは、アウトバウンドセールスをより効果的にします。数分でパーソナライズされたキャンペーンを立ち上げ、冷たいリードからの会話を増やします。この記事では、Customer Data HubアカウントでPersistIQコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/persistiq-connector/
---
## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|リードの作成| ✓| ✗|
|リードの更新| ✓| ✗|
|キャンペーンへのリード追加| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**：APIキーは、アカウントデータベースへの読み書きアクセスを許可します。パスワードのように保護してください。このAPIキーは会社全体のキーです。詳細については、[PersistIQのドキュメンテーション](http://apidocs.persistiq.com/#authentication)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - リードの作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|重複|  &lt;ul&gt;&lt;li&gt;スキップまたは更新。デフォルトはスキップです。このエンドポイントについての詳細は、[PersistIQのドキュメンテーション](http://apidocs.persistiq.com/#create-leads)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|作成者ID|  &lt;ul&gt;&lt;li&gt;リードを作成するユーザーのID。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;リードのメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;リードの名前。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;リードの姓。&lt;/li&gt;&lt;/ul&gt; |
|住所|  &lt;ul&gt;&lt;li&gt;リードの住所。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;リードの市区町村。&lt;/li&gt;&lt;/ul&gt; |
|州|  &lt;ul&gt;&lt;li&gt;リードの州。&lt;/li&gt;&lt;/ul&gt; |
|会社名|  &lt;ul&gt;&lt;li&gt;リードに関連する会社名。&lt;/li&gt;&lt;/ul&gt; |
|業界|  &lt;ul&gt;&lt;li&gt;リードの業界。&lt;/li&gt;&lt;/ul&gt; |
|電話|  &lt;ul&gt;&lt;li&gt;リードの電話番号。&lt;/li&gt;&lt;/ul&gt; |
|スニペット|  &lt;ul&gt;&lt;li&gt;リードに関する追加のメモ。&lt;/li&gt;&lt;/ul&gt; |
|スニペット2|  &lt;ul&gt;&lt;li&gt;リードに関する追加のメモ。&lt;/li&gt;&lt;/ul&gt; |
|スニペット3|  &lt;ul&gt;&lt;li&gt;リードに関する追加のメモ。&lt;/li&gt;&lt;/ul&gt; |
|スニペット4|  &lt;ul&gt;&lt;li&gt;リードに関する追加のメモ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リードの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ステータス|  &lt;ul&gt;&lt;li&gt;リードステータスの名前。このエンドポイントについての詳細は、[PersistIQのドキュメンテーション](http://apidocs.persistiq.com/#update-a-lead)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|ステータスID|  &lt;ul&gt;&lt;li&gt;リードステータスのID。&lt;/li&gt;&lt;/ul&gt; |
|バウンス|  &lt;ul&gt;&lt;li&gt;`True`または`false`。`True`はリードをバウンスとして構成します。&lt;/li&gt;&lt;/ul&gt; |
|オプトアウト|  &lt;ul&gt;&lt;li&gt;`True`または`false`。`True`はリードをオプトアウトとして構成します。&lt;/li&gt;&lt;/ul&gt; |
|データ|  &lt;ul&gt;&lt;li&gt;リードのデータ属性。&lt;/li&gt;&lt;/ul&gt; |

### アクション - キャンペーンへのリード追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;リードを追加したいキャンペーンのID。このエンドポイントについての詳細は、[PersistIQのドキュメンテーション](http://apidocs.persistiq.com/#add-lead-to-a-campaign)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|リードID|  &lt;ul&gt;&lt;li&gt;キャンペーンに追加したいリードのID。&lt;/li&gt;&lt;/ul&gt; |
