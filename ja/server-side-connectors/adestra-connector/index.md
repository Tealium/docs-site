---
title: Adestraコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAdestraコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adestra-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先の作成または更新| ✓| ✓|
|リストに連絡先を追加| ✓| ✓|
|リストから連絡先を削除| ✓| ✓|
|メールを送信| ✓| ✓|

## 構成の構成

**Connector Marketplace**に移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **API Key**: 必須: AdestraアカウントのAPIキー、参照：[Create API Token](https://app.adestra.com/doc/page/current/index/integration/zapier/initial-config#Step3:CreateAPITokeninMessageFocus &#34;Create API Token&#34;)

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新戦略|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;適用可能な更新戦略を選択します。  &lt;ul&gt;&lt;li&gt;**作成のみ** 既存の連絡先を検索し、見つからない場合は新しい連絡先を作成します。&lt;/li&gt;&lt;li&gt;**更新のみ** 既存の連絡先を検索し、更新します。&lt;/li&gt;&lt;li&gt;**作成または更新** 既存の連絡先を検索し、見つかった場合は更新し、見つからない場合は新しい連絡先を作成します。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|コアテーブル|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先を作成または更新するコアテーブルを選択します。&lt;/li&gt;&lt;/ul&gt; |
|連絡先検索メールアドレス|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;連絡先を検索するメールアドレス。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リストに連絡先を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|コアテーブル|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;連絡先が所属するコアテーブルを選択します。&lt;/li&gt;&lt;/ul&gt; |
|連絡先検索メールアドレス|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;連絡先を検索するメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|リスト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先を追加するリスト。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リストから連絡先を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|コアテーブル|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;Adestraに連絡先を保存するコアテーブル。&lt;/li&gt;&lt;li&gt;連絡先が所属するコアテーブルを選択します。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メールアドレス|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先を検索するメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|リスト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先を削除するリスト。&lt;/li&gt;&lt;/ul&gt; |

### アクション - メールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メールキャンペーン|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;開始するキャンペーンを選択します。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メールアドレス|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;メールを送信するメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|トランザクションデータ|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;メールキャンペーン内に構成するテンプレートデータ。&lt;/li&gt;&lt;/ul&gt; |

