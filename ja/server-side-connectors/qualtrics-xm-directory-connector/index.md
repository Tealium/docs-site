---
title: Qualtrics XMディレクトリコネクタ構成ガイド
description: この記事では、Qualtrics XMディレクトリコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/qualtrics-xm-directory-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Qualtrics XM Directory API
* APIバージョン：v3
* APIエンドポイント：`https://ca1.qualtrics.com`
* ドキュメンテーション：[Qualtrics XM Directory API](https://api.qualtrics.com/api-reference/docs/api-reference.md)

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ディレクトリコンタクトの作成または更新| ✓| ✓|
|コンタクトトランザクションの作成| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **データセンターID**
  * データセンターIDは、**アカウント構成** &gt; **Qualtrics IDs**&gt; **IDs** &gt; **Box User**に移動することで見つけることができます。
* **クライアントID**
  * Qualtrics XM Directory APIにアクセスできるウェブアプリケーションのクライアントIDを提供します。
  * クライアントIDは、**アカウント構成** **&gt; Qualtrics IDs &gt;** **OAuthクライアントマネージャー**に移動することで見つけることができます。
  * Qualtrics XM Directory APIのOAuthクライアントマネージャーページには、以下の**許可タイプ**が含まれている必要があります：
    * `client_credentials` および **スコープ**は次のようになります：`manage:contact_transactions`, `manage:directory_contacts`, `read:directories`, および `read:mailing_lists`。
  * 追加情報については、[OAuth認証（クライアント資格情報）](https://api.qualtrics.com/api-reference/docs/Instructions/oauth-authentication.md)および[OAuth 2.0スコープ](https://api.qualtrics.com/api-reference/docs/Instructions/oauthscopes.md)を参照してください。
* **クライアントシークレット**
  * ウェブアプリケーションのクライアントシークレットを提供します。

 
<blockquote>
Qualtrics内でアプリケーションを作成する際には、リダイレクトURLをTealium環境と一致させるように構成します。例：SSOが有効な顧客の場合は[https://sso.tealiumiq.com/oauth/qualtrics/callback.html](https://sso.tealiumiq.com/oauth/qualtrics/callback.html)、標準の顧客の場合は[https://my.tealiumiq.com/oauth/qualtrics/callback.html](https://my.tealiumiq.com/oauth/qualtrics/callback.html)。
</blockquote>
 

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ディレクトリコンタクトの作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新戦略|  <ul><li>必須。</li><li>適用可能な更新戦略を選択します。  <ul><li>**作成のみ**：既存のコンタクトを検索し、見つからない場合は新しいコンタクトを作成します。</li><li>**更新のみ**：既存のコンタクトを検索し、更新します。</li><li>**作成または更新**：既存のコンタクトを検索し、見つかった場合は更新し、見つからない場合は新しいコンタクトを作成します。</li></ul> </li></ul> |
|ディレクトリ|  <ul><li>必須</li><li>コンタクトを作成または更新するディレクトリを選択します。</li></ul> |
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|埋め込みデータ|  <ul><li>埋め込みデータオブジェクトには、コンタクトに関連付けたい追加のメタデータが含まれています。</li><li>このユーザー定義データには、出生地、性別、雇用状況などのデータが含まれることがあります。</li></ul> |
|ContactId|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|

### アクション - コンタクトトランザクションの作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ディレクトリ|  <ul><li>必須</li><li>コンタクトを作成または更新するディレクトリを選択します。</li></ul> |
|メーリングリスト|  <ul><li>必須</li><li>コンタクトトランザクションを作成するメーリングリストを選択します。</li></ul> |
|ContactId|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|トランザクション日|

