---
title: イベント、訪問、またはデータレコード機能にOAuth 2.0認証を追加する
description: この記事では、イベント、訪問、またはデータレコード機能にOAuth 2.0認証を追加する方法について説明します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/oauth2-authentication/
---
## OAuth 2.0認証を追加する

OAuthは認証のためのオープンスタンダードです。詳細については、[OAuth 2.0](https://oauth.net/2/)を参照してください。

OAuth 2.0認証を追加する前に、別のブラウザタブまたはウィンドウでOAuth APIプロバイダーの構成を開き、Tealium FunctionsとのOAuth統合用に新しいアプリケーションを追加します。

1. 関数を作成した後、**Advanced**タブをクリックします。
1. **Assign Authentications**をクリックします。
1. **+Add Authentication**をクリックし、**OAuth 2.0**を選択して**Continue**をクリックします。
1. **Grant Type**を選択します。
1. アクセストークンの**Name**を入力し、**Next**をクリックします。  
指定された**Name**に基づいて関数のためのユニークなアクセストークン名が生成されます。

**Establish Connection**の手順は、グラントタイプごとに異なります。以下のセクションでは、各グラントタイプについてこれらの手順を説明します。

### 認可コードグラントタイプ

認可コードグラントタイプを使用して接続を確立するには、以下の手順を使用します：

1. **Copy**をクリックしてTealiumリダイレクトURLをコピーします。
1. クライアントアプリケーションの構成にTealiumリダイレクトURLを追加します。
1. **Client Application Credentials**セクションで以下を入力します。  
    * アプリケーションの**Client ID**。Consumer KeyまたはAPI Keyと呼ばれることがあります。
    * アプリケーションからの**Client Secret**。Consumer SecretまたはAPI Secretと呼ばれることがあります。
    * **Scope**（オプション）は、データへのアクセスを制限します。

1. **Endpoint Configuration**セクションで以下を入力します：
    * 認証コードを要求するためのAPIエンドポイントのURLであるAuthorization URL。
    * Authorization URL Query Parameters
    * アクセスおよびリフレッシュトークンを要求するためのAPIエンドポイントのURLであるAccess Token URL。

1. **Establish Connection**をクリックします。  

接続が確立された場合、以下のようなメッセージが表示されます：  
    ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
    接続が確立できなかった場合、その理由に関する情報が含まれたメッセージが表示されます。構成を更新して問題を修正し、再試行してください。
1. **Finish**をクリックします。

### クライアント資格情報グラントタイプ

クライアント資格情報グラントタイプを使用して接続を確立するには、以下の手順を使用します：

1. **Client Application Credentials**セクションで以下を入力します。  
    * アプリケーションの**Client ID**。Consumer KeyまたはAPI Keyと呼ばれることがあります。
    * アプリケーションからの**Client Secret**。Consumer SecretまたはAPI Secretと呼ばれることがあります。
    * **Scope**（オプション）は、データへのアクセスを制限します。

1. **Endpoint Configuration**セクションで以下を入力します：
    * アクセスおよびリフレッシュトークンを要求するためのAPIエンドポイントのURLである**Access Token URL**。
    * 必要に応じて**Access Token URL**の**Authorization URL Query parameters**。

1. **Test Connection**をクリックします。  

接続が確立された場合、以下のようなメッセージが表示されます：  
      ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
      接続が確立できなかった場合、その理由に関する情報が含まれたメッセージが表示されます。構成を更新して問題を修正し、再試行してください。
1. **Finish**をクリックします。

### ユーザーパスワードグラントタイプ

ユーザーパスワードグラントタイプを使用して接続を確立するには、以下の手順を使用します：

1. **Client Application Credentials**セクションで以下を入力します。  
    * アプリケーションの**Client ID**。Consumer KeyまたはAPI Keyと呼ばれることがあります。
    * アプリケーションからの**Client Secret**。Consumer SecretまたはAPI Secretと呼ばれることがあります。
    * **Scope**（オプション）は、データへのアクセスを制限します。

1. **Endpoint Configuration**セクションで以下を入力します：
    * アクセスおよびリフレッシュトークンを要求するためのAPIエンドポイントのURLである**Access Token URL**。
    * 必要に応じて**Access Token URL**の**Authorization URL Query parameters**。

1. **Test Connection**をクリックします。  
接続が確立された場合、以下のようなメッセージが表示されます：  
      ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
      接続が確立できなかった場合、その理由に関する情報が含まれたメッセージが表示されます。構成を更新して問題を修正し、再試行してください。
1. **Finish**をクリックします。