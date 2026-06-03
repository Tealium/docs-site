---
title: Add authentication to an event, visitor, or data record function
description: This article provides information on adding authentication to an event, visitor, or data record function.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/authentication/
---
Event and visitor functions might require authentication to access some service providers, such as Facebook or Google. To add authentication to a function, you must have an account with the service provider.

## How it works

When you add authentication to a function, an access token is generated and is displayed in the **Advanced** tab of the code editor where you give it a name. Access this authentication in your function by passing that name to [`helper.getAuth()`]().

![](/images/server-side/functions-editor-advanced-tab.png)

Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder. This restriction is to prevent unauthorized access to the token.

For example, if you create an authentication with an access token named `firebase_cloud_messaging`, access that token in your function through an HTTP request using `helper.getAuth(&#39;firebase_cloud_messaging&#39;)`. This feature is commonly used to set authorization headers when making requests to authenticated endpoints:

```js
activate(async ({ visitor, helper }) =&gt; {
  const response = await fetch(
    &#34;https://fcm.googleapis.com/v1/projects/YOURPROJECT/messages:send&#34;,
    {
      method: &#34;POST&#34;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;firebase_cloud_messaging&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body:body
    }
  );
});
```

Outside of an HTTP request, the authentication token is replaced by a UUID placeholder. For example, the following declaration will return the placeholder because it is not within an HTTP request:

```js
const token = helper.getAuth(&#39;firebase_cloud_messaging&#39;);
```

## Supported authentication types

The steps for adding an authentication vary depending on the authentication selected. The following sections provide instructions for adding Facebook, Google, API Key, and UID 2.0 authentication.

For information on adding OAauth 2.0 authentication, see [Add OAuth 2.0 authentication]().

### Facebook authentication

You must log in to Facebook before adding a Facebook authentication. To add Facebook authentication, use the following steps:

1. After you create a function, click the **Advanced** tab.
1. Log in to your Facebook Ad account.
1. Click **Assign Authentications**.
1. Click **&#43;Add Authentication**, then select **Facebook Authentication**, and click **Continue**.
1. Enter a **Name** and click **Connect to Facebook**.  
An authentication token is returned in **User Token**.
1. Click **Add**.

### Google authentication

To add Google authentication, use the following steps:

1. After you create a function, click the **Advanced** tab.
1. Click **Assign Authentications.**
1. Click **&#43;Add Authentication**, then select **Google Authentication**, and click **Continue**.
1. Enter a **Name**, the **Developer Token** name, and click **Connect to Google**.  
An authentication token is returned in **User Token**.
1. Click **Add**.

### API key authentication

To add an API key authentication, use the following steps:

1. After you create a function, click the **Advanced** tab.
1. Click **Assign Authentications**.
1. Click **&#43;Add Authentication**, then select **API Key**, and click **Continue**.
1. Enter a **Name** for the token, and click **Next**.  
A unique access token name for the function is generated based on the specified **Name**.
1. Enter the **API Key**. After you save and publish, the API Key is obfuscated and no longer visible.
1. [Optional] Enter a host name to whitelist.
1. To add an additional host name to whitelist, click **&#43; Add Host Name** and enter the name.
1. Click **Add**.
1. Click **Done**.

## Delete an authentication

Authentications assigned to a function or to a connector cannot be deleted. To delete an authentication, use the following steps:

1. On the **Advanced tab**, click **Assign Authentications**.
1. In the menu for the authentication to be deleted, click **Delete**.  
If the authentication is assigned to a function or a connector, a message is displayed, listing the functions or connectors to which it is assigned. Click **Close**.

      ![](/images/server-side/functionsauthdelete.png)  
      
    If the authentication is not assigned to a function or to a connector, a confirmation dialog is displayed. Click **Delete**.