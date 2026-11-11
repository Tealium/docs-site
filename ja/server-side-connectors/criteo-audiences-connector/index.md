---
title: Criteo Audiencesコネクタ構成ガイド
description: この記事では、Criteo Audiencesコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/criteo-audiences-connector/
---

<blockquote>
訪問データをCriteoに送信するには、[Criteo Audiences（OAuth）コネクタ](https://docs.tealium.com/criteo-audiences-oauth-connector/)の使用を推奨します。OAuthコネクタでは、Criteoアカウントの認証情報と認可コードフローを使用することで、セキュリティとプライバシーをエンリッチメントし、アカウント管理を容易にします。
</blockquote>


## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ユーザーをオーディエンスに追加| ✓| ✓|
|ユーザーをオーディエンスから削除| ✓| ✓|

### API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Criteo API
* APIバージョン：2026-01
* APIエンドポイント：`https://api.criteo.com/2025-07/audiences`
* ドキュメント：[Criteo：Audiences API](https://developers.criteo.com/marketing-solutions/docs/audiences)

### バッチ制限

このコネクタでは、ベンダーへの大量データ転送に対応するため、リクエストをバッチ処理します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：50000
* 最も古いリクエストからの最大経過時間：15分
* リクエストの最大サイズ：10 MB

## 構成の構成

### Criteoに同意リンクをリクエストする

このコネクタを使用する場合は、[asintegrations@tealium.com](mailto:asintegrations@tealium.com)にメールを送信し、Tealium Customer Data Hubが広告主に代わってオーディエンスを管理することを承認する同意リンクを受け取ってください。詳細については、[Criteo Developers：ユーザーへの認可リクエストの送信](https://developers.criteo.com/marketing-solutions/docs/authorization-requests)を参照してください。


<blockquote>
この手順の承認には、最大3営業日かかる場合があります。
</blockquote>


Criteoのアクティベーションリンクを受け取ったら、次の手順を実行します。

1. 提供されたアクティベーションリンクをクリックします。  
**Criteo Consent Portal**が表示されます。
1. アカウントに対して要求された認可レベルを付与します。

### コネクタの追加と構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **広告主ID（必須）**  
Criteoアカウントのインテグレーションに関連付けられている**広告主ID**を構成します。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ユーザーをオーディエンスに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オーディエンス| ユーザーの追加先となるオーディエンスを選択するか、オーディエンスIDを入力します。 |
| 識別子 | ユーザー識別子の値をマッピングします。<ul><li>**メール**：組み込みのハッシュ処理を適用せず、メールアドレスの値をそのまま送信します。値をハッシュ化する必要がない場合、またはすでにハッシュ化されている場合は、このオプションを選択します。</li><li>**メール（MD5ハッシュを適用）**：送信前にメールアドレスの値をMD5でハッシュ化します。</li><li>**メール（MD5 SHA256ハッシュを適用）**：送信前にメールアドレスの値をMD5でハッシュ化し、その後SHA256でハッシュ化します。</li><li>**モバイルID**：Appleの場合はIDFAモバイルID、Androidの場合はADIDモバイルID。</li><li>**Identity Link**：Identity Link</li><li>**Gum ID**：Cookieマッチングから取得した識別子。対応するGum Caller IDがリクエストに自動的に追加されます。</li></ul> |
| Gum Caller ID | Gum Caller `ID` - Criteoが`GUM`（Generative Unified Media）のソルティングに使用する値。Tag ManagementのCriteo Cookie Matching Serviceタグを使用している場合は、マッピングしないでください。 |

### アクション - ユーザーをオーディエンスから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オーディエンス| ユーザーの削除元となるオーディエンスを選択するか、オーディエンスIDを入力します。 |
| 識別子 | ユーザー識別子の値をマッピングします。<ul><li>**メール**：組み込みのハッシュ処理を適用せず、メールアドレスの値をそのまま送信します。値をハッシュ化する必要がない場合、またはすでにハッシュ化されている場合は、このオプションを選択します。</li><li>**メール（MD5ハッシュを適用）**：送信前にメールアドレスの値をMD5でハッシュ化します。</li><li>**メール（MD5 SHA256ハッシュを適用）**：送信前にメールアドレスの値をMD5でハッシュ化し、その後SHA256でハッシュ化します。</li><li>**モバイルID**：Appleの場合はIDFAモバイルID、Androidの場合はADIDモバイルID。</li><li>**Identity Link**：Identity Link</li><li>**Gum ID**：Cookieマッチングから取得した識別子。対応するGum Caller IDがリクエストに自動的に追加されます。</li></ul> |
| Gum Caller ID | Gum Caller `ID` - Criteoが`GUM`のソルティングに使用する値。Tag ManagementのCriteo Cookie Matching Serviceタグを使用している場合は、マッピングしないでください。 |