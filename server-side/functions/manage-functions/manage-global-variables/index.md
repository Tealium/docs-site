---
title: Manage global variables
description: This article provides information on adding, editing, and deleting global variables that can be used in event, visitor, and data record functions.
url: https://docs.tealium.com/server-side/functions/manage-functions/manage-global-variables/
---
Global variables are variables that can be retrieved by all functions in a profile. These variables can contain numeric or string constants and provide a way to share data with multiple functions.

Global variables are stored as key-value pairs. The key is generated when you create a variable and is based on the variable name. Functions can retrieve the value of a global variable, but cannot modify it. You can add, edit, and delete global variables on the **Code** tab of the functions code editor. 

V3 event, visitor and data record functions can retrieve the value of a global variable using `helper.getGlobalVariable()`. For more information, see [Event and Visitor Functions V3]() and [V3 Event and visitor function examples]().

V2 event and visitor functions can retrieve the value of a global variable using `store.get()`. For more information, see [Event and Visitor Functions V2](). 

## Add a global variable for event or visitor functions

To add a global variable, follow these steps:

1. in the **Server-Side**, go to **Transform &gt; Functions**.
1. Select an event or visitor function, then click the **Code** tab.
1. Click **Global Variables**, then click **&#43; Add Variable**.
1. Enter a **Name** for the variable.  
The **Key** field is automatically populated with the specified name.
1. Enter the **Value** of the variable.
1. Click **Add**, then click **Close**.
1. Click **Save/Publish**.

The following example shows the name, key, and value after creating a global variable named `Cloud Function URL` that contains the URL of a Google cloud function.
![](/images/server-side/functions-global-variable.png)

## Edit a global variable

To edit a global variable, follow these steps:

1. in the **Server-Side**, go to **Transform &gt; Functions**.
1. Select an event or visitor function, then click the **Code** tab.
1. Click **Global Variables**.
1. In the menu for the variable, click **Edit**.
1. Modify the Name and Value as needed, then click **Done**.
1. Click **Close**, then click **Save/Publish**.

## Delete a global variable

To delete a global variable, follow these steps:

1. in the **Server-Side**, go to **Transform &gt; Functions**.
1. Select an event or visitor function, then click the **Code** tab.
1. Click **Global Variables**.
1. In the menu for the variable, click **Delete**.
1. Click **Close**, then click **Save/Publish**.