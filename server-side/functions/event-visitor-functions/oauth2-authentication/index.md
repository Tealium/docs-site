---
title: Add OAuth 2.0 authentication to an event, visitor, or data record function
description: This article provides information on adding OAuth 2.0 authentication to an event, visitor, or data record function.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/oauth2-authentication/
---
## Add OAuth 2.0 authentication

OAuth is an open standard for authentication. For more information, see [OAuth 2.0](https://oauth.net/2/).

Before you add OAuth 2.0 authentication, open your OAuth API provider settings in a different browser tab or window and add a new application for your OAuth integration with Tealium Functions.

1. After you create a function, click the **Advanced** tab.
1. Click **Assign Authentications**.
1. Click **+Add Authentication**, then select **OAuth 2.0**, and click **Continue**.
1. Select the **Grant Type**.
1. Enter a **Name** for the access token, and click **Next**.  
A unique access token name for the function is generated based on the specified **Name**.

The steps for **Establish Connection** vary for each grant type. The following sections describe these steps for each grant type.

### Authorization code grant type

To establish a connection using the authorization code grant type, use the following steps:

1. Click **Copy** to copy the Tealium Redirect URL.
1. Add the Tealium Redirect URL to the settings for your client application.
1. In the **Client Application Credentials** section, enter the following.  
    * **Client ID** for your application. May be called Consumer Key or API Key.
    * **Client Secret** from your application. May be called Consumer Secret or API Secret.
    * **Scope** (Optional) to limit access to your data.

1. In the **Endpoint Configuration** section, enter the following
    * Authorization URL, which is the URL of the API endpoint used to request an authorization code.
    * Authorization URL Query Parameters
    * Access Token URL, which is the URL of the API endpoint used to request access and refresh tokens.

1. Click **Establish Connection**.  

If the connection was established, a message similar to the following is displayed:  
    ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
    If the connection could not be established, the message includes information on the reason. Update your configuration to correct the problem and try again.
1. Click **Finish**.

### Client credential grant type

To establish a connection using the client credential grant type, use the following steps:

1. In the **Client Application Credentials** section, enter the following.  
    * **Client ID** for your application. May be called Consumer Key or API Key.
    * **Client Secret** from your application. May be called Consumer Secret or API Secret.
    * **Scope** (Optional) to limit access to your data.

1. In the **Endpoint Configuration** section, enter the following:
    * **Access Token URL** for the API endpoint used to request access and refresh tokens.
    * **Authorization URL Query parameters** for **the Access Token URL**, if needed.

1. Click **Test Connection**.  

If the connection was established, a message similar to the following is displayed:  
      ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
      If the connection could not be established, the message includes information on the reason. Update your configuration to correct the problem and try again.
1. Click **Finish**.

### User password grant type

To establish a connection using the user password grant type, use the following steps:

1. In the **Client Application Credentials** section, enter the following.  
    * **Client ID** for your application. May be called Consumer Key or API Key.
    * **Client Secret** from your application. May be called Consumer Secret or API Secret.
    * **Scope** (Optional) to limit access to your data.

1. In the **Endpoint Configuration** section, enter the following:
    * **Access Token URL** for the API endpoint used to request access and refresh tokens.
    * **Authorization URL Query parameters** for the **Access Token URL**, if needed.

1. Click **Test Connection**.  
If the connection was established, a message similar to the following is displayed:  
      ![](https://docs.tealium.com/images/server-side/connectionestablishedmsg.png)  
      If the connection could not be established, the message includes information on the reason. Update your configuration to correct the problem and try again.
1. Click **Finish**.