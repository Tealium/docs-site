---
title: Microsoft Dynamics 365 コネクタ構成ガイド
description: Microsoft Dynamics 365は、販売、マーケティング、サービス部門のプロセスを効率化し、利益を増加させる多面的なCRMソリューションプラットフォームです。
url: https://docs.tealium.com/ja/server-side-connectors/microsoft-dynamics-365-connector/
---## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先の追加または更新| ✓| ✗|
|連絡先にカスタムエンティティを追加| ✓| ✗|
|リードの追加または更新| ✓| ✗|
|リードを連絡先に変換| ✓| ✗|
|カスタムエンティティの更新| ✓| ✗|
|カスタムエンティティの作成または更新| ✓| ✗|
|連絡先をマーケティングリストに追加| ✓| ✗|
|連絡先をマーケティングリストから削除| ✓| ✗|

## 必要条件

* Microsoft Dynamics 365アカウント
* 組織URI（Microsoftから受け取ったルートWebアドレス）

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法については、[About Connectors]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **組織URI**：必須。Microsoft DynamicsのルートWebアドレスを提供します（例：&lt;https://your-domain.crm.dynamics.com&gt;）。  
URLはセキュアでなければならず、httpsが指定されていない場合は、自動的に&#34;https://&#34;がプレフィックスとして追加されます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

Microsoft Dynamicsアカウントの連絡先、リード、カスタムエンティティは、**To**リストのオプションとして動的に表示されます。探しているオプションが見つからない場合は、まずアカウントに追加する必要があります。

### アクション - 連絡先の追加または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先データ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;属性を追加または更新したいデータオプションにマッピングします。&lt;/li&gt;&lt;/ul&gt; |
|連絡先検索|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;属性を目的の連絡先を検索するための検索オプションにマッピングします。&lt;/li&gt;&lt;li&gt;連絡先が見つかった場合は、そのデータが更新されます。見つからない場合は新しい連絡先が作成されます。&lt;/li&gt;&lt;/ul&gt; |

連絡先フィールドの完全なリストについては、[Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx)を参照してください。

### アクション - 連絡先にカスタムエンティティを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|カスタムエンティティ|  &lt;ul&gt;&lt;li&gt;必須：カスタムエンティティを選択&lt;/li&gt;&lt;/ul&gt; |
|カスタムエンティティと連絡先の関係|  &lt;ul&gt;&lt;li&gt;必須：カスタムエンティティと連絡先を関連付けるルックアップフィールドを選択（参照：[Entity Relationships](https://technet.microsoft.com/en-us/library/dn531171.aspx)）&lt;/li&gt;&lt;/ul&gt; |

### アクション - リードの追加または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リードデータ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;属性を追加または更新したいデータオプションにマッピングします。&lt;/li&gt;&lt;/ul&gt; |
|リード検索|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;属性を目的のリードを検索するための検索オプションにマッピングします。&lt;/li&gt;&lt;li&gt;リードが見つかった場合は、そのデータが更新されます。見つからない場合は新しいリードが作成されます。&lt;/li&gt;&lt;/ul&gt; |

フィールドの完全なリストについては、[Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)を参照してください。

### アクション - カスタムエンティティの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|カスタムエンティティ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;カスタムエンティティを選択&lt;/li&gt;&lt;/ul&gt; |

### アクション - カスタムエンティティの作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新戦略|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;適用可能な更新戦略を選択&lt;/li&gt;&lt;li&gt;作成のみ：ルックアップなしで新しいエンティティを作成&lt;/li&gt;&lt;li&gt;更新のみ：既存のエンティティをルックアップし、それを更新&lt;/li&gt;&lt;li&gt;作成または更新：既存のエンティティをルックアップし、見つかった場合はそれを更新、見つからない場合は新しいエンティティを作成&lt;/li&gt;&lt;/ul&gt; |
|カスタムエンティティ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;カスタムエンティティを選択&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先をマーケティングリストに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|マーケティングリスト|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;連絡先を追加するマーケティングリストを選択。&lt;/li&gt;&lt;li&gt;連絡先を対象とした静的でロックされていないリストのみが表示されます。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先をマーケティングリストから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|マーケティングリスト|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;連絡先を削除するマーケティングリストを選択。&lt;/li&gt;&lt;li&gt;連絡先を対象とした静的でロックされていないリストのみが表示されます。&lt;/li&gt;&lt;/ul&gt; |

## ベンダードキュメンテーション

追加の情報については、以下のベンダードキュメンテーションを参照してください：

* [Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)
* [Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx)
* [新しいエンティティの作成](https://www.microsoft.com/en-us/dynamics/crm-customer-center/create-a-new-entity.aspx)
* [エンティティ関係の作成と編集](https://technet.microsoft.com/en-us/library/dn531171.aspx)

