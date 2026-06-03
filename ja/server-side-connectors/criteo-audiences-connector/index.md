---
title: Criteo Audiences コネクタ構成ガイド
description: この記事では、Criteo Audiences コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/criteo-audiences-connector/
---
訪問データをCriteoに送信するために、[Criteo Audiences (OAuth) コネクタ]()の使用をお勧めします。OAuthコネクタは、Criteoアカウントの認証情報とAuthorization Codeフローを使用して、セキュリティ、プライバシーの向上とアカウント管理を容易にします。

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザーをオーディエンスに追加| ✓| ✓|
|ユーザーをオーディエンスから削除| ✓| ✓|

### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名: Criteo API
* APIバージョン: 2025-07
* APIエンドポイント: `https://api.criteo.com/2025-07/audiences`
* ドキュメント: [Criteo: Audiences API](https://developers.criteo.com/marketing-solutions/docs/audiences)

### バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 50000
* 最古のリクエストからの最大時間: 15分
* リクエストの最大サイズ: 10 MB

## 構成の構成

### Criteoから同意リンクをリクエスト

このコネクタを使用する場合は、[asintegrations@tealium.com](mailto:asintegrations@tealium.com)にメールを送り、広告主に代わってTealium Customer Data Hubがオーディエンスを管理するための同意リンクを受け取ってください。詳細については、[Criteo Developers: Send an Authorization Request to Your Users](https://developers.criteo.com/marketing-solutions/docs/authorization-requests)を参照してください。

この手続きには最大3営業日かかる場合があります。

Criteoのアクティベーションリンクを受け取った後、次の手順を完了します：

1. 提供されたアクティベーションリンクをクリックします。  
**Criteo同意ポータル**が表示されます。
1. アカウントの要求された認証レベルを付与します。

### コネクタを追加して構成を構成

コネクタマーケットプレースにアクセスして、プロファイルにCriteo Audience Matchコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview]()を参照してください。

コネクタを追加した後、次の構成を構成します：

* **広告主ID（必須）**  
Criteoアカウント内の統合に関連付けられた**広告主ID**を構成します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーをオーディエンスに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オーディエンス| オーディエンスを選択するか、ユーザーを追加するオーディエンスIDを入力します。 |
| 識別子 | ユーザー識別値をマッピングします。 &lt;ul&gt;&lt;li&gt;**Email**: ハッシュ化せずにそのままのメール値を送信します。値がハッシュ化されていない場合やすでにハッシュ化されている場合は、このオプションを選択します。&lt;/li&gt;&lt;li&gt;**Email (MD5ハッシュを適用)**: 送信前にMD5でメール値をハッシュ化します。&lt;/li&gt;&lt;li&gt;**Email (MD5およびSHA256ハッシュを適用)**: MD5でメール値をハッシュ化した後、SHA256で再ハッシュ化します。&lt;/li&gt;&lt;li&gt;**モバイルID**: AppleのIDFAモバイルID、AndroidのADIDモバイルID。&lt;/li&gt;&lt;li&gt;**Identity Link**: Identity Link&lt;/li&gt;&lt;li&gt;**Gum ID**: クッキーマッチングから取得した識別子。対応するGum Caller IDが自動的にリクエストに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| Gum Caller ID | Gum Caller `ID` - Criteoが`GUM`（Generative Unified Media）のソルティングに使用する値です。Tealium iQ Criteo Cookie Matching Serviceタグを使用している場合は、この項目をマッピングしないでください。 |

### アクション - ユーザーをオーディエンスから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オーディエンス| オーディエンスを選択するか、ユーザーを削除するオーディエンスIDを入力します。 |
| 識別子 | ユーザー識別値をマッピングします。 &lt;ul&gt;&lt;li&gt;**Email**: ハッシュ化せずにそのままのメール値を送信します。値がハッシュ化されていない場合やすでにハッシュ化されている場合は、このオプションを選択します。&lt;/li&gt;&lt;li&gt;**Email (MD5ハッシュを適用)**: 送信前にMD5でメール値をハッシュ化します。&lt;/li&gt;&lt;li&gt;**Email (MD5およびSHA256ハッシュを適用)**: MD5でメール値をハッシュ化した後、SHA256で再ハッシュ化します。&lt;/li&gt;&lt;li&gt;**モバイルID**: AppleのIDFAモバイルID、AndroidのADIDモバイルID。&lt;/li&gt;&lt;li&gt;**Identity Link**: Identity Link&lt;/li&gt;&lt;li&gt;**Gum ID**: クッキーマッチングから取得した識別子。対応するGum Caller IDが自動的にリクエストに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| Gum Caller ID | Gum Caller `ID` - Criteoが`GUM`（Generative Unified Media）のソルティングに使用する値です。Tealium iQ Criteo Cookie Matching Serviceタグを使用している場合は、この項目をマッピングしないでください。 |