---
title: Connect to a data source
description: This article describes how to add and connect data sources to your account.
url: https://docs.tealium.com/server-side/data-sources/connect-to-data-source/
---
## Code and data source key

To install the code for the data source, you need the data source key and links to the installation guides.

To get the data source key:

1. In the sidebar, select **Sources &gt; Data Sources**.
1. Click the name of the data source you want to install to expand the details.
1. From the detailed view, copy the **Data Source Key** value.  
      ![](/images/server-side/whiteui-viewdatasource-datasourcekey.png)
1. Use the installation instructions for your platform to paste the data source key-value into your code.
1. With the data source details expanded, click **Get Code**.  
      ![](/images/server-side/whiteui-editdatasource-getcode.png)The **Get Code** dialog displays. From this dialog, you can download a PDF with installation instructions, view and copy the base code, or view and copy event tracking code.  
      ![](/images/server-side/whiteui-getcode.png)
1. Copy the code displayed in the window.
1. Use the installation instructions for your platform to install the code.
1. Click **Close** to close the Get Code dialog.


## Webhooks

A webhook data source consists of a generated unique URL. The data source key is appended to the webhook URL to make it unique.

A webhook data source URL has the format:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## Verify a data source

After you save and publish and install the code for the data source, verify the setup using Live Events.

Use the following steps to view and verify your data source:

1. With the data source details expanded, click the **Live Events** chart icon to view live events filtered to this data source.
1. In your installation, trigger test events and view them as they display in the Live Events feed.
