---
title: Retentlyコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでRetentlyコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/retently-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|顧客の作成または更新| ✓| ✗|
|調査の送信| ✓| ✗|
|顧客の退会| ✓| ✗|
|顧客の削除| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIキー**：APIキーは、Retentlyアカウントの構成の下で見つけることができます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 顧客の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://www.retently.com/api/#api-create-or-update-customers-post&gt;&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;顧客の名前。&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;顧客の姓。&lt;/li&gt;&lt;/ul&gt; |
|Company|  &lt;ul&gt;&lt;li&gt;顧客に割り当てられた会社名。&lt;/li&gt;&lt;/ul&gt; |
|Tag|  &lt;ul&gt;&lt;li&gt;顧客に割り当てるタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 調査の送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Campaign|  &lt;ul&gt;&lt;li&gt;キャンペーン識別子。トランザクション型のキャンペーンでなければなりません。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://www.retently.com/api/#api-send-survey-post&gt;&lt;/li&gt;&lt;/ul&gt; |
|Email|  &lt;ul&gt;&lt;li&gt;顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://www.retently.com/api/#api-create-or-update-customers-post&gt;&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;顧客の名前。&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;顧客の姓。&lt;/li&gt;&lt;/ul&gt; |
|Company|  &lt;ul&gt;&lt;li&gt;顧客に割り当てられた会社名。&lt;/li&gt;&lt;/ul&gt; |
|Tag|  &lt;ul&gt;&lt;li&gt;顧客に割り当てるタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 顧客の退会

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;退会するメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://www.retently.com/api/#api-unsubscribe-customers-post&gt;&lt;/li&gt;&lt;/ul&gt; |
|Message|  &lt;ul&gt;&lt;li&gt;オプトアウトメッセージ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 顧客の削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;削除する顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：&lt;https://www.retently.com/api/#api-delete-customers-delete&gt;&lt;/li&gt;&lt;/ul&gt; |
