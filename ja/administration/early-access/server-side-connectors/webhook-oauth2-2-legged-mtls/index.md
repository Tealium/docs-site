---
title: Webhook OAuth2 2-legged mTLS コネクタ
description: Tealiumが生成した相互TLSクライアント証明書を使用してエンドポイントで認証するためのWebhookコネクタを構成します。
url: https://docs.tealium.com/ja/administration/early-access/server-side-connectors/webhook-oauth2-2-legged-mtls/
--- 

<blockquote>
Webhook OAuth2 2-legged mTLSコネクタは現在Early Access中で、選ばれた顧客のみが利用可能です。開始するにはTealiumサポート担当者に連絡してください。
</blockquote>


Webhook OAuth2 2-legged mTLSコネクタは、[OAuth2 2-legged webhook認証](https://docs.tealium.com/webhook-authentication/#oauth2-2-legged)に相互TLS（mTLS）を拡張します。クライアントシークレットを使用する代わりに、TealiumはTLSハンドシェイク中にエンドポイントにDigiCert発行のクライアント証明書を提示します。

## 動作方法

この認証モデルでは、TealiumがTLSクライアントであり、あなたのAPIエンドポイントがTLSサーバーです。

1. TealiumはDigiCertによって署名されたクライアント証明書を生成し、有効期間は1年です。
1. クライアント証明書をダウンロードし、APIゲートウェイまたはサーバー管理者に提供します。
1. サーバーに証明書を信頼させるために、以下のいずれかを構成します：
    * DigiCertのルートおよび中間証明書機関を信頼し、証明書のアイデンティティを検証します。
    * Tealiumが提供する特定のクライアント証明書または証明書のフィンガープリントを明示的に許可します。
1. Tealiumがエンドポイントにリクエストを送信すると、サーバーはTLSハンドシェイク中にクライアント証明書を要求します。
1. Tealiumは証明書を提示し、関連する秘密鍵の所有権を証明します。
1. サーバーは証明書チェーンを検証し、クライアント証明書が構成された信頼要件を満たしていることを確認した後、接続を許可します。

## mTLS認証の構成

mTLS認証を構成するための以下の構成を使用します：

| 構成 | 説明 |
|---------|-------------|
| キーアルゴリズム | クライアント証明書を生成するために使用されるアルゴリズム。セキュリティ要件に基づいて **RSA-2048**、**RSA-3072**、または **RSA-4096** を選択します。 |

WebhookコネクタのmTLS認証を構成するには：

1. コネクタ構成で、認証タイプとして **OAuth2 (2-legged) with mTLS** を選択します。
1. **キーアルゴリズム** を選択し、**生成** をクリックします。
1. **証明書をダウンロード** をクリックし、APIゲートウェイまたはサーバーの管理者に証明書を提供します。

その他のWebhook構成については、[webhook-actions](https://docs.tealium.com/webhook-actions/)を参照してください。
